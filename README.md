# Things To Do Around Boon Keng

A mapped, filterable guide to 57 places within a walk, a bus, or a few North East Line stops of Boon Keng, Singapore.

**Live:** https://fang89.github.io/boon-keng-50/

Every place is plotted from its real address, with distance rings at 500 m, 1 km, 2 km and 3 km from Boon Keng MRT, so you can see at a glance what is genuinely walkable. The category and distance filters drive the map and the list together; clicking a card flies the map to that pin.

## What's in it

| Category | Count |
|---|---|
| Food | 15 |
| Shopping & malls | 11 |
| TCG / card shops | 7 |
| Gyms | 6 |
| Outdoors | 6 |
| Heritage & old streets | 6 |
| Sports | 4 |
| Video game shops | 2 |

By distance from Boon Keng MRT: **28** under 1.3 km, **24** between 1.3 and 2.5 km, **5** beyond 2.5 km. Nearest is Bendemeer Market at 134 m; furthest is NEX at 3.61 km.

## How the distances work

Coordinates come from [OneMap](https://www.onemap.gov.sg/), Singapore's national address database — not from hand-placed pins. Distances are straight-line (haversine) from Boon Keng MRT, so real walking is somewhat longer. Where a shop sits inside a larger building, the pin is the building: Sim Lim Square, Bugis+ and the hawker centres each hold several entries. Markers that share an address are fanned out about 24 m so all of them stay clickable; zoom in, or click the card, and they separate.

The distance bands are derived from the computed numbers rather than assigned by hand, so they can't drift out of sync with the map.

## Running it

No build step and no external JavaScript — Leaflet is vendored into `vendor/`. Map tiles are the only network call. Open `index.html`, or serve the folder:

```
python3 -m http.server 8000
```

## Editing

Every place is one row in the `P` array near the bottom of `index.html`:

```js
["Name", "Category", "walk|near|far", metres, lat, lng, "Address", "One-line blurb", "Optional tip"]
```

Categories must be one of `Food`, `Shopping`, `TCG`, `Games`, `Gyms`, `Sports`, `Outdoors`, `Heritage`; each has a colour token in the CSS at the top of the file, used for both the card accent and the map marker. Chip counts, the headline number and the distance-band counts are all computed from the array, so adding a row is the only edit needed.

To add a place, get its coordinates from OneMap:

```
curl "https://www.onemap.gov.sg/api/common/elastic/search?searchVal=29+BENDEMEER+ROAD&returnGeom=Y&getAddrDetails=Y&pageNum=1"
```

`data/coords.json` holds the geocoder output for everything currently on the map, including which query matched.

## Caveats

Hawker stalls close on rotation and the older ones shut when they sell out. Shop units inside Sim Lim Square and Bugis+ move around — check the store's socials before travelling for a specific one.

Compiled August 2026. Corrections welcome via pull request.

## Credits

Map tiles © [CARTO](https://carto.com/attributions), data © [OpenStreetMap](https://www.openstreetmap.org/copyright) contributors. Geocoding by [OneMap](https://www.onemap.gov.sg/). [Leaflet](https://leafletjs.com/) is BSD-2-Clause.
