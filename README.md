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

Touch devices (no fine pointer) get a different control set:

- **One thumbstick** — drag to move; push up to jump; keep it up and the jump
  reaches full height; hold a diagonal up for a running jump with the slow-fall;
  pull down for the jelly slam.
- **Tap anywhere on the picture** to spit a glob. On menus the same tap works as
  Enter, so every card can be pushed through.
- **Pause** sits in the band above the picture, nowhere a thumb rests.

In **portrait** the picture takes the full screen width and the leftover height
becomes drawn filler: a faint `S L O P I O` wordmark over the same drifting-chip
motif the title screen uses above, and a control deck holding the stick below.
Nothing the thumb touches is ever on top of the game. In **landscape** the picture
fills the height and the stick sits in the letterbox margin at the left, the pause
button in the margin at the right.

While you are actually playing there is nothing on screen but the game: the source
link and the pause control only exist on the title and about screens.

The stick and taps feed the same key state the keyboard does, so the game logic is
unchanged. Add `#touch` to the URL on a desktop to force the phone layout — handy
when testing, e.g. `index.html#touch`.

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

Inside `index.html` the body is a phone-shaped stack: `#deck` holds `#bandTop`,
`#wrap` (which holds `#game` and `#ui`), `#bandBot`, and `#pad` with the
thumbstick and the pause button. Outside it there is only `#linkbar` (menus only)
and `#err`, where a boot failure prints instead of a black screen.

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
