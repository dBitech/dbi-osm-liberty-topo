# dBi Technologies OSM Liberty Topo [![BSD licensed](https://img.shields.io/badge/license-BSD-blue.svg)](https://github.com/dBiTech/dbi-osm-liberty-topo/blob/gh-pages/LICENSE.md) [![GitHub CI status](https://github.com/dBiTech/dbi-osm-liberty-topo/workflows/CI/badge.svg)](https://github.com/dBiTech/dbi-osm-liberty-topo/actions?query=workflow%3ACI)

<img align="right" alt="OSM Liberty" src="logo.png" />

A free Mapbox GL basemap style for everyone with complete liberty to use and self host. dBi OSM Liberty Topo is a fork of [OSM Liberty](https://github.com/maputnik/osm-liberty) which is a fork of [OSM Bright](https://github.com/openmaptiles/osm-bright-gl-style) based on free data sources with a mission for a clear good looking design for the everyday user. It is based on the vector tile schema of [OpenMapTiles](https://github.com/openmaptiles/openmaptiles), with terrain layers from non-OpenStreetMap sources.

**[Preview OSM Liberty with Maputnik](https://maputnik.github.io/editor/?style=https://dbitech.github.io/dbi-osm-liberty-topo/style.json)**

## Usage

You can use the style in your Mapbox GL maps.

By default, the vector tiles and glyphs are served from [Maptiler Cloud](https://www.maptiler.com/cloud/) and the raster tiles and sprites directly from GitHub.
You would need to [subscribe](https://www.maptiler.com/cloud/plans) to Maptiler Cloud to get an access key and replace the placeholder {key} for the [vector source](https://github.com/maputnik/osm-liberty/blob/gh-pages/style.json#L11) and [glyphs](https://github.com/maputnik/osm-liberty/blob/gh-pages/style.json#L23) with your own key.


Another option is to create your own vector tiles with [OpenMapTiles](https://github.com/openmaptiles/openmaptiles) and host the tiles and assets yourself for complete liberty.

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset=utf-8 />
  <title>dBi Technologies OSM Liberty Topo</title>
  <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
  <style>
    body { margin:0; padding:0; }
    #map { position:absolute; top:0; bottom:0; width:100%; }
  </style>
  <script src='https://unpkg.com/maplibre-gl@1.15.2/dist/maplibre-gl.js'></script>
  <link href='https://unpkg.com/maplibre-gl@1.15.2/dist/maplibre-gl.css' rel='stylesheet' />
</head>
<body>
  <div id='map'></div>
  <script>
  var map = new maplibregl.Map({
      container: 'map',
      style: 'https://dbitech.github.io/dbi-osm-liberty-topo/style.json',
      center: [-119.28,49.872476],
      zoom: 5,
      hash: true
  });
  </script>
</body>
</html>
```

## Data Sources

- [OpenMapTiles](http://openmaptiles.org/) as vector data source
- [Natural Earth Tiles](https://klokantech.github.io/naturalearthtiles/) for relief shading
- [Maki](https://www.mapbox.com/maki-icons/) as icon set
- [AWS Terrain Tiles](https://registry.opendata.aws/terrain-tiles/) as hillshade layer
## Map Design

The map design originates from OSM Bright but strives to reach a unobtrusive and clean design for everyday use.
Colored relief shading from Natural Earth make the low zoom levels look good.

[![OSM Liberty Map demo](demo/zoom.gif)](https://maputnik.github.io/osm-liberty/)

## Edit the Style

You can [edit the style directly online in Maputnik](https://maputnik.github.io/editor?style=https://dbitech.github.io/dbi-osm-liberty-topo/style.json).

This style actually triggered the need for the development of [Maputnik](https://github.com/maputnik/editor/).

A pre-commit hook is included to validate and format the JSON styles using
[`mapbox-gl-style-spec`](https://www.npmjs.com/package/@mapbox/mapbox-gl-style-spec).
To use, just install the NPM dev dependencies:
```
npm install
```
and then validate or format the style with
```
npm run validate
npm run format
```

Validation and reformatting will happen automatically on commit if you have the
dependencies installed.

## Icon Design

A [Maki](https://github.com/mapbox/maki) icon set using colors to distinguish between icon categories.

Maki is a living project and adds new icons over time, which means that there
could be new icons that OSM Liberty could use for POIs. `maki_list.py` is a
simple script to list both the names in OSM Liberty's iconset that don't map to
any valid Maki name, and the Maki names that are not currently used in OSM
Liberty's iconset. You can run the script with `python3 maki_list.py`.

**Color Palette**

Color Name   | Hex Value
-------------|----------
Blue         | `#5d60be`
Light Blue   | `#4898ff`
Orange       | `#d97200`
Red          | `#ba3827`
Brown        | `#725a50`
Green        | `#76a723`

**Modify Icons**

1. Take the `iconset.json` and import it to the [Maki Editor](https://www.mapbox.com/maki-icons/editor/).
2. Apply your changes and download the icons in SVG format and the iconset in JSON format.
3. Mandatory if the updated `iconset.json` should become part of this repo: Format the JSON with `cat iconset.json | jq -MS '.'` for better legibility.
4. Add the SVG files from the folder [svgs_not_in_iconset](https://github.com/maputnik/osm-liberty/tree/gh-pages/svgs/svgs_not_in_iconset) to the folder `svgs` downloaded from the Maki Editor.
These are the SVGs for road shields, the dot used for city and town layers and the road area pattern which could not be modified using the Maki Editor. To modify these you could use e.g. [Inkscape](https://inkscape.org).
5. Install [spritezero-cli](https://gitlab.com/beyondtracks/spritezero-cli): `npm install -g @beyondtracks/spritezero-cli` (We're using a maintained fork of https://github.com/mapbox/spritezero-cli.)
6. Generate the low resolution sprite: `spritezero osm-liberty ./svgs/`
7. Generate the high resolution sprite: `spritezero --retina osm-liberty@2x ./svgs/`

## Have a look at ...

- [OSM Liberty Topo](https://github.com/nst-guide/osm-liberty-topo) - a topographic fork of OSM Liberty
