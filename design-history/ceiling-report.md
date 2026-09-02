# Ceiling pass: report

Branch `ceiling`, ten commits on top of `atlas-work-first`, each the smallest
defensible unit. The audience assumption and the section 5 answer were
delivered before any code in `plan.md`, alongside the plan for all five
fronts. Screenshots in `shots/` (390, 820, 1440, both themes) and the
resilience states beside them.

## What changed, by front

**A. First contact.** The home page's section order was the Atlas defect in
page form: three methodology sections before any work, Selected work sixth.
New order: Start here, Selected work, the corpus figure and its named twin,
then Three marks, its failure, and the note. Nothing deleted; one directional
cross-reference corrected. The contact address, which existed only in the
footer, now sits under the hero stats with a link to About.

**B. Legibility, assessed and mostly left alone.** The two-click test passes
on all four listing pages: every piece is reachable from its section page in
one click, and every section page is one click from anywhere. Coursework is
already subordinated where it matters: the home page's Start here block ranks
it third of three, the index orders it last, and the library labels it. I did
not restructure four listing pages inside this pass; the honest finding is
that the listing pages list well, and their real weakness, that a landing
page sells a piece less hard than the piece deserves, is a copy question for
you rather than a structure question for me.

**C. Atlas.** The six tool marks stand off the sphere at 1.13 radii on their
own bearings, tethered to the surface point they stand over, on the altitude
channel the stems established. The key names the channel. Label 01 already
admitted in prose that the six are not headings; the picture now agrees, and
the home teaser elevates the same six so the two views of the corpus make one
claim. Perspective projection: refused again for the standing reason. WebGL:
under the brief's own condition 1 it cannot be reached without the
perspective baseline I am declining to build; refusal is the brief's stated
correct outcome. Glow, light direction, depth of field: refused under
section 4, none encodes a recorded quantity.

**D. Infrastructure.** Inter Variable 4.1.1 self-hosted, subset to the
corpus: 444 glyphs, 75,956 bytes against 352,240 full, same origin, layout
features kept (kern, liga, calt, ccmp, tnum, frac, sups, subs, zero). The
build rewrites any hand-copied CDN preload in the same pass that owns the
nav, so the fix is a fixed point, reader.html included. Zero references to
any external host remain in any page. Best Practices 96 to 100 on all nine
pages; the one standing console error is gone.

**E. Resilience.** Tested: scripts off on all nine pages (all render their
full link structure, the Atlas serving 1,323 links and all six plates);
canvas blocked; fonts blocked (metric-matched fallback holds the layout);
200%-zoom-equivalent reflow at 720px (zero overflow); forced colors; print
to PDF on home, Atlas and one piece; keyboard walks on home (139 stops, zero
invisible) and Atlas. **Two things broke and were fixed.** A blocked canvas
crashed the boot after it had hidden the index, leaving a blank stage over
nothing; the script now returns before touching state, so that reader gets
the server-rendered page whole. And print showed the drag hint and tour
buttons as dead furniture; a print rule drops them.

## What I removed, and why

One, the CDN font link and preload from every page: the last external
dependency, the last console error, and the last render-blocking third-party
request. Two, the retired first stage's dead exports from the facts blob,
left behind by the re-anchoring pass. Three, the interactive furniture from
the print stylesheet. And one removal of a divergence rather than of bytes:
the home teaser no longer draws the six tools on the surface the Atlas
stands them off, the exact class of two-claims defect the teaser's own
comment warns about.

## Before and after, every row of section 10

| | before | after |
|---|---|---|
| Desktop Lighthouse, all nine pages | 100 / 100 / 96 / 100 | **100 / 100 / 100 / 100, all nine** |
| Mobile performance, Atlas | 97 pooled median (83–98) | **99 median of ten: 98, 96, 99, 99, 99, 99, 99, 99, 99, 99** |
| Mobile performance, home | not measured | **100 × 5** |
| Mobile, research / library | not measured | **100 × 3 each** |
| Desktop TBT / CLS | 0 ms / 0 | **0 ms / 0** (a 0.058 CLS my font fix exposed was found and zeroed) |
| Drag framerate, 1,247 marks | 60 fps | **60 fps** (427 frames / 6.26 s uncapped headless; loop idles at 0 rAF settled) |
| Label collisions | 0 in 48 | **0 in 48** (four widths, free and focused, re-run because marks moved) |
| Leader crossings | 0 | **0 by construction**: no leader attaches to a tool mark, and no labelled mark moved |
| Horizontal overflow 390 / 820 / 1440 | 0 / 0 / 0 | **0 / 0 / 0** (and 0 at 720) |
| Console errors | 1 (font CDN) | **0** |
| Key entries below 3:1 | 0 | **0** (tool marks keep their measured 4.99:1 light / 5.78:1 dark; colour unchanged, only position) |
| Keyboard-reachable marks | 1,247 | **1,247**, walks clean |
| Build idempotency | rewrote: nothing | **rewrote: nothing** |
| Self-verifying checks | 23 | **24**: the figure battery passes 24 of 24, and the build itself gained the font-coverage check, proven to fire on an injected U+0142 and to pass after restoration |

Mobile FCP moved from ~1,815 ms to ~1,700 ms and home mobile FCP to 1,066 ms;
the self-hosted font is most of it.

## Adversarial self-review

**The attack that landed.** My font fix regressed a budget and nearly
shipped: Atlas desktop CLS went from 0 to 0.058, because the plates collapse
at boot used to happen before first paint and the faster same-origin font
made paint early enough to watch it. The fix ships the collapsed state in
the HTML (plates after the first carry `hidden`) with a noscript reveal, so
CLS is 0, no-JS still shows all six plates, and deep links still land. The
uncomfortable part is what it implies: the old CLS 0 was partly an artifact
of a slow font, and only measuring every budget after every change caught
it.

**Attacks that did not land, with concessions.** One: "the 1.13 elevation is
arbitrary." Conceded in part: the channel is binary (is a tool), so the
amount encodes nothing; it is one legibility constant, unlike the stems'
count-scaled formula, and the key claims only the category. Two: "the tether
is decorative." Conceded that at the limb its alpha sits below 3:1; it is
construction like the leader lines, the keyed category lives in the mark,
which clears 4.99:1. Three: "the home reorder buries the three-marks
demonstration." It moves from first to fifth; the defence is the measured
lesson of the Atlas pass, work before apparatus, and the demonstration reads
as proof once a reader has seen work worth proving. Four: "you subset the
future away." True risk, and the new check is the answer: a page using a
glyph Inter covers that the subset lacks now fails the build by name.

**Tried and rejected.** A dark-first Atlas (real case, wrong pass: it breaks
site-wide coherence for the stated reader and the palette rule demands a
measured justification I cannot honestly write while the cream site is the
brand). Trimming the teaser payload (already two decimals and ~6 KB gzipped;
the comment in the build was ahead of me). Failing the build on any
non-subset character at all (the fallback renders emoji and box-drawing
today exactly as before; failing on those would be noise, so the check fires
only on characters Inter itself covers).

**What I cannot see from here.** Still the stranger: no measurement here
substitutes for one recruiter given thirty seconds. Also a real phone
rather than a 4x CPU multiplier, and GitHub Pages' caching behaviour versus
my gzip server. And whether "Start here" first reads as inviting or as
hand-holding to the second reader, the technical interviewer; I judged the
first reader outranks them.

**The single change carrying most of the improvement.** The self-hosted
font subset, commit `22da45d`, standing alone: it removes the last external
dependency and console error, lifts Best Practices to 100 on nine pages,
cuts mobile FCP on every page, and survives the corporate network the
audience assumption says the reader is on. Keep that one even if every
other commit is rejected.
