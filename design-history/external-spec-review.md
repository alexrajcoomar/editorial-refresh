# The "Celestial Engine" specification, reviewed item by item

An external specification proposed rebuilding the Atlas as a WebGL system:
three.js, GLSL shaders, 2,000+ nodes, orbiting asteroid belts, bezier
constellation arcs, cursor gravity, an octree, six TypeScript deliverables.
The instruction attached to it was to execute with judgment: take what
improves the portfolio, preserve what works, avoid unnecessary change.

The review below maps every item in the specification to one of four
verdicts: already built (often in a stronger form), executed now, refused on
a ratified constraint, or refused as unnecessary. One item survived contact
with the codebase and shipped. The rest is either behind us or forbidden by
rules this project adopted deliberately and in writing.

## Executed: the one real defect the specification found

**"Eliminate per-frame object allocation within the animation loop.
Pre-allocate all color arrays."** (Agent 4, memory governance.) This was
real. `draw()` built every mark's colour by string concatenation through
`rgba()`, fresh on every mark on every frame: at 1,373 marks and 60 fps,
tens of thousands of short-lived strings per second through the hottest
loop in the file, all garbage.

The fix is `tone2()`, a quantised colour cache: alpha snaps to 1/48 steps,
the composed `rgba()` string is cached under `hex+step`, and the cache is
emptied inside `readColours()` so theme changes rebuild it from the new
palette. Eight call sites in `draw()` route through it: the warm and hit
fills, the ring stroke, the field fill, the independent fill, the course
stroke, the tool fill, the personal fill, and the trail ring stroke.
Strokes with derived alphas (`a*1.25`, `a*0.85`) quantise the derived
value, so the cache stays small.

Measured on the final tree, gzip server, uncapped headless Chromium:
drag holds 69.2 fps over the full sweep with zero page errors; the
demand-driven contract is intact (the timeline below); and the visual cost
of quantisation is a maximum channel delta of 4/255 across 4.5% of canvas
pixels on an identical-camera A/B screenshot, invisible at any zoom.

## A measurement retraction, before the timeline

The first idle check after the change reported 144 rAF callbacks in a
4-second idle window, which read as a broken loop. The probe was wrong, not
the loop: it counted frames with a callback that unconditionally
rescheduled itself, so it measured the browser's frame rate, which is 60/s
whenever anyone, including the probe, holds a pending rAF. Any page on
earth scores "60 fps forever" under that probe. It was replaced with an
instrumented `requestAnimationFrame` that counts only requests the page
itself makes. Every number in this file comes from the corrected probe.

The corrected timeline, cold load, no input: 0 rAF/s for 26 straight
seconds. After a drag: 60, 60, 26, then 0 within three seconds as momentum
and the grid fade drain. Entering the free view: about six seconds of
flight and ambient drift, then 0 for five seconds, then at exactly the
12-second idle mark the survey wakes and the shape becomes what the design
says it is: 60 fps during each 1.5-second flight, 0 during each dwell.
One input during a flight: back to 0 within the same second. The loop
idles at zero, the survey pays only for motion, and the tour stage never
surveys because the reader there is already being shown something.

## Already built, sometimes in stronger form

**The Fibonacci lattice** (Agent 2). The specification's placement formula
is, symbol for symbol, the formula `build/atlas.py` has shipped since the
redesign: theta from arccos(1 − 2i/N), phi from the golden angle. Its
"localized clustering offsets based on parent categories" is the part we
refuse below.

**Depth occlusion** (Agent 1's atmospheric shader; §3's dot-product
opacity ramp). The Atlas dims and desaturates the back hemisphere through
the depth alpha ladder in plain canvas paint. A GLSL shader is a means;
the end already exists, and the 2D form of it costs no GPU pipeline, no
context-loss handling, and no second renderer.

**Cinematic fly-to** (Agent 3). `flyTo()` with eased tweens, distance
matched to the cap radius of the target, is how every stage change, focus,
survey stop, and word-light click already moves. The specification wants
cubic bezier easing specifically; no reader can tell ours apart, and no
data hangs on the difference.

**Label occlusion and collision** (Agent 3). Labels whose anchors turn
past the limb already wait, and the ladder resolves collisions from
DOM-measured rectangles, which is stricter than the proposed grid because
it measures rendered text, not estimated boxes. Zero collisions in 48
sweeps is the standing figure.

**Two-way state sync** (Agent 4). Search, the kind filter, the document
list, deep links, and the hash already round-trip with the sphere. This
was built as the price of admission, not as a feature.

**The reference grid** (§3's geodesic wireframe). Ours is the drag-only
graticule: it rises while the sphere turns, when orientation is the
question, and settles when it stops. A permanent 10% grid at a fixed
`#888888` is strictly worse twice over: always-on ink for a sometimes
question, and a hardcoded colour in a two-theme palette.

**60 fps on integrated GPUs** (§1). The measured drag rate is 69.2 fps
uncapped and headless. The stronger claim the specification cannot make:
at rest this page draws nothing at all, which no "sustained 60 fps"
architecture matches.

## Refused on ratified constraints

**three.js, TypeScript, GLSL, six module deliverables** (§2, §4). The
footer's claim, hand-written HTML and CSS with no framework, is
load-bearing and true. The redesign brief fixed no-framework, no-WebGL,
no-CDN as constraints, and WebGL's own entry condition (a measured need
the 2D renderer cannot meet) has never been met. A build step for
TypeScript violates the no-bundler rule the same way.

**2,000+ nodes, 3,000+ belt particles** (§1, Agent 1). The corpus has
1,373 sections. Every mark on the sphere is one of them. Two thousand
marks would require inventing six hundred, and the honesty contract is
one sentence: every mark corresponds to recorded data. Particle counts
are not a target; they are a census, and the census is 1,373.

**Asteroid belts and Keplerian orbits** (Agents 1 and 2). Orbital
eccentricity and 15–35° inclination encode nothing about any document.
The six tools already stand off the sphere at 1.13 radii precisely
because detachment is the honest form of their difference: they are named
one-point objects, elevated and tethered, and they hold still, because
position is the data.

**Cursor gravity and spring dynamics** (Agent 2). Marks pulled toward the
pointer are marks displaced from the coordinates the placement pass
computed. A damped harmonic oscillator un-places the data smoothly, but
un-places it. Hover already answers the pointer honestly: the mark warms,
its label rises, its owners fan, and nothing lies about where anything is.

**Constellation bezier arcs with travelling light pulses** (Agent 3).
The corpus records no edges. This is not a missing feature but a measured
fact, verified in the first audit, and drawing arcs between documents that
share a hover would manufacture relationships out of adjacency. This
exact class of defect, geometry with no datum behind it, is what the
redesign was scoped to prevent.

**The search resonance pulse shader** (Agent 1). Search already answers on
the sphere: matching territories light, non-matching marks dim, and the
result list and sphere agree. A wavefront propagating outward from the
match adds animation to an answer already delivered, and under the
override rule every moving thing must correspond to data; a ripple's
radius corresponds to elapsed time since a keystroke, which is not a fact
about the corpus.

## Refused as unnecessary

**The octree** (Agent 4). A spatial index earns its complexity when the
linear alternative misses budget. Hit-testing here is one pass over 1,373
screen-space points, run on pointer events rather than per frame, and the
measured drag rate with hover active is 69.2 fps. The specification's own
budget is 1 ms; nothing here has ever been measured near it. Code that
solves an unmeasured problem is the kind of code this project removes.

**Maximum 5 draw calls** (§3). Draw-call economy is GPU accounting. A 2D
canvas paints immediate-mode; the constraint does not translate, and the
figure that actually governs, whole-frame cost, is measured directly and
passes.

**The agent swarm** (§2). Four specialised agents are proposed to build
six files. The system that exists is one generator, one runtime file, and
24 self-verifying checks; its maintainability comes from smallness. No
division of labour is needed to maintain 2,000 lines that already verify
themselves.

## The judgment, in three sentences

The specification describes an impressive generic product and prescribes
abandoning every constraint that makes this particular one credible: the
no-framework claim, the census-exact mark count, the no-edges honesty, the
stillness of placed data. Its one transferable insight, that the hot loop
should not allocate, was real, is now shipped, and measurably cost nothing
visually. Everything else was either already here in a form that tells
the truth, or was declined because it would not.
