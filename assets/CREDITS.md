# Third-party assets

Everything shipped in this folder is **CC0 1.0 (public domain)** unless noted —
free for commercial use, no attribution legally required. Credit is given here
anyway because it is the decent thing to do.

## Sprites — `assets/sprites/` (Pixel Frog, CC0 1.0)

**"Pixel Adventure"** by **Pixel Frog**
License: CC0 1.0 Universal — https://creativecommons.org/publicdomain/zero/1.0/
Source: https://pixelfrog-assets.itch.io/pixel-adventure-1 and
https://pixelfrog-assets.itch.io/pixel-adventure-2

Used: 7 heroes (`ninja_frog`, `mask_dude`, `pink_man`, `virtual_guy`,
`ksatria`, `ninja_bayangan`, `paladin_kopi`) and 24 enemies (slime → robot, incl. minotaur/demon/zombie/
soldier). Strips are composited into atlases at load in `index.html`; if a PNG
is missing the game falls back to procedural sprites so nothing renders blank.

## Item icons — `assets/icons/items/` (original, generated for this project)

18 Indonesian absurd icons at 24x24 (batu_akik, cendol, esteh, golok_ida,
gorengan, helm_ojol, indomie, jamutolakmati, kerupuk, kopijoss, obatexpired,
panci_wajan, pedang_laser_kw, rendang, sandal_swallow, sapu_lidi, seblak,
whetstone). These are drawn procedurally for this project, not taken from any
pack. Loaded at boot with a `buildItemIcon` fallback if a file is absent.

## Extra art — `assets/ext/` (CraftPix free packs — NOT CC0)

Shipped and used as in-game art: `loot/` (40 loot icons), `weapons/`
(32x32 weapon icons), `portraits/` (medieval NPC avatars), `fx/`
(explosion sprites), `fairy/` (fairy avatar icons), `clouds/`.

License: CraftPix Freebies License — https://craftpix.net/file-licenses/
Terms that matter here, quoted:
  * "You can sell and distribute games with our assets."
  * "an app that uses the art as part of the play of the game is fine."
  * "You can NOT resell the art source files (PNG, JPG, EPS, Adobe
    Illustrator, etc) or slightly modified version of the art."
  * "No attribution or link back to this site is required, however any
    credit will be highly appreciated."

Using them as gameplay art inside this game is the permitted use. Credit is
given here voluntarily. Do NOT repackage these PNGs as a downloadable asset
set — that is the one thing the licence forbids. The raw `.zip` packs in
`game-2d-pxl-assets/` are excluded from deploys for exactly this reason.

## Music — `assets/music/`

**"5 Action Chiptunes"** by **Juhani Junkala** (subspaceaudio)
License: CC0 1.0 Universal — https://creativecommons.org/publicdomain/zero/1.0/
Source: https://opengameart.org/content/5-chiptunes-action

| File in this repo | Original | Used for |
|---|---|---|
| `music/title.m4a`  | `title screen.mp3` | Title screen |
| `music/level1.m4a` | `level1.mp3` | Biome 1 — Emerald Ruins |
| `music/level2.m4a` | `level2.mp3` | Biome 2 — Crystal Caves |
| `music/level3.m4a` | `level3.mp3` | Biome 3 — Magma Fortress |
| `music/ending.m4a` | `ending.mp3` | Victory screen |

**"Spooky Dungeon"** by **Memoraphile @ You're Perfect Studio**
Multi-licensed by the author as CC-BY 4.0 / OGA-BY 3.0 / **CC0** — used here under CC0.
Source: https://opengameart.org/content/spooky-dungeon
Used as `music/level4.m4a` for Biome 4 — Void Sanctum (biomes 5-8 reuse
tracks 1-4 via `SND.setBiome(Math.min(b,3))`).

Re-encoded from the original 160 kbps MP3 to 96 kbps AAC (`afconvert -f m4af -d aac
-b 96000 -s 3`) to cut total payload from 7.5 MB to 4.9 MB. No other modification.

## UI icons — inlined in `index.html`

**Lucide** — https://lucide.dev
License: ISC (permissive; the licence text below covers the icon geometry embedded
in `index.html`). Lucide is a fork of Feather Icons (MIT, © Cole Bemis).

```
ISC License

Copyright (c) for portions of Lucide are held by Cole Bemis 2013-2022 as part of
Feather (MIT). All other copyright (c) for Lucide are held by Lucide Contributors
2022.

Permission to use, copy, modify, and/or distribute this software for any purpose
with or without fee is hereby granted, provided that the above copyright notice
and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH
REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND
FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT, INDIRECT,
OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE,
DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS
ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS
SOFTWARE.
```

## Dev-only reference — `game-2d-pxl-assets/` (NOT shipped)

~140 CraftPix free-pack zips used as a design reference for systems (tilesets,
backgrounds, loot/food/weapon icons, slash/flame/water/explosion FX, NPC
portraits, extra hero/enemy sheets). This folder is excluded from git and
deploys (see `.gitignore`; deploys ship a staging dir with index.html +
assets/ only) and the game boots with
zero external assets. If extracted under `assets/ext/<category>/`, the EXT
loader in `index.html` picks them up automatically. Check each pack's own
licence before redistributing extracted files.


## Region backdrops — `assets/bg/` (CraftPix free packs)

Fifteen parallax sets, one per region of Nusagara. Only the two DISTANT plates
are used per region — the near layer stays procedural, because pack foregrounds
are drawn for a 576px viewport and render enormous against this game's
~30-world-unit view.

| Folder | CraftPix pack |
|---|---|
| `greenfield/` | Free Nature Pixel Backgrounds for Games (craftpix-net-138963) |
| `longforest/` | Forest and Trees Free Pixel Backgrounds (craftpix-net-154389) |
| `portselat/` | Free Summer Pixel Art Backgrounds (craftpix-net-256745) |
| `harvest/` | Free Autumn Pixel Backgrounds for Game (craftpix-net-311636) |
| `coldstore/` | Free Winter Backgrounds Pixel Art (craftpix-net-882062) |
| `ranggapass/` | Free Mountain Backgrounds Pixel Art (craftpix-net-773023) |
| `meridian/` | Free Futuristic City Pixel Art Backgrounds (craftpix-net-219100) |
| `works/` | Free Steampunk Cityscape Pixel Backgrounds (craftpix-net-972811) |
| `exclusion/` | Free Post-Apocalypse Pixel Art Backgrounds (craftpix-net-300196) |
| `drowned/` | Free Underwater World Pixel Art Backgrounds (craftpix-net-917640) |
| `oasis/` | Free Desert Oasis Pixel Art Background Pack (craftpix-net-546708) |
| `temple/` | Free Ancient Temple Pixel Game Backgrounds (craftpix-net-323621) |
| `upper/` | Free Sky With Clouds Background Pixel Art Set (craftpix-net-558275) |
| `oldgrowth/` | Free Nature Backgrounds Pixel Art (craftpix-net-823949) |
| `endings/` | Free Planets in Space Pixel Game Background Pack (craftpix-net-410031) |
| `relay/` | Free City Backgrounds Pixel Art (craftpix-net-322807) |
| `tide/` | Ocean and Clouds Free Pixel Art Backgrounds (craftpix-net-724983) |
| `margin/` | 4 Free Seamless Nature Pixel Backgrounds (craftpix-net-514191) |
| `field/` | Free Pixel Art Fantasy 2D Battlegrounds, set 1 Bright (craftpix-net-776320) |
| `annex/` | Free Pixel Art Fantasy 2D Battlegrounds, set 2 Bright (craftpix-net-776320) |

Two plates per new folder (sky + far motif — the only indices the loader
displays). Seven unreferenced backdrop folders (`ashfall/`, `cloudport/`,
`depot/`, `driedsea/`, `frozenqueue/`, `neonbazaar/`, `termstemple/`) were
removed with the 20-region upgrade; they were never loaded by any region.

All packs: CraftPix Freebies License — use in a game is permitted, reselling
the art files is not. See `assets/ext/` section above for the full licence text.

## Extra heroes — `assets/sprites/heroes/` (CraftPix free packs)

`enchantress` comes from the Fantasy Chibi Female pack; `senior_one`,
`senior_two`, `senior_three` from the Schoolgirls Anime Character pack;
`satyr_band` from the Satyr pack; `tengu_intern` from the Yokai pack;
`samurai` from the Shinobi pack (Samurai); `vampir` from the Vampire pack
(Converted Vampire); `robot_rusak` from the City Man pack (City Men 1, a road
works crew member — the folder keeps its old name so saved games keep working).
All 128x128 cells, drawn at 2.9x world scale. The other seven heroes remain
Pixel Frog CC0 (see above).

Same CraftPix Freebies License as `assets/ext/` above: use in a game is
permitted, reselling the art files is not.


## Gate bosses — `assets/sprites/enemies/{dragon,lizard,medusa,jinn,sdragon,karasu,kitsune,yamabushi}/` (CraftPix free packs — NOT CC0)

`dragon`, `lizard`, `medusa`, `jinn`, `sdragon` from **Free RPG Monster
Sprites Pixel Art** (craftpix-561178); `karasu`, `kitsune`, `yamabushi` from
**Free Yokai Pixel Art Character Sprites** (craftpix-net-605776 — the same pack
`tengu_intern` comes from). Full 128px cells, stitched from the pack
strips for this game (bosses render big, so they ship big). Twenty-one boss
postings (19 gate seals + 2 arenas) share these eight sets.

`ghost` from **Free Ghost Pixel Art Sprite Sheets** (craftpix-net-872297,
Yurei idle, downscaled to 64px cells). The old 44px ghost sheet never made it
into the repo, so every ghost rendered as a fallback slime; fixed with the
20-region upgrade.

`poop` / `poopking`: the Pixel Frog slime's own pixels above, barnyard-shifted
to brown in `assets/sprites/enemies/poop/idle_run.png` (same cells, new smell).
Same CC0 source, modified for in-game use, which the licence permits.

Same CraftPix Freebies License as `assets/ext/` above: use in a game is
permitted, reselling the art files is not.

## Dialogue portraits — `assets/portraits/` (CraftPix free packs)

`npc1`-`npc4`: Medieval NPC Avatars for Dialogue — six emotions each
(talk / calm / smile / sadness / aggression / special), driving the RPG scene
player. `senior1`-`senior3`: emotion portraits cropped from the Schoolgirls
Anime pack's own animation sheets (Dialogue/Idle/Walk/Book/Attack/Protection).

## Schoolgirl heroes — `assets/sprites/heroes/senior_*`

Playable skins from the Schoolgirls Anime Character pack (128x128 cells).

## Typeface — `assets/fonts/nusagara.ttf` (extended from the pack's own font)

**Source:** `Planes_ValMore.ttf`, which ships inside the CraftPix "Tiny Pixel
Hero Sprites with Melee Attacks" pack. The original is kept alongside it at
`assets/fonts/Planes_ValMore.ttf`, unmodified.

The whole interface is set in this face — labels, values, dialogue, headings —
so the UI speaks in the same voice as the sprites instead of an imported
webfont. Doing that honestly required extending it: the original has no
apostrophe, so English contractions ("it's", "won't") rendered as gaps.

**Glyphs added** for this game, drawn on the font's own 68/1000em pixel grid so
they match its weight and rhythm exactly:

| Codepoint | Glyph | Why it was needed |
|---|---|---|
| U+0027 / U+2019 | `'` `'` | every English contraction in the dialogue |
| U+00B7 | `·` | the separator used across the HUD |
| U+00D7 | `×` | "jump ×2" in the controls legend |
| U+2191 | `↑` | the jump key in the controls legend |
| U+00B0 | `°` | degrees |
| U+0026 | `&` | ampersand |

Its pixel is 68/1000 em, so all UI type is set at **multiples of 14.7px**
(1 design pixel = 1 CSS pixel) and lands on whole pixels instead of smearing.

Modifying the art for use inside the game is permitted by the CraftPix
Freebies License; **redistributing the font file itself as an asset is not**,
and it is not offered for download anywhere in this project.

## Everything else

Tiles, backgrounds, particles, boss, coins/gems/chests/torches/totems/portals
and sound effects are generated procedurally in `index.html`.
