# CLAUDE.md

Notes for Claude Code (and other coding agents) working in this repository.

## What this is

An interactive, illustrated textbook — *Homology & Cohomology: an illustrated journey* —
built as a prerendered SvelteKit static site: 32 chapters (~250k words, ~280 figures),
live 3D figures (three.js + custom GLSL), math rendered at build time (KaTeX), and a
small tested math engine. Every push to `main` deploys to GitHub Pages via
`.github/workflows/deploy.yml` (Node 22, `npm ci` → test → build), so run the full gate
before pushing.

## Commands

```sh
npm install
npm run dev          # vite dev server
npm test             # vitest run — tests live at src/**/*.test.ts
npm run check        # TeX-aware svelte-check wrapper — must report 0 errors
npm run build        # static site into build/ (BASE_PATH=/homology for the Pages URL)
```

- `node scripts/chapter-stats.mjs` — per-chapter word/figure/exercise counts.
- Knot geometry is generated, never hand-drawn: `npx vite-node scripts/knot-shapes.ts`
  (env knobs: `FLAT`, `OUT`, `STEPS`, `TOL`, `ALPHA`, `BETA`; args are knot ids) writes
  `src/lib/knots/shapes.json` / `shapes-space.json`; `knots.test.ts` verifies the result.
- `scripts/knot-invariants.ts` regenerates `src/lib/knots/invariants.json`.

## Read this before writing content

`docs/AUTHORING.md` is the house guide and canonical reference: voice and pedagogy,
chapter anatomy, notation conventions, the concept ledger (§5 — which chapter may
introduce which idea; binding), colour semantics (§6), the full component library (§7),
figure design rules (§8), and the verification checklist (§11). Read it fully before
touching chapters or figures. This file only covers what breaks the build.

## Layout

- `src/lib/content/toc.ts` — the table of contents: single source of truth for parts,
  chapters, numbering, prereqs and reading time. Nav, sidebar, the map and prev/next
  links all derive from it. Adding a chapter = entry here + route folder + glossary file.
- `src/routes/(book)/<part>/<slug>/+page.svelte` — one Svelte file per chapter; you
  write only the body (the layout supplies title block, headings numbering, nav).
- `src/lib/components/` — `prose/` (Definition, Theorem, Figure, Exercise, Term, Ref,
  Cite, …), `ui/` (Slider, Toggle, Segmented, StepControls, …), `svg/` (Svg, SvgTeX,
  ComplexView2D, GluingSquare), `three/` (Scene3D), `layout/`, `map/`.
- `src/lib/figures/<part>/<slug>/` — per-chapter figure components and `.ts` helpers.
- `src/lib/math/` — tested math engine: `SimplicialComplex`, homology over ℤ/ℤ2/ℚ,
  Smith normal form, persistence, Hodge decomposition, worked examples.
- `src/lib/knots/` — knot table, diagrams, invariants, generated shape JSONs, a worker.
- `src/lib/katex/` — build-time math preprocessor, macro definitions, a11y labels.
- `src/lib/content/` — glossary (`glossary/<part>--<slug>.ts`, double dash), `bib/`,
  `notation.ts`, `people.ts`, `conjectures.ts`; all guarded by tests.
- `scripts/` — the check wrapper, chapter stats, knot generators.

## Hard rules (the build and tests enforce these)

1. **Math syntax.** Inline `\( … \)`, display `\[ … \]`, written directly in template
   markup; a Svelte preprocessor renders it at build time. Math may not appear inside
   an attribute string — pass a snippet instead (`{#snippet head()}…{/snippet}` for
   callout titles, `caption` for figures). Never write a literal `{` or `}` in prose
   outside math (Svelte parses it as an expression). Dynamic math: `<TeX tex={…} />`.
   TeX errors fail `npm run build` with file:line.
2. **`npm run check` is the linter.** It wraps svelte-check and drops diagnostics that
   fall inside TeX ranges (plain svelte-check never runs the KaTeX preprocessor and
   reports floods of false errors). Use the wrapper as-is; it hides nothing else.
3. **Macros and notation.** `\Z`, `\Z/n`, `\im`, `\ip{a}{b}`, `\set{…}`, colour macros
   `\cyc{}`/`\bdy{}`/`\chn{}`/`\hole{}` … are defined in `src/lib/katex/macros.js`.
   Notation is conventional across the book (e.g. `\Z/n`, never `\Z_n`) — the table in
   AUTHORING §4 is binding.
4. **Svelte 5 runes only** (`$state`, `$derived`, `$effect`, snippets) — no legacy
   `let`-reactivity. Known pitfall: in `$effect`, read every reactive value *before*
   any `api?.…` call, or the effect tracks nothing and controls silently die.
5. **TypeScript strict mode; no new npm dependencies** without asking.
6. **Colour semantics are fixed and shared with prose** (gold = cycles/highlight,
   teal = boundaries, violet = chains, rose = holes/obstructions, blue = neutral
   structure, green = exercises/success; amber = warnings). Dark night-sky backgrounds
   only — never white inside figures.
7. **Content tests are structural.** `src/lib/content/*.test.ts` check figure numbering
   (`num="chapter.k"` in document order), the required closing sections (Exercises,
   Summary, Further reading), glossary anchors and see-also keys, that every `<Term>`,
   `<Ref>` and `<Cite>` resolves, and that each conjecture record appears exactly once.
   When adding content, make these tests pass — don't weaken them.
8. **Quotes and history must be verified** against primary sources. No invented or
   misattributed epigraphs; if it can't be verified, don't quote it.
9. **Generated files**: `src/lib/knots/shapes.json`, `shapes-space.json` and
   `invariants.json` come from `scripts/` — regenerate, never hand-edit.

## Conventions

- Tabs for indentation, single quotes, semicolons — match the surrounding code.
- Commits describe the reader-visible change, as the log does ("Figure 2.2.8: the
  octagon becomes a two-holed doughnut in one continuous 3D motion"). Don't push or
  rewrite history unless asked.
- Chapter targets: 4,500–8,000 words, ≥5 figures (≥3 interactive), 4–8 exercises with
  solutions, a glossary entry for every new term.
