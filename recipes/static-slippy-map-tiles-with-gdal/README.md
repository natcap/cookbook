# Static Slippy Map Tiles with GDAL

## Background

There are plenty of cases where we have large spatial raster layers that

1. Are represented by rasters that are too large and cumbersome to download
   easily
2. Require GIS expertise to easily visualize and interpret
3. Can have styles applied once, where the styles do not change for any reason.

There are many applications where it is useful to preview a large spatial
raster, but we have previously not known how to generate these map tiles so
that they could be hosted and served as static files, _without_ the need for
expensive servers and specialized software that requires maintenance.

## Setup

To install dependencies:

```
mamba create -p ./env -c conda-forge python=3.10 gdal jupyter git ipyleaflet wget
```

## Running the notebook

```
mamba activate ./env
jupyter notebook demo.ipynb
```
