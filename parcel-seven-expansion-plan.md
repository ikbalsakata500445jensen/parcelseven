# PARCEL SEVEN — Expansion Plan
## 15-Region Overhaul, Story Rework, and Full Background Integration

---

## Overview

The game currently ships 8 biomes across a 960-tile world (120 tiles each). The
owner's STORY.md already specifies **15 regions** in three acts. This plan
expands the world to **15 biomes × ~107 tiles = ~1600 tiles** (LW = 1600),
integrates all 15 CraftPix background packs as named in the request, reworks the
story/characters to be authentic and non-comedic, and hardens the registry files
(CLAUDE.md, facts.json, .cursorrules) with the absolute rule that **no
development vocabulary ever enters the build**.

### What changes

| Area | Before | After |
|---|---|---|
| World width | 960 tiles, 8 biomes | 1600 tiles, 15 biomes (~107 per biome) |
| Background sets | 8 parallax sets | 15 parallax sets (1:1 with regions) |
| REGIONS array | 8 entries | 15 entries — all from STORY.md §6 |
| BIOME array | 8 lighting configs | 15 lighting configs |
| BIOME_MONSTERS | 8 pools | 15 pools |
| Story regions 9–15 | Stub / not wired | Fully wired with NPC, copy, backdrop |
| New NPCs | 5 cast members wired | Regions 4, 7, 8 get own NPCs |
| STORY.md | Current draft | Full 15-region narrative rewrite |
| facts.json | Reflects 8 biomes | Updated to reflect 15 |
| CLAUDE.md | R0–V30 present | New hard rule: no dev vocab in game |
| .cursorrules | Same as CLAUDE.md | Synced with CLAUDE.md additions |

### What does NOT change

- Single-file `index.html` (no build step)
- All 16 couriers and their stats — they are already correctly named
- All 24 enemy species — no changes to art or stats
- Physics constants (PHYS)
- The Nusagara document design system (paper, ink, stamps, typography)
- Currency, gear, crafting, achievement systems
- Deploy target: stage index.html + _headers + assets/ to /tmp/stage, then
  `npx -y wrangler pages deploy /tmp/stage --project-name=parcelseven`
- The staging dir keeps `game-2d-pxl-assets/` out of deploy

---

## Background Pack → Region Mapping

This is the authoritative assignment. One pack → one region → one `bg` folder
under `assets/bg/`. The pack ZIP names are in `game-2d-pxl-assets/`.

| # | Region (STORY.md §6) | Biome folder | CraftPix ZIP |
|---|---|---|---|
| 1 | GREENFIELD DEPOT | `greenfield` | `craftpix-net-138963-free-nature-pixel-backgrounds-for-games.zip` |
| 2 | THE LONG FOREST | `longforest` | `craftpix-net-154389-forest-and-trees-free-pixel-backgrounds.zip` |
| 3 | PORT SELAT | `portselat` | `craftpix-net-256745-free-summer-pixel-art-backgrounds.zip` |
| 4 | HARVEST DISTRICT | `harvest` | `craftpix-net-311636-free-autumn-pixel-backgrounds-for-game.zip` |
| 5 | THE COLD STORE | `coldstore` | `craftpix-net-882062-free-winter-backgrounds-pixel-art.zip` |
| 6 | RANGGA PASS | `ranggapass` | `craftpix-net-773023-free-mountain-backgrounds-pixel-art.zip` |
| 7 | NEW MERIDIAN | `meridian` | `craftpix-net-219100-free-futuristic-city-pixel-art-backgrounds.zip` |
| 8 | THE WORKS | `works` | `craftpix-net-972811-free-steampunk-cityscape-pixel-backgrounds.zip` |
| 9 | THE EXCLUSION | `exclusion` | `craftpix-net-300196-free-post-apocalypse-pixel-art-backgrounds-for-game-projects.zip` |
| 10 | THE DROWNED WARD | `drowned` | `craftpix-net-917640-free-underwater-world-pixel-art-backgrounds.zip` |
| 11 | KERING OASIS | `oasis` | `craftpix-net-546708-free-desert-oasis-pixel-art-background-pack.zip` |
| 12 | TEMPLE OF THE UNREAD | `temple` | `craftpix-net-323621-free-ancient-temple-pixel-game-backgrounds.zip` |
| 13 | THE UPPER OFFICE | `upper` | `craftpix-net-558275-free-sky-with-clouds-background-pixel-art-set.zip` |
| 14 | THE OLD GROWTH | `oldgrowth` | `craftpix-net-823949-free-nature-backgrounds-pixel-art.zip` |
| 15 | DEPARTMENT OF ENDINGS | `endings` | `craftpix-net-410031-free-planets-in-space-pixel-game-background-pack.zip` |

**Extraction rule:** Each ZIP extracts into a staging folder, the parallax PNG
layers are copied to `assets/bg/<folder>/1.png`, `2.png`, ... `N.png` (sky to
far, in depth order). Only what the game uses (PNG layers) is committed; all
Photoshop / PDF / license files stay local.

---

## Story Rework: 15 Regions, Three Acts

The existing STORY.md story is already strong. The rework task is to:
1. Expand from 8 to 15 regions — regions 1–5 get refined copy; 6–15 get full
   NPC copy + scene dialogue that sounds like the voice established in the
   existing SCENES (in-world, dry, no AI-tidy prose).
2. Rename any placeholder / unauthentic character names — the existing six cast
   members (BUNGA ARIMBI, HARUN SETIAWAN, LASMI/TIRA/WENING, IBU RANTI, TUAN
   BIMA WISESA, SRI HANDAYANI) are already correct; only NPC quest-givers that
   currently use throwaway names (TUKANG PARKIR GAIB, MBAH DUKUN ONLINE, ABANG
   BAKSO HANTU, OJOL NYASAR, TUYUL RESELLER) need authentic replacements.
3. Wire the three new Act I NPCs (regions 4, 7, 8) as proper cast members with
   portraits and two-scene dialogues.
4. The parcel's secret (spare key to a demolished house, sent by Pak Hasan) is
   not touched — it is the right ending.

### Absolute Prohibition (to be written into CLAUDE.md + facts.json)

> Words used to brief this work — "enterprise grade", "absurd", "nyeleneh",
> "AI slop", "prompt", "raw prompt" — are **not in the fiction**. They must
> never appear in the build, in any UI string, in a version string, or in
> any source comment visible to a player. This is RULE R-VOCAB-BANNED and
> applies to every subtask.

---

## Sub-Tasks

---

### SUB-TASK 1 — Registry hardening: CLAUDE.md + facts.json + .cursorrules
**Status:** [ ] pending

**Intent:** Add the hard vocabulary prohibition to all three authoritative rule
files so every future session enforces it automatically.

**Expected Outcomes:**
- `CLAUDE.md` contains a new rule (R-VOCAB-BANNED) under Section 0 that
  explicitly names "enterprise grade", "absurd", "prompt", "AI slop",
  "FREAK", "autentik" (used as dev-speak) as banned from any game string.
- `facts.json` has a `banned_game_vocabulary` array listing these terms.
- `.cursorrules` is updated to match CLAUDE.md identically.

**Todo List:**
1. Open CLAUDE.md and insert R-VOCAB-BANNED under the R0 block.
2. Open facts.json and add `"banned_game_vocabulary"` key with the banned list.
3. Open .cursorrules and mirror the same new rule.

**Relevant Context:**
- CLAUDE.md exists at root, Section 0 is the owner's absolute rules.
- facts.json exists at root, currently has a `"design_system"."banned"` array.
- .cursorrules exists at root, mirrors CLAUDE.md for Cursor editor.

---

### SUB-TASK 2 — STORY.md full 15-region rewrite
**Status:** [ ] pending

**Intent:** Rewrite STORY.md to be the complete narrative bible for all 15
regions. Authentic, dry, emotionally coherent. No comedy names, no
developer vocabulary. Voices must be distinguishable. The source document that
every future dialogue derives from.

**Expected Outcomes:**
- §6 now lists all 15 regions with subtitle, biome folder, and NPC owner.
- §5 (Cast) expanded: the five quest-giver NPCs get authentic Nusagara names,
  brief bios, want/wrong/voice entries like the six main cast.
- §10 (Not built yet) updated to list only genuinely unbuilt features.
- §2 (Theme) and §4 (Structure) refined to address the 3-act × 15-region scope.

**Todo List:**
1. Draft authentic replacement names for the five NPC quest-givers and add them
   to §5.
2. Expand §6 from 8 to 15 rows — include subtitle (dry, not explained), biome
   folder, and which cast member appears there.
3. Write 1-paragraph "the scene" notes for regions 9–15.
4. Update §10 to reflect current build state accurately.
5. Write the document to disk.

**Relevant Context:**
- Current §5 has six main cast; the five NPC quest-givers currently use joke
  names (TUKANG PARKIR GAIB etc.) that need replacing.
- The region 9–15 biomes already have `assets/bg/` folders (exclusion,
  drowned, oasis, temple, upper, oldgrowth, endings) so art assets exist.
- SCENES in index.html derives from STORY.md; keep voices consistent.

---

### SUB-TASK 3 — Asset extraction: 15 background packs → assets/bg/
**Status:** [ ] pending

**Intent:** Extract the 15 CraftPix background ZIPs and populate
`assets/bg/<folder>/1.png`…`N.png` for every region. The extraction is
mechanical and does not touch index.html.

**Expected Outcomes:**
- Every folder in the pack → region mapping table above contains at least
  3 PNG files numbered `1.png`, `2.png`, `3.png` (sky/far/mid order).
- No Photoshop, PDF, or license file is added to `assets/bg/`.
- Folders that already have PNGs (greenfield, longforest, portselat, etc.)
  are verified to have the correct pack's layers, not stale placeholders.
- `assets/CREDITS.md` is updated with the 15 pack names.

**Todo List:**
1. For each of the 15 ZIPs: unzip into a temp folder, identify the parallax
   PNG layers (usually named `1.png`/`2.png` or `Layer_0001`/`Layer_0002`),
   rename to canonical `1.png`…`N.png`, copy into `assets/bg/<folder>/`.
2. Verify each folder has ≥3 layers.
3. Update `assets/CREDITS.md`.

**Relevant Context:**
- ZIPs are in `game-2d-pxl-assets/` (see mapping table above for exact names).
- Existing folders: `greenfield`, `cloudport`, `driedsea`, `neonbazaar`,
  `ashfall`, `frozenqueue`, `termstemple`, `endings` — some may already have
  correct layers; check before overwriting.
- `craftpix-net-514191-4-free-seamless-nature-pixel-backgrounds.zip` is a
  second nature pack — do not confuse with pack #1 for greenfield.

---

### SUB-TASK 4 — World expansion: 8 biomes → 15 biomes in index.html
**Status:** [ ] pending

**Intent:** Expand the engine from 8 to 15 biomes. Changes `LW`, `biomeAt()`,
`BIOME[]`, `BIOME_MONSTERS[]`, `REGIONS[]`, `REGION_BG_COUNT`, and
`MINIMAP_COLS`. All arithmetic must stay correct.

**Expected Outcomes:**
- `LW = 1605` (15 × 107 tiles).
- `biomeAt(x)` returns 0–14 correctly.
- `BIOME` array has 15 entries with authentic lighting configs tuned to each
  background pack's colour palette.
- `REGIONS` array has 15 entries matching STORY.md §6 (names + bg folder keys).
- `BIOME_MONSTERS` has 15 pools — new pools for regions 9–15 use monsters
  already in the game; no new monster species needed.
- `REGION_BG_COUNT` covers all 15 biome folder names.
- `MINIMAP_COLS` has 15 triplets.
- `facts.json` `world.biomes` updated to 15.
- 0 console errors, 0 failed assets after expansion.

**Todo List:**
1. Update `LW` constant (find and replace).
2. Update `biomeAt()` to clamp 0–14.
3. Extend `BIOME[]` with 7 new entries (regions 9–15) with correct sky/rock/
   torch colours derived from the CraftPix pack palettes.
4. Extend `REGIONS[]` with 7 new entries (regions 9–15) from STORY.md §6,
   with correct `bg` key.
5. Extend `BIOME_MONSTERS[]` with 7 new pools.
6. Extend `REGION_BG_COUNT` with 7 new entries.
7. Extend `MINIMAP_COLS` with 7 new triplets.
8. Update `facts.json` world.biomes, world.tiles, world.tiles_per_biome.
9. Run syntax check (V4 command) and verify 0 errors.

**Relevant Context:**
- `BIOME[]` starts at index.html line 1651.
- `REGIONS[]` starts at index.html line 5179.
- `BIOME_MONSTERS` is an array of arrays used by level generation.
- `MINIMAP_COLS` lives near the minimap rendering code.
- `LW` is set near the top of the script, referenced throughout world gen.
- IMPORTANT: `biomeAt(x) = floor(x / (LW/15))` — must recalculate the
  divisor from `LW` dynamically or use `Math.floor(x / 107)` for 107 tiles
  per biome.

---

### SUB-TASK 5 — NPC replacement: authentic names + new region NPCs
**Status:** [x] done

**Intent:** Replace the five joke-name NPC quest-givers with authentic
Nusagaran names and add three new NPC cast entries for regions 4, 7, 8
(HARVEST DISTRICT, NEW MERIDIAN, THE WORKS) which currently have no NPC.

**Expected Outcomes:**
- `NPC_ART` map updated with new NPC IDs.
- `CAST` object updated — old joke IDs (parkir, mbah, baksom, ojol, tuyul)
  replaced with new authentic IDs; names are Nusagaran (not parodies of any
  real person).
- Three new `CAST` entries for regions 4, 7, 8 with art assignments.
- All SCENES referencing old NPC IDs updated to new IDs.
- All quest definitions referencing old NPC IDs updated.
- `STORY.md` §5 matches (done in sub-task 2, cross-verified here).

**Replacement naming rule:** Names must follow the same register as BUNGA
ARIMBI, HARUN SETIAWAN, SRI HANDAYANI — Nusagaran given + family name, no
pun, no abbreviation, no archaic joke role in the name itself.

**Todo List:**
1. Define 5 replacement NPC names (see naming rule above).
2. Define 3 new NPC names for regions 4, 7, 8 with roles consistent with
   STORY.md (Harvest District is about produce-wage economy; New Meridian is
   the city rebuilt wrong; The Works is the factory that produces parts for
   itself).
3. Update `NPC_ART` and `CAST` in index.html.
4. Grep all SCENES and quest tables for old NPC IDs and update.
5. Syntax-check the file.

**Relevant Context:**
- `CAST` object at index.html line 5215.
- `NPC_ART` at index.html line 5214.
- `SCENES` object begins at index.html line 5234.
- Quest definitions reference NPC IDs via `npc:` field.

---

### SUB-TASK 6 — New dialogue scenes: regions 9–15
**Status:** [x] done

**Intent:** Wire proper two-scene NPC dialogue for every region that currently
has none or stub copy. Regions 9–15 get an `r8` through `r14` scene in
`SCENES`. Writing follows STORY.md rules: voices differ, every line has a turn,
no moral stated, emotion undercut.

**Expected Outcomes:**
- `SCENES` has 15 region-entry scenes (open + r0…r14) covering all 15 regions.
- Each scene has 4–7 lines.
- Each NPC voice is distinguishable from the others.
- All copy is in both EN + ID (no missing `id:` fields).
- No scene references any banned vocabulary.

**Todo List:**
1. Write scenes for regions 9–14 (THE EXCLUSION through THE OLD GROWTH) as
   per STORY.md §6 region notes — one NPC per region, each wanting something
   specific and wrong about it.
2. Write the region 15 ending scene (DEPARTMENT OF ENDINGS — Counter 8 is
   closed — the signature moment) to match STORY.md §4 Act III.
3. Insert scenes into `SCENES` object in index.html.
4. Wire each scene to trigger when entering the corresponding region (the
   existing `regionEnter()` trigger logic already drives this).
5. Syntax-check.

**Relevant Context:**
- Scene trigger at index.html ~line 7515 (`swapRegionBackdrop` is called on
  region enter; `openScene` fires there or nearby).
- Existing scenes `open`, `r0`…`r7` established the voice register.
- The ending scene must be playable straight — the one exception to the
  "emotion undercut" rule (STORY.md §8 final line).

---

### SUB-TASK 7 — Background rendering: extend to 15 parallax sets
**Status:** [x] done

**Intent:** The current rendering system uses 2 of up to 5 layers per set.
Expand `swapRegionBackdrop` to correctly handle all 15 sets, and ensure the
new biomes have reasonable repeat/parallax values calibrated to their art.

**Expected Outcomes:**
- `REGION_BG_COUNT` covers all 15 folders with correct layer counts.
- `swapRegionBackdrop(b)` resolves without errors for b=0…14.
- All 15 backgrounds visible in-game when entering the correct region.
- No tiling artefact that breaks immersion (verify visually, not just by
  0-error count).

**Todo List:**
1. Confirm layer counts for each of the 15 extracted sets.
2. Update `REGION_BG_COUNT` map.
3. Tune `rep` (tiling repeat) per biome if needed — sky at 3.0×, far at 2.2×
   is the safe default; adjust for art that tiles badly.
4. Deploy and open the deployed URL; walk through all 15 regions visually.

**Relevant Context:**
- `swapRegionBackdrop` at index.html line 6074.
- `loadRegionBackdrops` at index.html line 6101.
- Current `rep` logic at line 6094.

---

### SUB-TASK 8 — Miniboss placement recalibration
**Status:** [x] done

**Intent:** With LW expanding from 960 to 1605, the two minibosses (minotaur
@ x=350, demon @ x=620) are now both in the first 40% of the world, which
compresses Act I. Recalibrate to mid-Act-II and late-Act-II placement.

**Expected Outcomes:**
- Minotaur placed at approximately x = 700 (region 7, NEW MERIDIAN — the
  city that was rebuilt wrong; a miniboss here is structurally correct for
  Act II turn).
- Demon placed at approximately x = 1100 (region 11, KERING OASIS — the
  collector's last stand before the temple).
- `facts.json` `world.minibosses` updated with new x values.
- Both miniboss encounters visually verified at new positions.

**Todo List:**
1. Update `SPAWN.push({sp:"minotaur"...})` x value to ~700.
2. Update `SPAWN.push({sp:"demon"...})` x value to ~1100.
3. Update `facts.json` miniboss coordinates.
4. Verify in-game (walk to each position, confirm trigger fires, no regression
   in encounter logic).

**Relevant Context:**
- Miniboss spawn definitions are in level generation near `SPAWN.props.push`.
- Current coordinates: minotaur x=350, demon x=620 (from facts.json line 97).

---

### SUB-TASK 9 — Verification and deploy
**Status:** [x] done

**Intent:** Full verification pass per CLAUDE.md rules before deploy. This is
not optional — C1/C2 apply.

**Expected Outcomes:**
- V4 syntax check: 0 errors.
- Walk the full 15-region world: no missing backgrounds, no enemy feet
  buried, no NPC scene that never fires, no banned vocabulary in any UI string.
- All 15 region banners render correctly (V29: every glyph in nusagara.ttf).
- Phone HUD ≤ 14.7% idle, ≤ 25.9% with panel open.
- `facts.json` updated with final line count, biome count, and verified status.
- Deploy: stage + `npx -y wrangler pages deploy /tmp/stage --project-name=parcelseven`.
- Open deployed URL in a fresh tab — no 404, no console error.

**Todo List:**
1. Run V4 syntax check.
2. Walk the world in-game (all 15 regions).
3. Check region banners for font fallback (V29).
4. Check phone HUD coverage.
5. Update facts.json.
6. Deploy and verify deployed URL.
7. Report exactly what was checked and what was not.

---

## Implementation Order

```
SUB-TASK 1 (registry hardening)
    → SUB-TASK 2 (story rewrite — source of truth for all copy)
        → SUB-TASK 3 (asset extraction — backgrounds must exist before wiring)
            → SUB-TASK 4 (world expansion — engine changes)
                → SUB-TASK 5 (NPC names)
                    → SUB-TASK 6 (dialogue scenes)
                        → SUB-TASK 7 (background rendering)
                            → SUB-TASK 8 (miniboss placement)
                                → SUB-TASK 9 (verify + deploy)
```

Each sub-task is designed to be independently reviewable. Do not begin the
next sub-task until the current one passes its own Expected Outcomes check.

---

## Critical Constraints (apply to every sub-task)

1. **Single file**: `index.html` stays single-file. No imports, no modules.
2. **No banned vocabulary in the build**: "enterprise grade", "absurd",
   "prompt", "AI slop", "FREAK", "autentik" (as dev-speak) must not appear
   in any string the player sees or in any source comment.
3. **V4 after every edit**: `python3 -c "..."  && node --check /tmp/game.js`
4. **V19 — A person is the scale**: nothing changes hero/enemy sizing.
5. **V15 — Typography**: type only at 14.7px multiples. No new typeface.
6. **V27 — One WebGL context**: no second renderer added.
7. **R2 — No hand-drawn art**: all new NPC portraits come from extracted packs.
8. **R5 — Always both EN + ID**: every new string has an `id:` twin.
9. **Assets/CREDITS.md** must stay accurate for all 15 packs added.
