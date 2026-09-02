# Report: the Atlas re-anchored on the work

Direction B, built on branch `atlas-work-first`, five commits on top of the
merged tree. Diagnosis and directions are in this folder as `diagnosis.md`
and `directions.md`; screenshots in `shots/`.

## What changed, and where

**`build/atlas.py`.** The standalone first commit (`626869a`) makes label 01
true: 1,241 of the 1,247 marks are typed headings, six are whole tools, both
counts computed from the data (marks whose href carries no fragment), so a
seventh tool corrects the sentence by itself. The redesign commit then adds
to `facts()`: the flagship (largest independent document by the pass's own
count, its exact cap radius, one readable section inside it), the corpus
split by surface, the course-shelf totals, and `homeC`, the weighted centre
of the independent work. `labels()` is rewritten: stop 01 opens on the
flagship, stop 02 leads with the two essays before the midpoint mechanics,
stop 03 keeps the largest-cap geometry and gains the course shelf's scale.
Stops 04, 05 and 06 stand as audited, deliberately: the diagnosis defended
them.

**`atlas.js`.** The `one` stage is replaced by a `flag` stage (cap drawn at
the flagship's measured radius, its field keyed at the multiplier the
refinement pass verified above 3:1). The boot camera reads `homeC` from the
facts blob, so the sphere's first face is the independent work instead of
inherited yaw 0.6. Sphere captions rank independent work above larger course
references. Staged zoom clamps to 1 at phone widths.

**`build/build_site.py` and `site.css`.** A one-sentence corpus lede under
the h1, every figure interpolated; a style for it; a paper background under
the phone hint and keys so they stand on ground rather than on stem tips.

## What I verified, with the number

Every figure in the built page recomputed independently from the placement
pass: **23 of 23 checks pass** (flagship name, 59, 32°; pair 5 shared, 37°;
big 92, 36°, 882 marks from 34 documents, 102 inside the circle; knot 15 by
7, 52° to 84°; parallel 34°N, 291, 266, 25 ringed, 18 below; totals 1,247
and 50 in both lede and stop 06; the afacts blob agrees with the pass to
4 decimals). Build regenerates the page from source and the second run
reports **rewrote: nothing**; `checks passed` on every build. Keyboard walk:
58 tab stops sampled to the footer, **0 invisible, 0 inside the clipped
index**. Scripts off: **1,297 links render, all six plates and the lede
visible, nothing hidden**. Horizontal overflow **0 at 1440, 820 and 390**.
Console errors: one, the CDN font this sandbox cannot reach (the standing O1
referral, not this change).

Lighthouse, one host, gzip server, real 13.4.1. Desktop: **100 / 100 / 96 /
100 in five of five runs**, FCP 438 to 488 ms, TBT 0. Mobile, twenty runs in
four batches of five: **pooled median 97**, the floor exactly, spread 83 to
98, batch medians 97, 96, 97, 96. The honest reading: the page sits at the
floor on this host and the score's grain is coarser than the margin. The one
83 was the first, cold run; blocking time ranged 88 to 557 ms. On the
faster hardware the earlier phases measured on, this build sits above the
floor, but I cannot show you that from here.

## The adversarial case against this work, and what it did

**The attack that landed.** The lede and stop 01's second paragraph stated
the same four corpus figures one viewport apart. A reader meets 50/12/4/34
twice in 300 pixels, which is exactly the kind of redundancy the diagnosis
convicted the old page of. Acted on before reporting: stop 01 now carries
only what the lede does not, the tool honesty and the size rule
(`dbfcc4e^..`, the dedup commit), and check 23 asserts the duplicate
sentence is gone.

**The attacks that did not land, and my concessions.** One: "the inversion
is cosmetic, three stops of six are untouched." Half true by design; the
diagnosis defended 04 and 05 as the page's most distinctive material and 06
is the handover. The subject changed where the diagnosis located the
problem, stops 01 to 03, which are the ones a thirty-second visitor sees.
Two: "the featured section is still chosen by a string heuristic." Conceded
in part: `_readable_score` now runs only inside the flagship, so every
candidate is the chosen work, but the sentence-level pick is still
mechanical. The editorial override, one `featured` key in `pieces.json`
naming an anchor, is a five-line follow-up if you want to choose the
sentence yourself. Three: "stops 01 and 02 both feature the same document."
True, and kept deliberately: the flagship's shared vocabulary with its
neighbour is continuity, not repetition, and the camera move between the
stops is the demonstration. Four: "the mobile floor is met by zero margin."
Reported exactly as measured, above.

## What I tried and rejected

A `featured` editorial key in `pieces.json` for stop 01's named section:
rejected for this pass because it makes content policy without your voice;
the mechanical scoped pick is defensible and reversible. Re-ordering north
to stop 02: rejected because the pair stop needs the flagship fresh in mind,
and north's argument lands harder after the coursework's scale is admitted
at stop 03. Cutting the tour default entirely (Direction C's move):
rejected as part of B, because stop 01 now opens on the work, which removes
the reason to skip it.

## What I would need that I cannot see from here

A stranger. Every claim about the thirty-second experience is design
reasoning checked against screenshots, not observation of a person. One
recruiter-shaped reader, told nothing, timed for thirty seconds, asked what
the sphere is and what you wrote: that is the test this direction stakes
itself on, and no measurement in this report substitutes for it. Second, a
real phone: the mobile score here rides a 4x CPU multiplier on shared cloud
hardware, and 83-to-98 jitter says the instrument is at its resolution
limit. Third, whether GitHub Pages' gzip and caching match my local server;
the byte and FCP figures assume they roughly do.

## The single change carrying most of the improvement

**The boot camera plus the flag stage: the sphere's first face is now the
independent work, and the first sentence names your largest independent
project instead of explaining the encoding.** If you reject everything
else, keep commit `a55a3ff`'s changes to the boot camera and stop 01, which
stand alone. The lede, the caption ranking and the label rewrites for stops
02 and 03 each help, but the first three seconds are where the inertness
lived, and those two decisions are what changed them.
