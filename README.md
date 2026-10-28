# Channel Brewer

Inspired by the popular color selection tool [Color Brewer](https://colorbrewer2.org/), Channel Brewer helps you explore and experience the use of **combinations of two visual channels** in data visualization. 


**[Open the tool →](https://ebertini.github.io/channel-brewer/)**

## Run locally

Open `index.html`. One file, no build, no server, no dependencies — it works from `file://`.

## How to use it



**Triangular Matrix** — Every cell is a combination of channels. Hovering a cell previews the pairs; clicking keeps it selected.

**Main View** - The view in the middle gives you a sense of how the selected combination of channels looks.

**Layout** - Select grid, scatter, or lines to simulate basic visualization arrangements.

**Number of Objects** - Move the slider to increase/decrease the number of objects.

**Spatial Correlation** - Move the slider to increase the correlation that exists between the object placement and the channels. The correlation can be modulated for channel V1, V2, or both.

**Legend** - Check the legend to see how many different levels are used for each channel. Change the number of levels by clicking on the plus/minus signs.


## Not yet built

- Area marks (choropleths, treemaps) as a fourth mark type
- Variable data types (nominal/ordinal/quantitative) changing the mappings
- Position as an explicit, separately handled channel

## Inspirations

Bertin, *Sémiologie Graphique* · Cleveland & McGill on elementary perceptual tasks · Ware
on integral vs. separable dimensions · Munzner's channel effectiveness ranking ·
ColorBrewer (Cynthia Brewer) for the palettes

## Contact me!

If you use this tool for yourself or to teach a class, please let me know! I am very interested in knowing if anyone finds it useful to learn data visualization concepts. Also, feel free to send a pull request if you want to make any changes.

You can contact me on [LinkedIn](https://www.linkedin.com/in/ebertini/) or [Substack](https://substack.com/@enricobertini).