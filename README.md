# Things To Do Around Boon Keng

A mapped, filterable guide to 64 places within a walk, a bus, or a few North East Line stops of Boon Keng, Singapore.

**Live:** https://fang89.github.io/boon-keng-50/

Every place is plotted from its real address. The triangle on the map is home; the rings around it are 500 m, 1 km, 2 km and 3 km, so you can see at a glance what is genuinely walkable.

The radius filter is cumulative and matches those rings — picking **Under 1 km** shows everything within a kilometre and draws that ring solid. Category chips stack on top of it. Clicking a card flies the map to its pin, and a **Recenter** button appears once home scrolls out of view.

## What's in it

| Category | Count |
|---|---|
| Food | 17 |
| Shopping & malls | 11 |
| TCG / card shops | 7 |
| Games — board game cafés, arcades, game shops | 7 |
| Outdoors | 7 |
| Gyms | 6 |
| Drinks — coffee & bars | 5 |
| Courts & Pools | 4 |

By radius: **10** under 500 m, **23** under 1 km, **47** under 2 km, **59** under 3 km. Nearest is Dungeon Performance at 187 m. The five beyond 3 km are Bidadari Park, Qisahn, Funan, Games Haven and NEX.

### Open late

`Open late` is a cross-cutting tag rather than a category — it marks the seven places open **past midnight or around the clock**, spanning food, shopping and gyms. It is the filter to reach for at 2am, and it combines with everything else.

## How the distances work

Coordinates come from [OneMap](https://www.onemap.gov.sg/), Singapore's national address database — not from hand-placed pins. Distances are straight-line (haversine) from the home marker, so real walking is somewhat longer. Where a shop sits inside a larger building, the pin is the building: Sim Lim Square, Bugis+, Aperia and the hawker centres each hold several entries. Markers that share an address are fanned out about 24 m so all of them stay clickable; zoom in, or click the card, and they separate.

Radius bands are read straight off the computed metres rather than assigned by hand, so the filter, the rings and the list cannot drift out of sync.

Three candidate venues were cut during the last pass because their geocode resolved to the wrong tenant and the facts could not be confirmed — better a shorter list than a pin that sends you to the wrong door.

## Running it

No build step and no external JavaScript — Leaflet is vendored into `vendor/`. Map tiles are the only network call. Open `index.html`, or serve the folder:

```
python3 -m http.server 8000
```

## Editing

Every place is one row in the `P` array near the bottom of `index.html`:

```js
["Name", "Category", metres, lat, lng, "Address", "One-line blurb", "Optional tip", lateFlag]
```

Categories must be one of `Food`, `Drinks`, `Shopping`, `TCG`, `Games`, `Gyms`, `Courts & Pools`, `Outdoors`; each has a colour token in the CSS at the top of the file, used for both the card accent and the map marker. `lateFlag` is `1` for open-past-midnight, otherwise `0`. `metres` is the straight-line distance from home and is what the radius filter reads.

Chip counts, the headline number and the radius counts are all computed from the array, so adding a row is the only edit needed.

To add a place, get its coordinates from OneMap:

```
curl "https://www.onemap.gov.sg/api/common/elastic/search?searchVal=29+BENDEMEER+ROAD&returnGeom=Y&getAddrDetails=Y&pageNum=1"
```

Check that the `ADDRESS` in the response actually matches the venue — OneMap will happily return a co-tenant, or a historic-site marker, at the same coordinates. `data/coords.json` holds the geocoder output for everything currently on the map, including which query matched.

## Caveats

Hawker stalls close on rotation and the older ones shut when they sell out. Shop units inside Sim Lim Square and Bugis+ move around — check the store's socials before travelling for a specific one. Opening hours, especially the late-night ones, change without notice.

Compiled August 2026. Corrections welcome via pull request.

## Credits

Map tiles © [CARTO](https://carto.com/attributions), data © [OpenStreetMap](https://www.openstreetmap.org/copyright) contributors. Geocoding by [OneMap](https://www.onemap.gov.sg/). [Leaflet](https://leafletjs.com/) is BSD-2-Clause.
