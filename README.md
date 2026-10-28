# Channel Brewer

A sandbox for exploring **combinations of two visual channels** — ColorBrewer's premise
applied to Bertin's visual variables rather than to colour palettes.

Right now this is the *space*, not the guidance. Pick a pair of channels, see a field of
marks encoding two variables with them, and judge it yourself. There is no scoring and no
ranking of pairs.

**[Open the tool →](https://ebertini.github.io/channel-brewer/)**

## Run locally

Open `index.html`. One file, no build, no server, no dependencies — it works from `file://`.

## What's in it

**The picker** — a lower-triangle matrix of the six channels, 15 distinct pairs. Each
channel is named once, on its diagonal square. The row channel carries Variable 1 and the
column channel Variable 2. Hovering a cell previews its pair in the field; clicking keeps
it, and moving off the matrix returns to the kept pair.

**Channels** — size, lightness, hue, orientation, shape, texture. Both variables are
ordered, so every channel is legal for either variable and the whole matrix is fillable. Position is deliberately excluded: it is the layout rather than a channel you
combine freely, and it is handled separately.

**Colour** — hue and lightness are two axes of one percept, so they cannot be two separate
fills. They are composed using ColorBrewer's single-hue sequential palettes: hue selects
the ramp (Blues, Oranges, Greens, Purples, Reds), lightness selects the class within it.
Lightness alone uses Greys. The 6-class palettes are used with the lightest class dropped,
which is too pale to read as a mark on white. Other numbers of lightness steps are
interpolated in CIELAB between those five classes. ColorBrewer has only five single-hue
ramps, so hues 6–8 (teal, magenta, olive) are built to match Blues class by class in L*
and chroma.

**Steps** — each channel has its own number of steps (Bertin's *length*), set with the
small − / + next to its legend: 2 to 9, or 2 to 8 for hue, orientation and shape. Ordered
channels spread their steps over a fixed range, so more steps pack closer together
instead of extending the range; at 5 steps every scale lands on its original values.
Orientation divides 180° evenly. The setting belongs to the channel, so it carries over
when you pick another pair.

**Placement** — `grid` packs the marks into an even lattice, `scatter` places them at
uniform random, and `lines` is described below. An `objects` slider runs from 5 to 300; marks shrink as the field gets
crowded so they stay legible.

**Lines** — the third mode draws each object as a straight line in a slope chart: every
line runs between the same two x positions and only its two end heights vary. That is the
common core of line charts, parallel coordinates and network edges. The data sets the
path, which fixes the line's direction and leaves no outline to vary, so orientation and
shape are greyed out in the matrix, leaving 6 of the 15 pairs. Size becomes stroke width
and texture becomes a dash pattern, with dash and gap equal so every level carries the
same ink. A line spans the whole plot, so spatial correlation uses what it looks like: regions
are laid over its slope and mean height, so lines that look alike get similar values. Switching
to lines with an unavailable pair falls back to hue × size, and switching back restores
the earlier pair.

**Spatial correlation** — a slider for how strongly the values relate to where the marks
are, which is the point of the tool: the same pairing is far more legible when it lines up
with the layout. The slider is the share of marks taking the spatial value rather than
their random one, so structure emerges continuously and reversibly. Each variable gets
its own smooth 2D field, so values clump into irregular patches with no preferred
direction.

`V1 / V2 / both` chooses which variable the correlation applies to.

## Implementation notes

Size is baked into each glyph's geometry rather than applied as a `scale()` transform. A
transform would scale a mark's texture pattern along with it, so large marks would show
coarse hatching purely as a side effect of size, tangling the two channels together.

Rotation *is* still a transform, so under `orientation × texture` the hatch rotates with
the mark. That is the physically sensible reading, but the two channels are visibly coupled
in that cell.

## Not yet built

- Area marks (choropleths, treemaps) as a fourth mark type
- Variable data types (nominal / ordinal / quantitative) changing the mappings
- Position as an explicit, separately handled channel
- Stress tests: greyscale, thumbnail size, CVD simulation, very dense fields
- Shareable URL state, SVG export

## Reference points

Bertin, *Sémiologie Graphique* · Cleveland & McGill on elementary perceptual tasks · Ware
on integral vs. separable dimensions · Munzner's channel effectiveness ranking ·
ColorBrewer (Cynthia Brewer) for the palettes
