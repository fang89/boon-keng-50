# 50 Things To Do Around Boon Keng

A single-page, filterable guide to 50 places within a walk, a bus, or a few North East Line stops of Boon Keng, Singapore.

**Live:** https://fang89.github.io/boon-keng-50/

## What's in it

| Category | Count |
|---|---|
| Food | 15 |
| Shopping & malls | 11 |
| Outdoors | 6 |
| Heritage & old streets | 6 |
| TCG / card shops | 5 |
| Sports | 5 |
| Video game shops | 2 |

By distance: 14 within a 20-minute walk, 26 one to two stops (or one bus) away, 10 further out.

## Running it

It's one self-contained `index.html` — no build step, no dependencies, no external requests. Open the file, or serve the folder:

```
python3 -m http.server 8000
```

## Editing

Every place is one row in the `P` array near the bottom of `index.html`:

```js
[id, "Name", "Category", "walk|near|far", "Address · how far", "One-line blurb", "Optional tip"]
```

Categories must be one of `Food`, `Shopping`, `TCG`, `Games`, `Outdoors`, `Heritage`, `Sports` — each has a colour token defined in the CSS at the top. The filter chips, counts and card colours all derive from that array, so adding a row is the only edit needed.

If you change how many places sit in each distance band, update the three numbers in the ring diagram in the header to match.

## Caveats

Hawker stalls close on rotation and the older ones shut when they sell out. Shop units inside Sim Lim Square and Bugis+ move around — check the store's socials before travelling for a specific one.

Compiled August 2026. Corrections welcome via pull request.
