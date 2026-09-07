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
channel is named once, on its diagonal square. Clicking a cell assigns Variable 1 to the
row channel and Variable 2 to the column channel.

**Channels** — size, lightness, hue, orientation, shape, texture. Both variables have five
ordered levels, so every channel is legal for either variable and the whole matrix is
fillable. Position is deliberately excluded: it is the layout rather than a channel you
combine freely, and it is handled separately.

**Colour** — hue and lightness are two axes of one percept, so they cannot be two separate
fills. They are composed using ColorBrewer's single-hue sequential palettes: hue selects
the ramp (Blues, Greens, Oranges, Reds, Purples), lightness selects the class within it.
Lightness alone uses Greys. The 6-class palettes are used with the lightest class dropped,
which is too pale to read as a mark on white.

**Placement** — `grid` packs the marks into an even lattice, `scatter` places them at
uniform random. An `objects` slider runs from 5 to 300; marks shrink as the field gets
crowded so they stay legible.

**Spatial correlation** — a slider for how strongly the values relate to where the marks
are, which is the point of the tool: the same pairing is far more legible when it lines up
with the layout. The slider is the share of marks taking the spatial value rather than
their random one, so structure emerges continuously and reversibly. Two field shapes:

- `gradient` — Variable 1 runs left to right, Variable 2 top to bottom
- `regions` — each variable gets its own smooth 2D field, so values clump into irregular
  patches with no preferred direction

`V1 / V2 / both` chooses which variable the correlation applies to.

**Properties** — for each selected pair, Bertin's characteristics of the two channels
(selective, associative / dissociative, ordered, quantitative) with their usable number of
steps, plus one line on how the two behave when read together: *separable*, *partly
integral*, *integral*, *interfering*, *coupled*.

## Implementation notes

Size is baked into each glyph's geometry rather than applied as a `scale()` transform. A
transform would scale a mark's texture pattern along with it, so large marks would show
coarse hatching purely as a side effect of size, tangling the two channels together.

Rotation *is* still a transform, so under `orientation × texture` the hatch rotates with
the mark. That is the physically sensible reading, but the two channels are visibly coupled
in that cell.

A few of the pair notes describe this implementation rather than perception in general —
the ones about small marks losing shape or texture depend on the glyph sizes used here.

## Not yet built

- Mark types (point / line / area) gating which channels exist
- Variable data types (nominal / ordinal / quantitative) changing the mappings
- Position as an explicit, separately handled channel
- Stress tests: greyscale, thumbnail size, CVD simulation, very dense fields
- Shareable URL state, SVG export

## Reference points

Bertin, *Sémiologie Graphique* · Cleveland & McGill on elementary perceptual tasks · Ware
on integral vs. separable dimensions · Munzner's channel effectiveness ranking ·
ColorBrewer (Cynthia Brewer) for the palettes
