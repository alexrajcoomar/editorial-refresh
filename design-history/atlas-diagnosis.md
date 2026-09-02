# Step One: why the Atlas is inert

Diagnosis only. No proposals appear in this document.

## Your facts, checked

**atlas.html is generated output.** Correct. It is one of the nine
`SHELL_PAGES` that `build_site.py` regenerates on every run, and hand-editing
it is lost at the next build.

**The sources are build_site.py, atlas.py, site.css and atlas.js.** Correct,
with two additions you need before editing. First, `harvest()` writes anchor
ids into the 50 piece files themselves, once, idempotently: the pieces are a
source too, and the ids already handed out are load-bearing. Second, each wall
label is split across two files. Its prose lives in `atlas.py:labels()`, but
its camera, its lit function and the construction it draws live in
`atlas.js:STAGES`. A change to "the six labels" that edits only `atlas.py`
changes what a label says while leaving what it shows untouched, and the two
can drift.

**Every figure in the copy is interpolated at build time.** Correct. Every
numeral in the six labels, the `#afacts` blob, and the header counts ("Search
1,247 sections") come from `facts()`. The only static prose is the key and the
hints, which carry no figures.

**The six tool marks make label 01 false.** Correct, and it is false twice,
not once. `harvest()` short-circuits pieces whose kind is in
`ONE_POINT_KINDS = {"Tool"}` and appends `{"t": p["t"], "id": "", "lvl": 1}`:
the mark's text is the catalogue title from `pieces.json`, which nobody typed
into a document, so "Every mark on this sphere is a heading somebody typed
into a document" fails for six marks. And because `id` is empty, those six
hrefs carry no fragment, so "Click it and the passage opens, not the front of
the piece, and all 1,247 marks behave the same way" fails for the same six,
which open `daily-learning-cockpit.html` and five others at the top. I checked
for other outliers: exactly six marks in 1,247 have no anchor, and no other
kind bypasses harvesting. Your "one real outlier" is the complete list.

---

## The diagnosis

The page is a proof when it should be an exhibition, and every individual
decision below is a place where that choice was made. The history explains it:
this page survived two adversarial audits, and each rewrite made "every claim
checkable" more thoroughly the governing value. Copy written to survive audit
addresses a sceptical auditor. A recruiter is not a sceptical auditor, and
prose built to withstand a protractor does not invite anyone to pick one up.

### 1. The default state spends its entire budget on the method

A first-time visitor boots into the tour at stop 01 (`atlas.js` boot: the
`atlas.seen` flag decides, and a recruiter has never been here). The first
sentence on the page is "Every mark on this sphere is a heading somebody
typed into a document." That is a sentence about the encoding. The six stops
run 551 words, and their subjects are, in order: the encoding rule, the cap
geometry and its overlap price, the midpoint placement semantics, the failure
mode of averaging, the classification errors of a boundary line, and the
handover instructions. Fifty documents of actual work appear in those 551
words only as operands of geometric claims. Nowhere in the default path does
the page say the one thing a stranger needs first: fifty documents, twelve of
them independent, and here are the three largest. That sentence exists on the
page, but as the index below the fold, while the above-fold budget proves the
projection is honest to someone who has not yet been given a reason to care
whether it is.

### 2. The one guaranteed-visible passage is chosen by string metrics

Stop 01 names exactly one section, and it is the only piece of the work a
visitor is guaranteed to see. `facts()` picks it with `_readable_score`,
which optimises for: independent surface, 24 to 68 characters, at least four
spaces, not digit-led, level 2, length near 46. Today that lands on "Three
couplings people assert that do not hold." The spotlight decision, the single
highest-value editorial slot on the page, is delegated to a font-fitting
heuristic. It cannot pick your best passage except by coincidence, because
nothing in the score knows what the passage says.

### 3. The boot camera faces the coursework

`cam = {yaw: 0.6, pitch: -0.34}` was never chosen against the data. Computed
at that orientation, the six regions nearest the view axis are AFM 291
Chapter 9, The Gartner Hype Cycle, AFM 291 Financial Assets I, AFM 291
Inventory and Gap Map, AFM 291 Case Guide: Debt Investments, and AFM 291
Chapter 1: coursework, all six. Label 05's own claim is that north is the
independent work, and the camera does not look north. The free view keeps
the same yaw (`STAGES.free` reuses `cam.yaw`), so a returning visitor lands
on the same face. The sphere's first face is its least impressive one, by a
decision nobody made.

### 4. The captions rank by size, and size ranks the coursework

Region captions surface by document size, and the largest documents are
course references (AFM 291 Key Takeaways holds 92 sections against 59 for the
largest independent work). So the only words readable on the sphere at boot
are AFM 291 chapter titles. Meanwhile 882 of 1,247 marks (71%) are hollow
coursework rings, 284 are accent-filled independent marks, 81 personal, 6
tools. Both decisions are individually honest: size is real, and the fill
distinction is real provenance. But their composition means the sphere's ink
budget and its label budget both go to the material a recruiter cares about
least, and the page's own north-parallel argument says so. Nothing in your
override rule forces this: the rule fixes what a mark IS, not which regions
get the caption priority or where the camera points. Those are free
editorial channels currently spent by accident.

### 5. Structure, not cosmetics

Points 1 through 4 share one structure: every editorial channel the page has
(the opening state, the one named passage, the camera, the captions) is
assigned either by the method's own internal logic or by a mechanical
heuristic, never by the question "what should a stranger see first". That is
why the page reads as inert despite being interactive everywhere: drag works,
hover works, search works, every mark opens a passage. The interaction is not
the problem. The page has no editorial voice about its own contents, because
every place a voice could act was given to the method to spend. Fixing
cosmetics inside that structure would produce a prettier proof.

---

## Decisions I would defend in any redesign

**Build-time interpolation and the no-invented-edges rule.** The page's one
genuinely rare property. Every figure recomputes from the pass; stop 03's
false claim was findable precisely because the contract made it checkable.
This is the moat, not the problem.

**Stops 04 and 05 existing at all.** A portfolio that names the failure mode
of its own method ("the honest failure of the method, and it is left
visible") and draws its boundary's false negatives is doing something no
recruiter has seen before. The self-critical material is the most memorable
copy on the page. Its placement in the sequence is an open question; its
existence is not.

**The index as the accessible instrument.** The canvas is `aria-hidden`, the
server-rendered index carries all 1,297 links, works with scripts off, and is
the crawler payload. Ordered independent, personal, coursework, by size:
this is the one place the page already curates, and it is correct.

**The demand-driven render loop, the depth stems, the harvest idempotence.**
All three earned their place through measurement this month. The stems are
the right kind of ornament: elevation is share count, and the key says so.

**One camera, used twice.** The staged views and free exploration sharing
one camera means the tour teaches the same object the reader then drives.
Whatever happens to the sequence, that continuity should survive.

**The 0.45 shrink on shared-heading scatter, the cap-radius formula, the
Fibonacci lattice.** The placement maths is fixed by your brief and I found
nothing in it I would change if it were open: the geometry is not why the
page is inert.
