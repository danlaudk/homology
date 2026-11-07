# Prompt Lineage — the prompts that built `homology`, reconstructed

> Companion to `docs/fossil-record.md` (the geological survey). Method:
> `retroprd` (git archaeology fallback — **no construction transcripts exist**,
> so nothing here is quoted; everything is reconstructed) with an added
> analysis layer: every prompt is decomposed into the *functional concerns*
> it bundled, because the improvement goal is to write the next book from
> **concern-separated prompts**.
>
> **Purpose of this file:** be rewritten into the prompt suite for the
> improved book. Section 4 is the payload — the separated prompt
> architecture, weighted toward the later phases (figure craft, geometry
> engines, physics, prose polish) where the current book's quality lives and
> where its prompts conflated the most.

---

## 0. How to read this file

- Every reconstructed prompt is graded: **[H]** strong echo (commit body
  literally restates an instruction, e.g. "checked by tests", "following
  their code, MIT licence"), **[M]** pattern-level reconstruction, **[L]**
  mostly inferred.
- `WU-xx` refers to work-unit numbers in `fossil-record.md` §5.
- `Concerns:` tags use the taxonomy in §1. A prompt that tags 8+ concerns is
  a conflation; the archaeological record shows what that cost.

---

## 1. The Concern Taxonomy (the separation lens)

Distilled from what the history actually conflated. Three families,
sixteen concerns. The names matter — they become prompt-suite roles in §4.

**Family A — CONTENT (what the reader learns)**
- **C1 Curriculum**: which ideas exist, in what order (the concept ledger).
- **C2 Pedagogy**: how each idea is motivated; concrete→abstract ladder.
- **C3 Exposition**: the prose itself — voice, pacing, word budget.
- **C4 Structure/labels**: TOC, part/chapter numbering, section titles.
- **C5 Scholarship**: history, portraits, quotes, citations — and their
  verification against primary sources.
- **C6 Glossary/notation**: term entries, see-also, symbol conventions.

**Family B — FIGURE (what the reader sees and touches)**
- **F1 Figure selection**: *which* ideas deserve a figure at all.
- **F2 Medium**: static SVG / interactive 2D / live 3D / film / scrub-bar.
- **F3 Interaction**: drag, throw, scrub, step — and what it teaches.
- **F4 Readability**: labels, phone sizing, crossing legibility, colour.
- **F5 Visual identity**: the book's look — night sky, gold/teal/violet,
  glass surfaces. Distinct from readability: identity is taste, readability
  is function.

**Family C — ENGINEERING (what makes it run)**
- **E1 Math engine**: pure, testable computation (homology, Smith normal
  form, Khovanov). No DOM, no Svelte.
- **E2 Geometry/physics engine**: shape generation & simulation (repulsive
  curves, XPBD sheets). Also pure and testable.
- **E3 Framework implementation**: Svelte/SvelteKit components, runes,
  bundling.
- **E4 Performance**: render loop, bundle size, idle frames, pixel ratio.
- **E5 Build/deploy**: KaTeX-at-build, CI, Pages.
- **E6 Verification**: the test suite itself — structural content tests,
  math tests, continuity tests.

The original process's gravest systematic error, visible everywhere in the
record: **chapter-writing prompts bundled ~12 of these 16 concerns into one
instruction**, and craft-phase prompts bundled the wrong ones together
(physics with Svelte; readability with identity; figure selection with
medium with interaction).

---

## 2. The Stability Law (empirical, from this repo)

Correlation observed across the 198-commit history:

- **Isolated concerns fossilize into stable beds.** `src/lib/math/`
  (E1-only, born 10-03) was *never touched again*. The colour semantics
  (F5, codified once in AUTHORING §6) needed only enforcement passes, never
  redesign. Conjecture infrastructure (E3+C5, built once on 10-17) held.
- **Bundled concerns churn.** Every chapter `+page.svelte` — written by one
  mega-prompt touching C1–C6, F1–F5, E3 — was subsequently edited **12–17
  times each** (equivalence 17×, gluing 16×, characteristic-classes 16×…).
  No chapter file was ever "done" on first write; all 32 needed the audit
  era, the phone era, the prose-pass era, and the figure-craft era.
- **Late spontaneous separations mark where the process was heading.** The
  knot saga (Eras V) naturally pulled E2 out of the render path (offline
  settlement → stored shapes → `ColourKnot` draws stored views), pulled
  physics out of the component (`e907007`: "not a hand-tuned spring …
  checked by tests"), and pulled readability out of identity ("choose views
  by legibility" as a *measured* criterion, with a test that stored views
  are minimal). The improved book should **start** where the old one
  **arrived**.

Stated as law: *the half-life of a prompt's output is inversely
proportional to the number of concerns it bundled.*

---

## 3. The reconstructed prompts, era by era

Format per prompt: reconstruction → evidence & confidence → concerns
bundled → what it cost → the separated rewrite (§4 templates referenced as
`T-xx`).

### Era I — Cambrian Explosion (10-03)

**P-01 · The Platform Prompt** `[H]` — WU-02
> *"Scaffold an interactive homology textbook: SvelteKit static site,
> KaTeX rendered at build time, three.js scenes with a shared render loop,
> a tested math engine (homology over ℤ, ℤ/2, ℚ; Smith normal form;
> persistence; Hodge), night-sky/gold design, deploy to GitHub Pages."*

Evidence: `138efd1` — 117 files, 9,478 lines, one commit; its bullet list
reads like the prompt's clause list, ending in "tests" as a deliverable.
Concerns bundled: E1+E3+E4+E5+E6+F5 — the *entire* Family C plus visual
identity, minus E2 (not yet imagined).
Cost: remarkably little — this is the repo's best prompt. But note why: the
concerns it bundled are genuinely coupled at birth (you cannot test a
scaffold before it exists), and it **excluded** all content and figure
concerns. It succeeded by scope, not by craft.
Lesson: scaffold prompts may bundle Family C; they must fence out Families
A and B. → Template **T-00**.

**P-02 · The Rulebook Prompt** `[M]` — WU-03
> *"Write the authoring guide: voice, chapter anatomy, notation, concept
> ledger (which chapter may introduce what), colour semantics, component
> library, figure rules, verification checklist. Add the TeX-aware check
> and per-chapter glossaries."*

Evidence: `b43075b` + AUTHORING.md's structure; §9 ("Files you own, and
files you must not touch") only makes sense as a **contract for parallel
agents** — it was written for machines about to be spawned, not for humans.
Per-part glossaries went extinct in this same commit (replaced by
per-chapter files) — a granularity decision made *before* the swarm ran,
and it held forever after.
Concerns: C1+C2+C4+C6+F4+F5+E6 — the rulebook *is* the concern-separation
instrument, so bundling is its job. This prompt was the process's
separation layer, and it worked: it is the second-most-stable artifact in
the repo.
Lesson: one prompt must own the *codification* of concerns for everyone
else. → **T-01**.

**P-03 · The Chapter Factory Prompts (×32)** `[M]` — WU-05…11
> *"Write chapter <n>: <topic>, following AUTHORING.md — prose, ≥5 figures
> (≥3 interactive), exercises with solutions, glossary entry per new term,
> tested helpers. You own these files, touch nothing shared."*

Evidence: every "Write chapter X" message follows the same deliverable
checklist ("prose, 12 figures, glossary, tested helpers" — the commit
message *is* the prompt's rubric); ~16 `worktree-agent-*` merge branches on
day one; AUTHORING §9 as the fence.
Concerns bundled: C1–C6, F1–F5, E3, E6 — **twelve concerns per agent,
thirty-two agents at once**.
Cost: the single most expensive decision in the history. Each agent chose
figure subject, medium, interaction, readability *and* identity while also
writing prose and tests — so every chapter shipped with figures that would
each be reworked in Eras II and IV–V (see churn counts above). The
parallelism bought speed at exactly the price §2 predicts.
Lesson → **T-10/T-11/T-12**: never again one prompt per chapter; one
*pipeline* per chapter with the figure decisions extracted upstream.

**P-04 · The Salvage Prompt(s)** `[H]` — WU-13
> *"Commit everything now, we're about to hit the usage limit."*
> (×18, verbatim in commit titles: "WIP: salvage work in progress (usage
> limit reached)".)

Not a design prompt — an *operational* one, but it taught the process its
most valuable habit: checkpoint commits as resumable state (21 "Checkpoint:"
commits follow). No concern content; pure process.
Lesson → **T-20**: the improved pipeline needs durability prompts as
first-class citizens (checkpoint discipline, resume contracts), because
agent sessions die.

### Era II — Stabilization (10-06 → 10-07)

**P-05 · The Freeze Report** `[H]` — WU-15
> *"The browser freezes within seconds — find out why and fix it."*

Evidence: `540e5f0` body: "a `wake()` from inside a frame no longer
schedules a second loop (renders doubled every frame…)". A perfect bug
report: one symptom, one root cause found.
Concerns the *fix* bundled: E4 (the actual bug) + F5 + E3 + reading layout
+ icons + every UI control — a wholesale redesign rode along on a
performance fix. Either one prompt bundled them, or several prompts landed
in one commit; either way the record shows conflation.
Cost: an entire era of UI re-audits follows; the redesigned controls get
re-tweaked in every later era.
Lesson → **T-30**: bug prompts must be quarantined — fix E4, *then* run the
F5/E3 prompts separately against the fixed base.

**P-06 · The Honesty Pass** `[H]` — WU-16, 17
> *"Number every figure chapter.k with a test; make reading times honest
> (from actual length); make the math accessible and phone-width; keep
> punctuation on the same line as inline math."*

Evidence: `408af75`, `f91ed9a`, `3fd44ec` — instruction-echo phrasing
("honest reading times" is a *policy* sentence, not a code description).
Concerns: C4 + F4 + E5 + E6. Reasonably coupled (all are "global
consistency" work), and notably it *separated* policy (numbering) from
enforcement (test) — good discipline. Cost: low.
Lesson → **T-31**: global-consistency prompts should always pair the rule
with its enforcement test in the same unit.

**P-07 · The Scholarship Prompt** `[H]` — WU-19
> *"Add a shared bibliography with inline author–year citations and a
> per-chapter reference list. Verify every DOI against Crossref."*

Evidence: `44e85ee`: "Each DOI in the core bibliography was checked against
Crossref" — verification instructions survive verbatim in commit bodies.
The dup-key incident (`c8052f1`, "warns instead of breaking every page; a
test still fails on it") shows the honest-failure convention.
Concerns: C5 + E6. Well separated already; this is a model prompt.
Lesson → **T-32**.

**P-08 · The Audit Prompts** `[H]` — WU-22, 23
> *"Audit chapter by chapter across four axes — maths, history/citations,
> prose, figures — verify against primary sources, fix what's wrong."*

Evidence: checkpoint titles name the axes verbatim ("chapter audits in
progress (maths, prose, citations, figures)"); `18de0f7` (flat-Earth
correction), `4d4b341` (Aristotle on root-2), `2d3f16e` (Tubbenhauer's
tetrahedron), `0021c05` ("teach the calculus it uses… let d and the
pullback arrive as answers to questions").
Concerns: C2+C3+C5+F1/F4 — the axes are *almost* concern-separated, which
is why this era worked. But maths-audit and figure-critique still shared
commits, so a pedagogy correction and a figure redesign landed
entangled.
Lesson → **T-33**: keep the per-axis audit, but one branch per axis.

### Era III — Dormancy (10-08 → 10-15)

No prompts recoverable — nothing happened. The improved book should treat
this as the *review gap*: the resumes on 10-16 opened with quality passes,
suggesting the human spent the gap reading the book and returned with a
list. **[L]** — but the shape of Era IV (global, chapter-by-chapter,
taste-driven) is exactly what a reading notebook produces.

### Era IV — Renaissance (10-16) — first craft era

**P-09 · The Great Prose Pass** `[H]` — WU-26
> *"Do a full prose pass over every chapter in all five parts; end the
> book back at the clay ring."*

Evidence: seven "Prose pass on X–Y" commits in one day, the last
(`5f70aa5`→`2f733b0`) closing the narrative loop the Prelude opened.
The ring instruction is a *whole-book* structural directive — the first
prompt to treat the book as one object rather than 32 chapters.
Concerns: C2+C3 (+C1 at the seams). Correctly separated from figures —
prose passes touched prose. Model behavior.
Lesson → **T-13**.

**P-10 · The Portraits Prompts (×8, iterative steering)** `[H]` — WU-28
> *"Put gold-line portraits in the history boxes"* → *"the faces have dark
> patches, relight them"* → *"blend from a black ground, half size"* →
> *"no likeness of Lhuilier is known — his box has no portrait"* → *"found
> Mayer's photograph"*

Evidence: `2d6b893`→`e601dcd`, eight commits, each message a taste verdict.
The scholarship rule ("no likeness… is known") is C5 discipline inside an
F5 task — the right fusion (historical honesty is *part of* image policy).
Cost: eight iterations because **there was no image-quality rubric** —
every generation was judged only after rendering. The improved book needs
the rubric up front (lighting, ground, crop, scale, fallback-when-no-
likeness) so it converges in 2–3 rounds.
Lesson → **T-40**.

**P-11 · The Torus Physics Prompts (×3 — the era's clearest conflation→separation arc)** `[H]` — WU-29
> 1. *"Throw with momentum; grab the surface and stretch it like rubber,
>    it springs back; loops that roll, sweep and ripple."*
> 2. *"The stretch is hand-tuned and looks fake — make it a real simulated
>    elastic sheet; released, it settles in ~0.3 s with at most a small dip;
>    check by tests."*
> 3. *"Canvas fills the whole hero; thicker rubber (two-layer wall, solid
>    core, stiffening) that doesn't fold when yanked."*

Evidence: `546dacc`, `e907007` (its message *is* prompt 2, nearly
verbatim), `e77c296`.
Anatomy: prompt 1 bundled **F3 (interaction: throw/grab) + E2 (elastic
response) + F5 (identity: 'like rubber')** and produced a hand-tuned
spring. Prompt 2 *separated E2 out* — real XPBD simulation, numeric
acceptance criteria (0.3 s settle, bounded overshoot) in the prompt itself
— and it converged with tests. Prompt 3 was F5-only (material character).
This trio is the whole thesis of this file in miniature: **the second
prompt's separation is what the first prompt should have been.**
Lesson → **T-50/T-51**: interaction spec and physics spec are different
prompts; physics prompts must carry numeric acceptance criteria; identity
(what it should *feel* like) is a third prompt feeding the physics target.

**P-12 · The Folding-Square Prompt** `[H]` — WU-30
> *"Figure 1.2.7: the square folds into a torus in 3D; threads join the
> pairs to be glued and shrink as the sides stitch; live counts show the
> classes (corners 4→2→1)."*

Evidence: `d61437b`, refined `133c3d1` ("threads are dotted circular arcs,
each in the plane where its gap closes… checked continuous by tests").
Concerns: F1–F4 + E4 + E6 in one figure prompt — and note the refinement
added *mathematical* acceptance ("checked continuous by tests"): the
geometric truth of an animation became a testable property. Good. But the
device itself (threads) was chosen inside the same prompt that implemented
it — so when taste later ruled threads noisy (Era V, `03533e7`: extinct),
the whole implementation died with the choice. **Device choice and device
implementation must be separate prompts** — that's what lets a later taste
verdict swap one without killing the other.

### Era V — Knot Radiation (10-17 → 10-18) — the deepest craft era

**P-13 · The Frontier Prompt** `[H]` — WU-32
> *"Add conjecture boxes and an Open Problems page: one record per
> conjecture (statement, status, how settled, what's known, a way in,
> sources); a <Conjecture> component; statuses checked as of October 2026;
> shown exactly once, in its chapter, with real sources."*

Evidence: `14b0d15`, `5f70aa5` bodies — the field list is the prompt's
schema; even "statuses checked as of October 2026" (a *currency*
instruction) survives, along with named recent results (Navier–Stokes
Sept 2026, S⁶ Aug 2026).
Concerns: C5 + C1 + E3 + E6. Coupled *well*: the schema is the contract,
the test enforces it, the content is verifiable. A model prompt; the
improved book's data-driven features should all look like this.
Lesson → **T-32**.

**P-14 · The Knot Engine Prompt** `[H]` — WU-33
> *"Build the knot engine: knots as curves in space → diagrams (PD codes,
> crossing signs) → Kauffman bracket, Jones, Alexander, Fox colourings,
> determinant, linking numbers, Seifert circles; torus knots; invariant
> table with PD codes from KnotInfo."*

Evidence: `14b0d15` body names the pipeline stage by stage.
Concerns: E1 + E6 only — a pure math-engine prompt, and (like `src/lib/math/`)
it held. Confirms the law: engine prompts that refuse to touch rendering
are stable.
Lesson → **T-02**.

**P-15 · The Insertion Prompt** `[M]` — WU-34
> *"Add Knots and Links as chapter 3.7 — persistence becomes 3.8; weave
> knots into 2.1 and 2.3 (the trefoil's non-commuting lassos)."*

Evidence: `5843808`, `69c840d`, `bb838a4`.
Concerns: C1+C4 (curriculum + renumbering) — a structural edit executed
cleanly against the TOC-as-single-source-of-truth. Cost: renumbering
ripples (figure ids `chapter.k` all shift) were absorbed by the E6 tests,
not by the prompt. **Structure prompts are safe exactly when enforcement
tests already exist.** Lesson → **T-14**.

**P-16 · The Repulsive-Curves Prompt — the highest-signal reconstruction in the repo** `[H]` — WU-38
> *"Generate knot shapes with the repulsive-curves method — Yu, Schumacher
> & Crane's tangent-point energy (α=3, β=6), fractional Sobolev descent;
> here's their code (github.com/ythea/repulsive-curves, MIT). Port:
> edge-based energy + exact gradient, Sobolev–Slobodeckij Gram matrix,
> barycentre/edge-length constraints as a saddle-point system, Armijo line
> search, Newton back-projection."*

Evidence: `f864997` body names paper, authors, parameters, repo, licence,
and the exact algorithmic inventory — this is a *pasted reference* prompt
and it produced the deepest, fastest-converging technical arc in the
history.
Anatomy: pure **E2**, with its own acceptance (energy values). Everything
after it is the concern pulling its neighbors into line: convergence
diagnostics (`29e60b7`), env knobs (`27d102b`), full-convergence reruns
(`ff0f66d`) — E2 iterating alone. Then the **LU-solve crater** (`bc3cdbf`,
`37ba1aa`): a silent numerical bug invalidated every settlement; the
re-settlement commit is the recovery. With E2 isolated and tested this was
caught and healed in two commits — the same class of bug in a bundled
prompt would have been invisible.
Lesson → **T-50**: geometry/physics generation belongs offline, in its own
module, with energy/acceptance numbers in the prompt, rerun knobs in env
vars, and **numerical regression tests comparing stored energies** (the
one guard the original lacked — the LU bug shipped once).

**P-17 · The Legibility Prompts (the craft steering loop)** `[H]` — WU-35, 38
> *"Choose each knot's view by legibility — crossing angles, clearance, no
> foreshortened strands"* → *"settle them flat in a slab, like a knot
> table"* → *"the gallery turns the knot itself; a flat knot rocks instead
> of turning edge-on"* → *"stop searching for views on the main thread —
> store the best view and test that stored views are minimal."*

Evidence: `12977c3`, `bdc0d69`, `f0fae09`, `e40b6b7`, `e9c9720`.
This is a human looking at rendered knots and dictating *readability as a
measured criterion* — F4 becoming quantitative (clearance, crossing
angles) and then *compiled offline* into stored data. The arc F4-criterion
→ offline precomputation → E6-guard is exactly the right shape; it just
took five steering rounds because no legibility rubric existed on day one.
Lesson → **T-52**: a figure-readability rubric (min crossing angle,
clearance px, label sizes relative to figure width — `75a28e6` already
found the law: size by the figure's width, not the window's) belongs in
the *initial* figure prompts.

**P-18 · The Taste Verdicts (extinction drivers)** `[H]` — WU-40, 41
> *"Tubes: the far wall showed its inside — hand-drawn ones must face
> inwards."* · *"Square-to-torus: drop the threads; just coloured points
> that meet."* · *"The octagon becomes a two-holed doughnut in one
> continuous motion."*

Evidence: `272b30a`, `03533e7`, `9033d9d`.
These are the purest F4/F5 prompts in the repo — single verdicts, single
commits, each killing a device or fixing a visual falsehood. Cheap,
decisive, correct. The improved book wants *more* of these, earlier: the
devices they killed (threads, cones for orientation, dark outlines) all
came from Era-I/IV prompts that chose the device and implemented it in the
same breath. A cheap verdict stage before implementation would have saved
each device's whole build.

---

## 4. The improved prompt architecture (payload)

### 4.1 The pipeline (dependency order)

Concerns have a natural DAG; prompts should follow it and never span
backward:

```
T-00 PLATFORM      E5,E3,E4,E6  scaffold + gates (P-01's scope, fenced)
T-01 RULEBOOK      all          codify every concern's rubric (P-02)
T-02 ENGINES       E1,E2        pure modules + tests (P-14, P-16)
T-10 CURRICULUM    C1,C4        per-part concept ledger + TOC
T-11 FIGURE PLAN   F1,F2        per chapter: which ideas get figures, what medium
T-12 INTERACTION   F3           per figure: what the reader does, what it teaches
T-13 EXPOSITION    C2,C3        prose, per chapter, against the figure plan
T-14 STRUCTURE     C4           numbering/insertion edits (safe post-T-01 tests)
T-30 QUARANTINE    E4           perf/bug fixes, one concern per branch (P-05)
T-31 CONSISTENCY   C4,F4,E6     rule + enforcement test pairs (P-06)
T-32 DATA APPARATUS C5,E6      citations/conjectures as schemas + tests (P-07,P-13)
T-33 AXIS AUDITS   C2|C3|C5|F4  one axis per pass, per chapter (P-08)
T-40 IMAGE POLICY  C5,F5        portrait/figure-image rubric (P-10)
T-50 SIMULATION    E2           physics/geometry with numeric acceptance (P-11.2, P-16)
T-51 INTERACTION PHYSICS  F3+E2 contract: feel targets → sim parameters (P-11.1→.2)
T-52 READABILITY   F4           measured rubric, offline-precomputed (P-17, 75a28e6)
T-60 VERDICTS      F4,F5        cheap taste kills before build (P-18)
T-20 DURABILITY    process      checkpoints, resume contracts (P-04)
```

### 4.2 What each later-phase template must contain (the craft deep-dive)

The later eras are where the improved book wins or loses. Extracted
templates:

**T-50 Simulation/geometry prompt** (from P-16 + the LU crater):
name the method and reference; the exact algorithmic inventory; parameters
(α, β, tolerances); **numeric acceptance criteria** (energy to 4 digits,
settle time, overshoot bound); env-var knobs for reruns; **regression
tests pinning stored outputs** (energies, settle curves) so a silent
solver bug cannot ship; regeneration script as the only way to touch
generated JSON. Rule: *no Svelte import may appear in this module.*

**T-51 Interaction-physics contract** (from the torus trio):
two documents. (1) FEEL spec — F3/F5 only: "grab stretches like rubber;
release springs back in ≲0.3 s with a small dip"; (2) SIM spec — E2:
method (XPBD), mesh, constraints, and the acceptance numbers translated
from the feel spec, testable headlessly. The component consumes the
engine; the engine never learns the component exists.

**T-52 Figure readability rubric** (from P-17 + `75a28e6`):
per-figure acceptance, machine-checkable where possible: label font sized
to **figure width, never window width**; min crossing angle and clearance
for knot/diagram figures; over/under unambiguous at every crossing;
no label overlap at 375px; dark-sky palette only; orientation shown by
light drift, not cones; tubes hand-wound with faces outward. Compile the
rubric offline (stored views) and test the compiled artifact.

**T-11/T-12 Figure selection & interaction** (from the churn data):
figure prompts split into three passes per chapter — *what* (which ideas
earn a figure: one per idea the ledger marks must-see), *how* (medium:
static ≤ interactive ≤ live-sim, cheapest that teaches), *act* (the
interaction script and what it reveals). A **T-60 verdict gate** runs on
the three-line proposals before any implementation budget is spent —
this is the mechanism that would have killed threads, cones and dark
outlines for free.

**T-13 Exposition** (from P-09's success): prose passes run *against a
frozen figure plan* so the text can trust figures existing; whole-book
arcs (open at the clay ring, return to it) are decided at T-10 and merely
executed here.

**T-33 Axis audits** (from P-08): four separate, resumable passes —
maths, history, prose, figures — one branch each; primary-source
verification (Crossref DOI checks, no-unverified-quote rule,
no-likeness-known rule) lives in the history axis and the image policy.

### 4.3 The three rules that would have prevented most churn

1. **No prompt touches more than one family** (A/B/C) — and within a
   family, no prompt touches more than two adjacent concerns. (P-03 broke
   this twelve times at once; the audit era paid for it for two days.)
2. **Every artifact-producing prompt carries its acceptance test** in the
   same unit — numbering (P-06), citations (P-07), conjectures (P-13),
   settle times (P-11.2), stored views (P-17) all prove this pattern;
   every artifact that lacked one needed a later era.
3. **Taste verdicts are cheap; make them upstream.** A one-line verdict
   after rendering cost one commit (fine); the same verdict before
   implementation costs one line. Device choice and device build are
   always separate prompts, so verdicts can swap devices without
   rewrites.

---

## 5. Concordance

| Prompts | Eras | Fossil-record WUs |
|---|---|---|
| P-01…P-04 | I | 01–13 |
| P-05…P-08 | II | 14–23 |
| — | III | 24 |
| P-09…P-12 | IV | 25–30 |
| P-13…P-18 | V | 31–41 |

*Reconstructed 2026-10-29 from the 198-commit local history (no
construction transcripts exist; all prompts are inference from commit
bodies, file trajectories and AUTHORING.md). Grades: [H] echo-verbatim,
[M] pattern-level, [L] speculative. The `worktree-lin-alg-smith-torsion`
branch is excluded from this lineage by direction.*
