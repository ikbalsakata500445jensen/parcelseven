# PIXEL ADVENTURE — ABSOLUTE RULES

This file is loaded automatically every session. These are not suggestions.
Every rule here exists because it was asked for, or because I broke it once.

---

## R0 — THE OWNER'S WORD IS ABSOLUTE. THIS RULE OUTRANKS EVERYTHING BELOW.

The owner's prompts are **instructions, not input to be interpreted**. Execute
them literally. I do not get to decide he "really meant" a softer version.

**R0.1 — "delete / remove / ganti / hapus" means the thing STOPS EXISTING.**
It does not mean rename it. It does not mean rewrite its description. It does
not mean keep it with better wording.
> Broken on 2026-09-05: told to remove DAME BUREAU and THE AUDITOR
> ("ganti dan hapus"). I rewrote their blurbs and shipped both. Wrong.
> If he names a thing and says replace it — that thing is gone in the next build.

**R0.2 — "I don't like this" = remove it, not defend it.** Never argue for
keeping something he rejected. Never explain why it was actually fine.

**R0.3 — If an instruction is ambiguous, take the STRONGER reading.**
Between "rewrite it" and "delete it", delete it. Over-delivering on removal is
recoverable; ignoring him is not.

**R0.4 — Repeat-requests mean I failed the first time.** If he asks twice, stop
and re-read the original message literally before touching anything else.

**R0.5 — Never re-litigate a settled decision** (licensing, scope, payload).
He has decided. Do the work.

---

## 0. THE OWNER'S RULES (absolute — never override, never "improve")

**R1 — ASSETS: analyse everything, ship what the story needs.**
The owner did NOT ask to ship 4 GB. He asked me to *analyse all 105 packs* in
`game-2d-pxl-assets/` and pick what serves the story. Arguing about payload size
instead of doing the analysis is a wrong answer to a question he never asked.
Catalogue first. Then choose. Then wire it.

**R2 — NEVER hand-draw a character in code.** Hero and monster art comes from the
downloaded packs. This was called "mutlak, no negotiable". Procedural art is a
*fallback only*, never the deliverable.

**R3 — NYELENEH IS THE CORE.** Absurd, funny, slightly annoying, addictive.
Every system must pass the nyeleneh test:
  * ✗ "Fire Sword +10 DMG" — boring
  * ✓ "Auntie's kitchen cleaver that got lost in the dungeon. +10 DMG, but
       enemies get hungry."
Reference point: **Gintama** — total nonsense on the surface, a real emotional
spine underneath, and the serious moment always undercut before it gets smug.

**R4 — WRITING MUST SOUND HUMAN.** No AI-tidy prose. Rules that make it human:
  * Characters, not concepts. A joke needs somebody to be wrong.
  * Every blurb/line has a **turn** — it goes somewhere you didn't expect.
  * Do not state the irony. Show the fact and stop talking.
  * Voices must differ. If two characters could swap lines, rewrite both.
  * Never explain a joke. Never end on a moral.
  * Emotion is undercut, never announced.

**R5 — LANGUAGE: English primary, Indonesian secondary.** Always both.

**R6 — GLOBAL AUDIENCE, NO REAL COUNTRY.** SEA-flavoured humour is wanted, but
the setting is the invented republic of **NUSAGARA**. Never name a real country.

**R7 — NO RELIGIOUS JOKES. Family-friendly.**

**R8 — ENTERPRISE GRADE MEANS ZERO BUGS.** 0 console errors, 0 failed assets,
0 dead code paths — verified on the deployed URL, not just locally.

**R9 — RPG PRESENTATION.** Missions/dialogue use portraits with emotion states,
name plate, typewriter text. Not a bare text box.

**R10 — KEEP GOING.** Do not stop early to ask permission for work already asked
for. Finish, verify, deploy, then report.

**R-VOCAB-BANNED — DEVELOPMENT VOCABULARY NEVER ENTERS THE BUILD.** The words
used to brief this work are not part of the fiction and must never appear in the
running game — not in any UI string, not in a version string, not in any source
comment a player could read. The complete banned list:

  * "enterprise grade" / "enterprise-grade"
  * "absurd" (as a design term, not a character using it naturally)
  * "prompt" / "raw prompt"
  * "AI slop" / "AI"
  * "FREAK" (the owner used it as criticism, not as content)
  * "autentik" (used as dev-briefing feedback, not in-fiction word)
  * "nyeleneh" (internal design language — never in the build)
  * "enterprise" alone as a quality descriptor

If any of these appear in a string the player reads, it is a bug at the same
severity as a console error. Grep for them before every deploy.

---

## 0.5 — NO FALSE CONFIDENCE. NO HALLUCINATED SUCCESS.

**C1 — Never call something "verified" or "enterprise grade" on the strength of
metrics alone.** `0 console errors` + `0 failed assets` + `16 cards` says the
page did not throw. It says NOTHING about whether the game looks right or plays
right. Both can be true while the result is garbage.
> Broken 2026-09-05: reported "live and verified, 0 blank, 0 failed" while the
> player sprite was ~2x oversized, HUD panels were stacked on top of each other,
> and a dialogue box interrupted play constantly. All three were visible in one
> screenshot the owner took. I had never actually played it.

**C2 — PLAY IT BEFORE CLAIMING IT WORKS.** Start the game, move, fight, walk
into another region, and LOOK at the composition: sprite scale against the
world, panels overlapping, text readable, anything blocking play. A title
screen screenshot is not a gameplay check.

**C3 — State confidence honestly.** Say "I checked X and Y; I did not check Z."
Never imply broader verification than was performed. If it was not looked at,
say it was not looked at.

**C4 — The owner's screenshot outranks my test output.** If he shows a problem,
it exists. Do not re-run a passing metric and imply he is mistaken.

**C5 — Do not describe work as complete while known gaps exist.** List what is
still broken in the same message, without being asked.

---

## 1. VERIFICATION RULES (these exist because I broke them)

**V1 — LOOK AT IT. Counting is not verifying.**
I once reported "16 hero cards" as success while all five new cards rendered
**blank**. `querySelectorAll().length` proves a node exists, not that a human
sees anything. Every visual change ends with a screenshot I actually examine.

**V2 — A stale console is not a clean console.**
The browser tab buffers errors across navigations. Always confirm the error's
URL matches the build under test, or use a fresh tab.

**V3 — Extracted ≠ wired.**
I extracted the schoolgirl sprites and shipped without adding them to the
roster. An asset counts as done only when it is visible in the running game.

**V4 — Syntax check every edit:**
```
python3 -c "import io;s=io.open('index.html',encoding='utf-8').read();i=s.rindex('<script>');j=s.rindex('</script>');io.open('/tmp/game.js','w',encoding='utf-8').write(s[i+8:j])" && node --check /tmp/game.js
```

**V5 — Guard every material access.** Unlit materials have no `.emissive`.
Writing to it every frame killed the game loop with 22 000 exceptions.
Feature-check before touching a Three.js material property.

**V7 — Guard the load race.** A key or click arriving before `genLevel()` has
run left `SPAWN` null and threw on `SPAWN.start`. Any entry point reachable
during loading must check that the world exists before using it.

**V8 — A deploy is not verified until the deployed URL is opened.** The bug
above only surfaced on production, because the load there is slow enough for a
keypress to land mid-boot. Local-only verification would have missed it.

**V9 — One thing owns the bottom strip.** The scene player, the controls
legend, the minimap and the dev bar all lived at `bottom:0`. Any new fixed-
position panel must fade the others (`body.scene-on`) or it will overlap.

**V10 — Every panel that can appear during play must be dismissible.** The case
file opened mid-game with no close control. Anything that covers the game needs
Esc, a visible close button, or an auto-close.

**V11 — Synthetic keys need a hold.** `keydown`+`keyup` dispatched in the same
tick are never sampled by `readInput()`, so the input looks broken when it is
not. Hold ~140 ms between them when testing.

**V12 — Fix the cause, never shrink the symptom.** Feet sank into the floor,
so I shrank the hero. Wrong: `o.y` is the BOTTOM of the collider, and the
sprite was pinned at a fixed `p.y+1.0` that only lines up for a 2-unit cell.
Heroes are BIG; anchor the lowest opaque pixel to `p.y` instead.

**V13 — Hiding UI is not solving a layout.** When the dialogue overlapped the
legend and minimap I faded them out. The real fix was a smaller box in its own
lane. Never delete information to avoid designing.

**V14 — THE DOCUMENT SYSTEM (the UI's identity, in full).**
Generic dark glass cards read as slop. Nusagara runs on paperwork, so the
interface **is** paperwork — everywhere, with no second visual language:

* ink on paper (`--paper*` / `--ink*`); **squared corners, `--r-*` are 0**
* hard offset shadows, no blur, one light source
* a solid `--ink` **head band** carries every panel's title
* hairline rule = field divider · double rule = section close ·
  dotted leader = label ...... value · punch column = lives in a binder
* **red pad `--stamp` means an authority acted on it.** Blue `--stamp-2` is
  secondary. Nothing else on screen is red.
* START, RETRY and every announcement are **rubber stamps**, not gradient pills
* title / pause / death / victory are ONE sheet — FORM 404-B — stamped
  UNDELIVERED / PENDING / REJECTED / SIGNED FOR

**V15 — The typeface is the packs' own, extended, never imported.**
`assets/fonts/nusagara.ttf` = the CraftPix Tiny Pixel Hero pack's
`Planes_ValMore.ttf` plus the 7 glyphs it lacked (`'` `’` `·` `×` `↑` `°` `&`),
drawn on its own 68/1000em grid. Its pixel is 68/1000 em, so **set type only at
multiples of 14.7px** (`--t` 14.7 / `--t2` 29.4 / `--t3` 44.1). 12px smears it.

**V16 — No emoji in the UI.** Marks come from `ICONS` + `icon(name,size)`;
static markup writes `<i data-ic="key" data-s="14">` and `hydrateIcons()` swaps
it at boot. `icon()` returns **markup** — assign with `innerHTML`. Assigning it
with `textContent` printed raw `<svg …>` across the HUD.

**V17 — A derived value must be derived where it is USED, not frozen where it
is measured.** `monsterFoot()` measured the foot correctly and the legs were
still buried, because `applyTier` (×1.22) and miniboss status (×1.45 — 1.77
total) resize the mesh *afterwards*, and a plane scales about its **centre**,
sinking the feet by `height*(sc-1)/2`. `e.sc` is now the single source of truth
for monster size; `anchorFeet(e)` recomputes `yOff` after any change to it, and
both `scale.x` and `scale.y` are set from `e.sc` each frame (setting only X
left minibosses stretched vertically).
> This was the real cause of "kakinya terpendam ke bawah". Fixing the
> measurement and stopping there changed nothing on screen.

**V29 — EVERY GLYPH THE UI TYPES MUST EXIST IN THE PACK FONT.** The deck's
`&lsaquo;` / `&rsaquo;` arrows were not in `nusagara.ttf`, so those two
characters — and only those two — silently fell back to a system typeface: a
different face, different metrics, sitting off the baseline. Before shipping a
character in the UI, check `getBestCmap()`; if it is missing, DRAW it on the
68-unit grid like the other nine. Never let a fallback face into the interface.

**V30 — A DRAG SURFACE MUST NOT SWALLOW ITS OWN BUTTONS.** `#deck` took
`pointerdown` and called `setPointerCapture` for swipe. The `‹ ›` buttons live
inside it, so their clicks were retargeted to the deck and swallowed, and a
press-and-drag on an arrow fired the step twice — once from the drag, once from
the click. Any container that captures the pointer must bail out on
`ev.target.closest()` of its own controls, and those controls must honour the
same "that was a swipe" guard. Related: `:hover` latches after a tap, so guard
hover styling with `(hover:hover) and (pointer:fine)`; and a container with
`overflow:hidden` needs a `min-height` that fits its own controls.

**V27 — DO NOT MAKE THE TITLE SCREEN RENDER THE GAME.** I made the title
see-through so the live world showed behind it. That meant the engine rendered
the whole lit world — lights, backdrop, particles — every frame before the game
had started, alongside a SECOND WebGLRenderer for the roster card, with CSS
`filter` on sixteen 3D-transformed layers. It stuttered and froze real hardware.
> "GAME PATAH PATAH SEMUA FREEZING MY COMPUTER ALSO FREEZING." He was right.
Rules that follow from it:
  * **One WebGL context.** Never a second renderer for decoration.
  * **Never `filter:` on a transformed/composited layer.** Opacity is free;
    a filter re-rasterises the layer every frame.
  * Out-of-range items get `display:none`, not `visibility:hidden` — hidden
    still composites.
  * The title screen is paper. Nothing renders behind it.

**V28 — CPU TIME IS NOT FRAME TIME.** I timed the loop at 0.55 ms/frame and
took it as proof the game was fine while the owner's machine was freezing. That
number measures JavaScript only — it says nothing about GPU, compositor or
context switching, which is where this class of jank actually lives. If someone
reports stutter, believe them and REMOVE the expensive thing; do not answer a
hardware report with a microbenchmark.

**V22 — READ `STORY.md` FIRST.** It is the source everything derives from:
premise, cast, regions, tone law, why the interface is paperwork, what each
system is for, and what is still unbuilt. If the code and it disagree, one of
them is a bug.

**V23 — ONE PIXEL SIZE PER LINE-UP.** The art is not one resolution (32px Pixel
Frog, 128px CraftPix). Forcing both to one on-screen HEIGHT upscaled the 32px
sheets 6.6-8.0x and the 128px sheets 2.1-2.8x — three times the pixel size, side
by side, which is what "that magenta block" was. Anywhere characters appear
together, fix the **pixel**, not the height: one integer magnification for all,
honest heights, one shared floor line. (The WORLD still normalises people to
`HERO_TARGET_H` — V19. That is physics; this is presentation.)

**V24 — NEVER TRUST ONE READING OF THE VIEWPORT.** `window.innerHeight` returns
0 in some embedded contexts, which silently collapsed the roster magnification
to 1x and made every courier tiny. Take the largest sane value of
`documentElement.clientHeight`, `innerHeight` and a floor.

**V25 — WHATEVER IS OPEN ON TOP ABSORBS `Escape` FIRST.** The kit drawer's Esc
was being eaten by the pause handler underneath it. Order the keydown branches
so the topmost open thing gets first refusal, then `return`.

**V26 — A HIDDEN PANE PAUSES `requestAnimationFrame`.** `document.hidden` is
true in this browser pane, so nothing animates and every screenshot is a still
of frame one — a static screenshot here is NOT evidence the animation is broken,
and it is not evidence it works either. Expose the frame function temporarily,
drive it with explicit timestamps, verify, then remove the driver.

**V21 — A SHEET CARRIES DECISIONS. REFERENCE GOES BEHIND A TAB.**
The title screen holds only what the player must decide — who goes, and whether
to go. The manifest, the controls and the capability register are pulled out of
the folder one page at a time (`SHEETS` + `openSheet`/`closeSheet`), which cut
the sheet from ~2500px to ~930px without losing a single word.
Every pulled page is dismissible **three** ways (V10): `Esc`, the button in its
own head band, and clicking the desk around it — and while one is open it owns
the keyboard and the mouse, so Enter cannot start a run behind it.
The roster shows **the couriers themselves, no card frames**: a frame around a
sprite is chrome competing with the art. They stand on a soft ground shadow so
they are on the paper, not floating over it — which means the WebGL plane is
positioned by the **bottom** of the view, not its centre.

**V20 — THE TITLE SCREEN'S WEBGL IS A GUEST, NOT A RESIDENT.**
The roster's featured card runs a second `THREE.WebGLRenderer` (`heroStage`).
Three rules keep it honest:
  * `THREEJS` is a **closure var**, never `window.THREEJS`. Guarding on
    `window.THREEJS` silently disabled the whole showcase.
  * **Clone the texture.** `texHeroes[i]` is the live player sheet; writing
    `offset.x` on it to animate the card would corrupt the in-game sprite.
  * `heroStage.stop()` on `startGame`, and a `webglcontextlost` handler that
    falls back to the flat 2D avatar. A second GL context is allowed to fail;
    the drawer must keep working when it does.
Size the card's plane by **measured opaque pixels**, not the cell — same law as
V19, because the cells are 32px and 128px with different padding.
Keep the idle sway small (~9°): pixel art has no anti-aliasing to hide the
stair-stepping a large continuous rotation produces.

**V19 — A PERSON IS THE SCALE OF THIS WORLD.** Character size must never be
an accident of how much padding an artist left in a sprite cell. Heroes are
normalised to `HERO_TARGET_H` (**2.90**) by measured opaque pixels; a monster
that is people-shaped declares `hgt` in `MONSTERS` and is normalised the same
way (`zombie` 2.65, `soldier` 2.80, `robot` 2.85). Everything else keeps its
pixel-density size, so wildlife reads small and minibosses read huge.
> Broken until 2026-09-05: heroes were 2.35 and the human enemies were **1.56**
> — shorter than a rabbit (2.56). The owner's screenshot showed a schoolgirl
> being loomed over by a bunny. "karakter yang berbasis manusia harusnya
> diperbesar lagi... ini juga berlaku untuk enemy seperti zombie."

**V18 — `var L` anywhere shadows the translator.** `L(en,id)` is a function;
a `var L` inside any function hoists over it for that whole function. A torch
`var L` in `boot()` broke every translated string on the title sheet. Grep to
zero.

**V6 — Rename means rename everywhere.** `STORY.acts` → `STORY.thread` left a
stale read that crashed `startGame`. Grep the old name to zero after renaming.

---

## 2. PROJECT FACTS (current, verified)

* Single file: `index.html`. **Keep it single-file** — no build step.
* World: `LW = 1605` tiles, **15 biomes**, 107 tiles each, `biomeAt(x)=floor(x/107)`.
* 16 heroes, 24 monster species, 14 named NPCs (6 main cast + 8 supporting),
  quests, shop, gear, 3 currencies.
* Story: **PARCEL SEVEN** — three acts, 15 regions, one road west to east.
  Cast (main): BUNGA ARIMBI, HARUN SETIAWAN, LASMI/TIRA/WENING, IBU RANTI,
  TUAN BIMA WISESA, SRI HANDAYANI.
  Cast (supporting): PARMAN WIBISONO, SINTA RAHAYU, DREW SITUMORANG,
  AGUS WICAKSONO, RATNA KUSUMAWATI, WIRAWAN DJAYA, HENDRIK SOEMANTRI,
  NADIA SURYANA.
  The thread: everyone has a theory about the box; it is a spare key to a
  demolished house, sent by PAK HASAN (Counter 9). Delivered 41 years late.
* Minibosses: minotaur @ x=700 (biome 6, NEW MERIDIAN), demon @ x=1100 (biome 10, KERING OASIS).
* 15 background sets extracted — one per region, `assets/bg/<folder>/1.png`…`N.png`.
* All 15 region scenes (r0–r14 + open + end) wired in SCENES.
* Deploy: stage `index.html` + `_headers` + `assets/` to `/tmp/stage`, then
  `npx -y wrangler pages deploy /tmp/stage --project-name=parcelseven`
  → https://parcelseven.pages.dev
* `DEV.enabled` **must ship `false`** (hides the dev bar + `DEVAPI`).
  Flip to `true` only to verify, and always restore before deploying.
* `game-2d-pxl-assets/` (4 GB of packs) never enters the staging dir.
  It is the source library, not shipped content.

## 3. LICENSING (settled — do not re-litigate)

* **Pixel Frog** packs: CC0. Anything goes.
* **CraftPix** free packs: using the art *inside the game* is expressly
  permitted; **reselling the art files is not**. Never repackage the PNGs as a
  downloadable asset set. Credit lives in `assets/CREDITS.md`.
* Keep `assets/CREDITS.md` accurate. Do not label a CraftPix pack "CC0".
