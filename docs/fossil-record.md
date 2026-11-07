# Fossil Record: Geological Survey — `homology`

> Complete evolutionary narrative of this repository, produced by the
> `fossil-record` archaeology method (read-only local git analysis).
> **This file is written to be consumed by the `retroprd` skill**: §5 groups
> every commit into chronological, PRD-sized work units, ready to be turned
> into PRDs. Evidence markers: `git` = commit evidence, `code` = code reading,
> `inferred` = reconstruction from patterns.

## 1. Survey summary

```
Repository:   homology — "Homology & Cohomology: an illustrated journey"
              (interactive SvelteKit static textbook, 32 chapters)
History:      2026-10-03 → 2026-10-18 (15 days, 198 commits, 165 non-merge)
Volume:       ~182,900 insertions / ~11,800 deletions; 776 tracked files,
              387 Svelte components, ~250k words, ~280 figures
Authors:      196 commits Claude (AI, "Claude Opus 5.5" trailer on 153)
              + 2 human commits (Neo Mohsenvand: initial commit, banner gif)

ERAS: 5
├── I. Cambrian Explosion      2026-10-03   (49 commits) scaffold + all 32 chapters drafted in parallel
├── II. Stabilization          2026-10-06 → 10-07 (48 commits) perf fires, audits, citations, numbering
├── III. Dormancy              2026-10-08 → 10-15 (0 commits) nine-day silence
├── IV. Renaissance            2026-10-16   (26 commits) global prose pass, portraits, torus physics
└── V. Knot Radiation          2026-10-17 → 10-18 (42 commits) conjectures + full knot engine & chapter

FAULT LINES: 5 major (see §3)
IMPACT CRATERS: 4 (usage-limit salvage, render-loop freeze, double-key
  bibliography breakage, LU-solve mis-settlement)
FOSSIL BEDS: src/lib/math (born 10-03, never touched again — stable by design)
EXTINCTION EVENTS: 6 (see §4) — notably per-part glossaries → per-chapter,
  threads/stitches gluing figures → 3D folding, banner.webp → banner.gif
UNMERGED LINEAGE: branch claude/eloquent-darwin-y83dw4 (1 commit, braid/plat
  sampling fix) + local worktree branch `worktree-lin-alg-smith-torsion`
TRAJECTORY: content-complete book entering deep figure-craft phase; knot
  geometry engine is the active radiation front
```

## 2. Era-by-era narrative (the WHY)

### Era I — Cambrian Explosion (2026-10-03, 49 non-merge commits)

Genesis is a two-author act. The human (Neo Mohsenvand) makes the empty
initial commit `61ea224`; the machine then writes a whole organism in one
commit: `138efd1` "Scaffold interactive homology textbook" lands 117 files /
9,478 lines in a single stride — SvelteKit, the KaTeX build-time
preprocessor, three.js scene infrastructure, and the entire tested math
engine (`src/lib/math`: simplicial complexes, homology over ℤ/ℤ₂/ℚ, Smith
normal form). The architecture is front-loaded: every architectural decision
that still stands (prerendered static site, build-time math, tested engine,
generated knot geometry) predates the first chapter.

Then the swarm: the merge record shows ~16 `worktree-agent-*` branches merged
on Oct 3 (plus 6 more on Oct 6). Chapters were drafted **in parallel by
per-worktree agents**, each producing "Write chapter X" commits of startling
scale (e.g. `e5fbc5b` writes §4.7 and §4.8 together; `b55d5fb` writes §2.5
with 12 figures). All 32 chapters exist in draft by the end of day one,
including Part V (`fd4da4b`, flagged WIP).

The day ends in crisis: **the usage-limit salvage event**. Twelve commits
`e5027e8`…`812034e`, all literally titled "WIP: salvage work in progress
(usage limit reached)", plus six more "salvage final … before the agent
stopped" on Oct 6 (`68dc1c8` et al.). These are emergency checkpoints
committed while the writing agent was dying of quota — preserving partial
edits across dozens of figure files mid-flight. One of them (`41f8551`, Oct 3)
quietly contains a `knots.ts` (116 lines + test) inside
`src/lib/figures/cohomology/poincare-duality/` — the fossil of the idea that,
eleven days later, becomes the book's largest subsystem. Knots began life as
a *figure helper for the Poincaré duality chapter*. (git)

Also fixed in this era: per-part glossary files (`content/glossary/topology.ts`
etc.) went extinct on day one (`b43075b`), replaced by per-chapter glossary
files — the granularity tests still enforce today.

### Era II — Stabilization (2026-10-06 → 10-07, 48 commits)

The draft book does not yet *run well*. Three fires, in order of severity:

1. **The render-loop pile-up** (`540e5f0`, Oct 6): "a `wake()` from inside a
   frame no longer schedules a second loop (renders doubled every frame,
   freezing the page within seconds)". This is the repo's deepest impact
   crater — the commit also rebuilds glass surfaces (winding order, depth
   pre-pass), the reading layout (sidebar from 1024px, one plate width),
   icons (Hugeicons), and every UI control. Architecture-level scar tissue
   from a perf incident.
2. **Bundle size** (`fead716`): "Render KaTeX as HTML only to halve chapter
   bundle size" — a build-output fault line; `macros.js` adjusted to match.
3. **Test fragility** (`4900e46`, back on Oct 3): §1.5 tests needed "smaller
   random sample and explicit timeouts".

Then the book acquires its scholarly skeleton: figure numbering `chapter.k`
enforced globally (`408af75`, with honest reading times), accessible math
labels (`f91ed9a`), phone-width display math (`f032706`, `e52ec57`), the
shared bibliography + inline author–year citations + per-chapter reference
lists (`44e85ee`, `cc3bd92`), and the duplicate-bib-key incident (`c8052f1`:
"a key defined twice warns instead of breaking every page; a test still
fails on it" — honest commit messages as instrumentation).

The era closes with the **chapter audits arc**: six "Checkpoint: chapter
audits in progress/wrapping up" commits (`1724adb` → `b17d93a`) interleaved
with per-part prose passes. This introduces the repo's signature commit
pattern — *checkpoint commits as session heartbeats* — 21 "Checkpoint:"
commits and 19 "WIP" commits in total, an agent leaving breadcrumbs because
sessions die (usage limits) and must resume. The audits verify quotes and
history against primary sources (e.g. `18de0f7` corrects the flat-Earth
myth; `4d4b341` cites Aristotle on the root-2 proof).

### Era III — Dormancy (2026-10-08 → 10-15, zero commits)

Nine days of silence after `3b33a7b` (Oct 7, 22:12 UTC). Nothing died; the
last pre-gap commits are "Checkpoint: figure fixes in progress (homology
groups)" — work frozen mid-arc. The resume point (`75a28e6`, Oct 16) picks
up figure checks exactly where they stopped. Cause of the gap is outside the
fossil record (quota, calendar, or attention — not determinable from git).

### Era IV — Renaissance (2026-10-16, 26 commits)

The session that resumes is different in character: no new chapters, no new
infrastructure — a **quality pass over the entire book**. A complete prose
pass chapter-by-chapter across all five parts (`b0e4cdb` 1.2–1.4, `be4ca1a`
2.2–2.4, `33d0aed` 2.5–2.6 with the Descartes defect explanation, `59aafb6`
3.5–3.7, `c08aeae` 4.4–4.6, `153de73` 4.7–4.8, `536a608` 5.1–5.3 ending
"back at the clay ring" — closing the narrative loop the Prelude opened).

Two craft sub-arcs:

- **The portraits saga** (`2d6b893` → `e601dcd`, 8 commits in one day):
  gold-line portraits for history boxes — layout variants tried (banner,
  panel, hero), relighting every face ("no dark patches"), blending from a
  black ground, deduplicating repeated stories (1935 Moscow conference,
  Leray's camp), and research-grade honesty: "Show Vietoris alone until
  Mayer's portrait exists; Lhuilier's box has no portrait (no likeness of
  him is known)" — then Walther Mayer's portrait arrives "from a photograph
  the owner supplied". Primary-source discipline applied to images.
- **The landing torus** (`546dacc` → `e77c296`, 3 iterations in one day):
  momentum throw + rubber stretch → replaced by a *simulated XPBD elastic
  sheet* with test-verified settle time (~0.3 s) → full-hero canvas with a
  thicker two-layer wall "that no longer folds when yanked". Hand-tuned
  springs went extinct in favour of real physics, checked by tests.

Plus the first continuous-math 3D folding figure: `d61437b`/`133c3d1`
(Figure 1.2.7, square→torus with gluing threads as dotted circular arcs,
"checked continuous by tests").

### Era V — Knot Radiation (2026-10-17 → 10-18, 42 commits)

Adaptive radiation after the polish era: the knot idea that survived as a
Poincaré-duality helper explodes into a full organ system.

- **Infrastructure first** (`14b0d15`): conjecture boxes + Open Problems
  page — the book grows a research-frontier layer. Then engine commits:
  Khovanov homology from the cube of resolutions (`0953da0`), knot/link
  table with settled shapes (`5b0c58f`), precomputed invariant table with
  PD codes from KnotInfo (`c74be7b`), tested framing/meridian/longitude
  (`70f6bdc`).
- **Structural fault line**: chapter insertion. `5843808` "Chapter 3.7 Knots
  and Links (in progress): TOC entry, knot gallery; **persistence becomes
  3.8**". A whole chapter is renumbered to make room — the TOC
  (`src/lib/content/toc.ts`, single source of truth) absorbing the change.
- **Knots woven back into existing chapters**: 2.1 (`69c840d`) and 2.3
  (`bb838a4`, the trefoil's non-commuting lassos) gain sections referencing
  the new engine.
- **The geometry saga** (Oct 18, the deepest single technical arc in the
  repo): repulsive-curves method with tangent-point energy and fractional
  Sobolev descent (`f864997`); torus knots kept symmetric (`9e8a373`);
  diagnostics (`29e60b7`); patient stopping rule, up to 2500 steps
  (`f9b5e43`); env knobs for energy/step-limit/output (`27d102b`); full
  convergence runs (`ff0f66d`); FLAT=1 slab mode (`bdc0d69`); save-after-
  each-knot (`f0fae09`); stored best views replacing main-thread search
  (`e40b6b7`, with a test that stored views are minimal); "knot shapes lie
  flat, as a table of knots draws them" (`e9c9720`).
- **Impact crater inside the saga**: an LU-solve bug (`bc3cdbf`, "a fix to
  the LU solve") invalidated settlements; `37ba1aa` re-settles the affected
  knots (5₂, 6₁, 6₃ get lower energies; 6₂ "opens out"). The generator was
  then trusted enough to draw `ColourKnot` straight from stored shapes.
- **Global correctness passes ride along**: glossary deduplication (25
  duplicate entries merged + test, `278572d`), see-also relaxation
  (`76362d6`), book-wide consistency sweep (`1029780`), colour semantics
  enforced in §1.5 and matrix figures (`66d770f`, `2f2fcea` — kernel gold,
  image teal, matching the book-wide colour code).
- **Closing commits** return to classic figures: tube winding fixed
  (`272b30a` — "tubes drawn by hand faced inwards"), the gluing chapter's
  threads go extinct (`03533e7`: "no threads between partners, just coloured
  points that meet" — replacing the Era-IV thread design), and the final
  commit `9033d9d` delivers the octagon→two-holed-doughnut continuous 3D
  morph (Figure 2.2.8).

**Unmerged lineage**: `55a9ecf` "Knots: keep closed braids' and plats'
samples off their crossings, whatever the sampling" sits on
`claude/eloquent-darwin-y83dw4` (also held by local worktree branch
`worktree-lin-alg-smith-torsion`) — **not an ancestor of main**. A real,
tested fix (crossings landing exactly on polyline corners) left adrift.

## 3. Fault lines (architecture-changing commits)

| # | Date | Commit | Shift |
|---|------|--------|-------|
| 1 | 10-03 | `138efd1` | Empty repo → full platform (SvelteKit + KaTeX-at-build + three.js + math engine). Every later decision inherits from this scaffold. |
| 2 | 10-03 | `b43075b` | Per-part glossaries → per-chapter glossary files; AUTHORING.md becomes binding law; TeX-aware check wrapper introduced. |
| 3 | 10-06 | `fead716` | KaTeX output mode changed to HTML-only — halves bundle, constrains macro usage forever after. |
| 4 | 10-06 | `540e5f0` | Render-loop architecture fixed (freeze); wholesale UI/layout/icon redesign in the same strike. |
| 5 | 10-17 | `5843808` | TOC renumbering: Knots inserted as 3.7, persistence pushed to 3.8 — content topology itself is malleable. |

Honourable mention: knots migrating from `figures/cohomology/poincare-duality/knots.ts` (Oct 6 salvage) to a first-class `src/lib/knots/` subsystem (Oct 17) — a directory-structure fault line without a single move commit.

## 4. Extinction events (what died, and what replaced it)

| Date | Commit | Extinct | Replaced by / reason |
|------|--------|---------|----------------------|
| 10-03 | `b43075b` | `content/glossary/{prelude,foundations,topology,cohomology,big-picture}.ts` | per-chapter glossary files (test-enforced granularity) |
| 10-06 | `540e5f0` | `figures/big-picture/categories/Stepper.svelte`, `figures/prelude/shape-of-a-question/deform.ts` | shared `ui/` components; Scene3D-native deformation |
| 10-07 | `6d8d20f`, `b3e05c1` | three `check.scratch.test.ts` files | scratch tests swept after the audit arc — disposable by design |
| 10-07 | `75bf7c1` | `docs/banner.webp` | `banner.gif` (human-uploaded `4e7ad36`) — animated beats static |
| 10-16 | `e907007` | hand-tuned spring stretch on landing torus | XPBD simulated elastic sheet, test-checked settle |
| 10-18 | `03533e7` | `figures/foundations/equivalence/stitches.ts` + test (gluing threads) | 3D folding figure 1.2.7 with coloured meeting points — threads abandoned as visual noise |

## 5. Work units for retroPRD (chronological, PRD-sized)

Each row is one coherent unit of product intent ("a PM would have written a
ticket for this"). Commits listed are the evidence trail; dates are author
dates. Confidence reflects how much is commit-evidenced vs inferred.

| # | Unit | Type | Commits (first→last) | Date | Conf. |
|---|------|------|----------------------|------|-------|
| 01 | Repo genesis (empty initial commit) | chore | `61ea224` | 10-03 | High |
| 02 | Platform scaffold: SvelteKit, KaTeX-at-build, three.js Scene3D, tested math engine | architecture | `138efd1` | 10-03 | High |
| 03 | Authoring infrastructure: AUTHORING.md, TeX-aware check, shared 2D components, per-chapter glossaries | architecture | `b43075b` | 10-03 | High |
| 04 | Site chrome: landing hero, journey map, glossary/notation/sources pages, search, cheat sheet, error page, chapter stats | feature | `ab0b05d`, `9b3fe5e`, `81a3cb3`, `e0919c0`, `8285870`, `b3a3237`(part) | 10-03 | High |
| 05 | Cup product & duality engine (ch. 4.5–4.6 support) | feature | `5e0a6da` | 10-03 | High |
| 06 | Prelude chapters 0.1–0.2 (six figures; how to read mathematics) | content | `b3a3237`, `e563cc1`, `891e956` | 10-03 | High |
| 07 | Part I Foundations: ch. 1.1–1.5 (sets, equivalence, groups, abelian groups, linear algebra) | content | `4b75f75`, `bd48e12`, `d068e27`, `b9f2837`, `badc5aa`, `e962c65`, `4900e46` | 10-03 | High |
| 08 | Part II Topology: ch. 2.1–2.6 (gluing, homotopy, simplicial, manifolds, Euler) | content | `039d9c6`, `d1f5f24`, `b55d5fb`, `b0d20ba`, `d3145aa`, `63c76fd`, `18de0f7` | 10-03 | High |
| 09 | Part III Homology: ch. 3.1–3.7 (cycles, chains, groups, computing, invariance, exact seqs, persistence) | content | `5d84392`, `7204939`, `2c8af95`, `cb09d17`, `32160ad`, `7b4728f`, `babba88` | 10-03 | High |
| 10 | Part IV Cohomology: ch. 4.1–4.8 (cochains, duality, forms, de Rham, cup product, sheaves, curvature) | content | `195b7cd`, `3bee743`, `9e41b0e`, `7719470`, `e5fbc5b` | 10-03 | High |
| 11 | Part V Big picture: categories, homological algebra, horizons (WIP) | content | `fd4da4b` | 10-03 | High |
| 12 | Parallel chapter factory: ~16 worktree-agent branches drafted the book in one day | process | merges `0ee8b02`, `fe12a0b`… `eac9f8c` | 10-03 | High |
| 13 | Usage-limit salvage event: 18 emergency checkpoint commits preserving partial work (incl. proto-`knots.ts` inside poincare-duality) | incident | `e5027e8`…`812034e`, `68dc1c8`+5 | 10-03→06 | High |
| 14 | Performance: KaTeX HTML-only output (halve bundles); lighter start-up | improvement | `fead716`, `382cae8`(part) | 10-06 | High |
| 15 | Render-loop pile-up freeze fix + reading layout, one plate width, Hugeicons, control redesign | bugfix/architecture | `540e5f0`, `2db6463`(prior mitigation) | 10-06 | High |
| 16 | Global figure numbering `chapter.k`, honest reading times, phone-fit home page | improvement | `408af75` | 10-06 | High |
| 17 | Accessibility & mobile math: a11y labels, punctuation with inline math, phone-width display math | improvement | `f91ed9a`, `3fd44ec`, `f032706`, `e52ec57` | 10-06 | High |
| 18 | Figure craft wave: homotopy rework, timelines/drag handles, idle 3D films | feature | `f61961f`, `382cae8`, `e52ec57`, `5c2dfe1` | 10-06 | High |
| 19 | Scholarly apparatus: shared bibliography, inline citations, sources page, dup-key warning | feature | `44e85ee`, `cc3bd92`, `c8052f1` | 10-06 | High |
| 20 | README/banner arc (webp → human-uploaded gif) | docs | `76a365d`, `4e7ad36`, `75bf7c1` | 10-07 | High |
| 21 | Klein bottle upright, one-sided shading, shared cell labels | bugfix | `4869ff1` | 10-07 | High |
| 22 | Chapter audits arc: maths/history corrections, per-part prose & figure passes (primary-source verified) | quality | `1724adb`…`b17d93a` (6 checkpoints) + `2d3f16e`, `0021c05`, `4d4b341`, `950ce05`, `ad14ffa`, `696c9ea`, `88176ec`, `3b33a7b`, `8d0dc80` | 10-06→07 | High |
| 23 | Cohomology motivation rework (4.1/4.2): impossible staircase, contravariance intuition | content | `2d3f16e` | 10-06 | High |
| 24 | — DORMANCY: no commits — | — | (gap) | 10-08→15 | High |
| 25 | Phone-sized graph figure labels/touch targets by figure width | improvement | `75a28e6` | 10-16 | High |
| 26 | Global prose pass II: all five parts; book ends "back at the clay ring" | quality | `e36ec29`…`536a608` incl. `b0e4cdb`, `be4ca1a`, `33d0aed`, `59aafb6`, `c08aeae`, `153de73`, `2f733b0` | 10-16 | High |
| 27 | 3D interaction fixes: grab-cursor honesty, barcode scrub cursor | improvement | `536a608`(cursor part), `1348683` | 10-16 | Medium |
| 28 | Portraits saga: gold-line history portraits for all parts; Mayer found, Lhuilier none known; dedup stories | feature | `2d6b893`, `0f3fc76`, `331291a`, `7529365`, `888727d`, `c7f7bee`, `3ca9222`, `e601dcd` | 10-16 | High |
| 29 | Landing torus physics: momentum throw, XPBD elastic sheet, full-hero canvas | feature | `546dacc`, `e907007`, `e77c296` | 10-16 | High |
| 30 | Figure 1.2.7: square folds into torus in 3D (threads → arcs → continuity-tested) | feature | `d61437b`, `133c3d1` | 10-16→17 | High |
| 31 | Course map rebuild (steady panel, dependency light, progress); Greek alphabet page in 0.2 | feature | `f047079`, `1ca0501` | 10-17 | High |
| 32 | Conjecture boxes + Open Problems page; conjecture boxes across the book; Goldbach's comet | feature | `14b0d15`, `a32218a`(part), `5f70aa5`(part) | 10-17 | High |
| 33 | Knot engine: Khovanov cube, knot/link table, invariants table (PD codes from KnotInfo), framing | feature | `0953da0`, `5b0c58f`, `c74be7b`, `70f6bdc`, `a5f70aa5` | 10-17 | High |
| 34 | Knots chapter 3.7 + TOC renumbering (persistence → 3.8); knot sections in 2.1 & 2.3 | content/architecture | `5843808`, `69c840d`, `bb838a4`, `a32218a` | 10-17 | High |
| 35 | Knot diagram craft: Reidemeister moves, bracket states, Khovanov cube, clean crossings, legibility views | feature | `30032f9`, `9946356`, `2c1d0c2`, `12977c3`, `afe5a08` | 10-17→18 | High |
| 36 | Glossary integrity: 25 duplicates merged + test; see-also relaxation; book-wide consistency sweep | quality | `278572d`, `76362d6`, `1029780` | 10-17 | High |
| 37 | §1.5 & matrix figure colour semantics (kernel gold, image teal); TeX parenthesis fixes | improvement | `66d770f`, `bf4dac9`, `2f2fcea`, `34f16f7` | 10-17 | High |
| 38 | Repulsive-curves knot geometry saga: tangent-point energy, Sobolev descent, convergence, FLAT mode, stored best views | feature | `f864997`, `9e8a373`, `29e60b7`, `f9b5e43`, `27d102b`, `ff0f66d`, `bdc0d69`, `f0fae09`, `e40b6b7`, `e9c9720` | 10-18 | High |
| 39 | LU-solve bug + full re-settlement; live relax demo (Fig 3.7.2) | bugfix | `bc3cdbf`, `37ba1aa` | 10-18 | High |
| 40 | Hand-drawn tubes faced inwards (live knot, homotopy loops, home loops) | bugfix | `272b30a` | 10-18 | High |
| 41 | Gluing chapter finale: threads extinct → meeting points; exact double curves; octagon→two-holed doughnut morph (Fig 2.2.8) | feature | `03533e7`, `cc78af3`, `9033d9d` | 10-18 | High |
| — | **Unmerged**: braid/plat crossing-sample fix on `claude/eloquent-darwin-y83dw4` / `worktree-lin-alg-smith-torsion` | bugfix (adrift) | `55a9ecf` | 10-17 | High |

## 6. Author topology & working style

- **Effective single-agent codebase with human curator.** 196/198 commits
  by Claude; the human's two commits are the empty genesis and a binary
  asset upload. Direction arrived out-of-band (prompts), not in git.
- **153 commits carry `Claude-Session:` trailers** and 153 a
  `Co-Authored-By: Claude Opus 5.5` trailer — sessions are traceable.
- **Checkpoint commits are the heartbeat**: "WIP"/"Checkpoint" commits
  (19 + 21) mark resumable state, because sessions end abruptly (usage
  limits — Era I proves it). This is an agent that learned to leave fossils
  deliberately.
- **Commit messages are unusually reader-facing** ("the trefoil's lassos do
  not commute", "no likeness of him is known") — they document reader-visible
  change, per the repo's own convention, and are high-signal for PRD
  reconstruction.
- Bus factor: 1 (agent) + 1 (human director). No knowledge voids — the
  knowledge holder is effectively the documentation itself.

## 7. Fossil beds & trajectory

- **`src/lib/math/` is the oldest untouched bed**: born `138efd1` (10-03),
  never modified since (git). Not neglect — the engine was right the first
  time; tests guard it. Contrast with `src/lib/knots/` (born 10-17, 20+
  files, churn daily): the active radiation front.
- **Trajectory at last commit**: content-complete (32 chapters), polish
  waves done book-wide; energy concentrated on (a) knot geometry
  generation, (b) gluing/folding figures, (c) landing-page physics. The
  Oct-18 pattern (extinct visual devices replaced by simpler exact ones —
  threads → points) signals a maturing taste: fewer, truer figures.
- **Likely next fault lines**: merging or abandoning `55a9ecf`; more
  generated-geometry chapters (braids?); a possible "final pass" era before
  a v1.0 announcement. (inferred)

*Survey generated 2026-10-29 from the full local git history
(198 commits, no network access). Method: fossil-record skill —
pressure analysis, decision reconstruction, extinction mapping,
sediment dating, fault-line detection, author topology.*
