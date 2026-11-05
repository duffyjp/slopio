# SLOPIO

**a gelatinous cube in three grids**

A 2.5D pixel-art platformer that lives entirely in one HTML file. No build step,
no dependencies, no assets to load — all art is drawn to offscreen canvases at
page load and all sound is synthesized with the Web Audio API.

**Play it:** <https://duffyjp.github.io/slopio/>

You are Slopio, a squishy cube on the run through three computer-themed grids and
whatever is waiting at the end of them.

## Controls

| Key | Action |
| --- | --- |
| Arrows / WASD | Move |
| Space (hold) | Jump — hold longer to fly higher |
| Down | Jelly slam (stomp enemies, break brittle floors and ice, freeze liquid) |
| J / X / K | Spit a glob (it arcs as it flies) |
| P | Pause |
| M | Mute |
| R | Restart the level |
| Enter | Confirm / start |

You can only have **three globs in the air at once** — gel pickups load special
ammo for a short while instead. Squishing an enemy often leaves a bead of its gel
behind, which is how you restock away from the fixed pickups.

## The grids

1. **The Marsh Grid** — dusk wetland, floppy-disk platforms, cable vines.
2. **Pixel Forge** — foundry: conveyors, piston stomp gaps, rivet armour,
   molten channels, and a Charge Gel circuit.
3. **Frostbyte Cathedral** — frozen server hall: slippery and shatterable ice,
   fans, and three hidden ice bells.
4. **The Heat Sink** — DIMMOLITH, online. Ride the floor jets up to the fins,
   pelt him, drop back down; eight clean hits jam his armour.

## Gel

| Gel | Loaded by | What it does |
| --- | --- | --- |
| Goo | always available | Default arcing glob |
| Ember | `G` pickups, the odd enemy bead | Extra-damage fireball |
| Frost | `F` pickups, the odd enemy bead | Globs freeze liquid into platforms; slamming does the same under you |
| Charge | `E` pickups, the odd enemy bead | You walk through the electrified bits, and the glob flies flat and fast and homes onto metal enemies |
| Heavy | `V` pickups, the odd enemy bead | Enough weight to squash armoured enemies a slam alone will not |

## Goals

- **100 shards** are hidden across the whole game. Collect all of them and you
  earn **★ Overclock**.
- Slam through brittle floors to find hidden vaults, and ring all three ice
  bells in the Frostbyte Cathedral.
- Your best clear time and the Overclock badge are saved in `localStorage`.

## Running it

Open `index.html` in a browser, or serve the folder:

```
python -m http.server 8000
```

Then visit `http://localhost:8000/`. Keyboard required; the game renders at a
480×270 logical resolution and scales up with crisp pixel edges.

## Repo layout

```
index.html   the whole game — one file, one <script>, four levels
README.md    this file
LICENSE      MIT
```

The single file is assembled from thirteen parts (`p01_head.js` through
`p13_main.js`), marked inline with `/* ==== pNN_name.js ==== */` comments so the
sections stay navigable.

## License

MIT — see [LICENSE](LICENSE).
