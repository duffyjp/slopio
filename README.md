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
| C | About card — credits, license, source links (from the title screen) |
| G | On the about card: open the repository in a browser tab |
| Enter | Confirm / start |

You can only have **three globs in the air at once** — gel pickups load special
ammo for a short while instead. Squishing an enemy often leaves a bead of its gel
behind, which is how you restock away from the fixed pickups.

### On a phone or tablet

On coarse-pointer devices (anything with no mouse hover) the game puts an
on-screen pad in the letterbox around the picture: `◀ ▶` move, `▲` jump, `▼` jelly
slam, `◎` spit, `II` pause, `START` to confirm. Tapping the picture itself works as
Enter, so every card can be pushed through with one thumb. A small
`github.com/duffyjp/slopio · MIT` link sits at the bottom, since there is no `G`
key to press there.

Landscape is the better way to play; in portrait the picture is letterboxed down
to the screen width rather than cropped. The pads feed the same key state as the
keyboard, so nothing else about the game changes.

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

Then visit `http://localhost:8000/`. Keyboard or touch, your choice.

## How it is drawn

The game keeps a 480×270 logical pixel buffer and blits it up with
nearest-neighbour scaling, which is what makes the sprites and tiles look like
pixel art. Menu and card text used to go through that same buffer, which made the
words mushy at 3× or 4×, so text now goes to a second canvas stacked exactly over
the first one and sized in **device** pixels (`#game`, `#ui`, both inside `#wrap`).
Sprites drawn onto menus still blit from their 1× art, so they keep their chunky
edges while the type stays sharp.

The world, the HUD and the ending cutscene still render entirely on the pixel
buffer — the crisp layer only carries the title screen, the about card, the level
intro and clear cards, the pause and game-over cards, and the credits.

## Repo layout

```
index.html   the whole game — one file, one <script>, four levels
README.md    this file
LICENSE      MIT
```

Inside `index.html` the body is just three things: `#wrap` holding `#game` and
`#ui`, `#pad` with the touch buttons, and `#err` where a boot failure prints
instead of a black screen.

The single file is assembled from thirteen parts (`p01_head.js` through
`p13_main.js`), marked inline with `/* ==== pNN_name.js ==== */` comments so the
sections stay navigable.

## License

MIT — see [LICENSE](LICENSE).

Attribution lives in the game too: a header comment at the top of `index.html`,
a small credit line on the title screen, the pause overlay and the end-of-game
credits, plus an about card on the title screen (`C`) that lists the play URL, the
repository, and the license. The author, year and URLs are set once as constants
(`AUTHOR`, `YEAR`, `LICENSE`, `REPO`, `REPO_URL`, `PLAY_URL`) near the top of the
script, so they are easy to change in one place.
