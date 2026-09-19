# PARCEL SEVEN: Pixel Adventure

One parcel. Forty-one years late. Twenty regions between the depot and whatever door it belongs to.

Play it right now, no install: **https://parcelseven.pages.dev**

It runs in any modern browser, desktop or phone. Keyboard on desktop, touch controls on mobile.

## What this game is

You are a courier in Nusagara, an invented archipelago republic that runs entirely on paperwork. The parcel authority handed you Delivery Order Seven. It has been in transit longer than most of the staff have been alive. Everyone you meet has a theory about what is inside. Nobody knows.

The road runs west to east through twenty regions: depots, forests, a drowned ward, an oasis with one well, a temple of unread terms, the Department of Endings (Counter 8 is closed, it is always closed), and five more regions past that, because the reroute desk filed a reroute. Sixteen couriers are on the roster. You pick whose day this is.

The interface is paperwork on purpose. Menus, HUD, title, pause, death and victory screens are all the same form, stamped differently. The state runs on forms, so the game is a form.

## How it plays

Walk, double jump, dash, slash. Climb walls by holding toward them and jumping. E talks, trades and fishes. F travels between lit totems. Q eats. C swaps courier.

Each region ends at a sealed gate with a boss in front of it. Kill the boss and the gate portal lights. Walk in to ride through. There are nineteen seals, two arena bosses, a poop baron in the harvest district, and a warden at the end of the road. Shops, gear, cooking, quests, a skill tree, a bestiary, three currencies, day and night, weather, random events. The usual RPG organs, plus some the genre declines to have.

## About the difficulty, read this first

This game is unfair on purpose. Not broken. Unfair.

A non-exhaustive list of things that will kill you: the department files forms from the sky with about a second of warning. Floor steps and platform planks that look ordinary and are razor sharp. Climbing over a sealed gate breaks the seal and the keeper hunts you until one of you is filed. Falling paperwork in every region has a name. Poop explodes.

None of that is a bug. It is the design, and it is tuned so a careful courier with full hearts, good gear and lit checkpoints always has a way through.

Actual bugs are a different matter. The rule on this project is simple: a player screenshot beats every metric. If you can show it, it exists, and it gets fixed. If you find something that looks broken, file an issue with a screenshot and the region name. Things that are merely cruel are working as intended.

## How this game was made

This game is a public stress test for [Vanexa Agent](https://github.com/ikbalsakata500445jensen/vanexa-agent), the agent harness built by [Ikbal Fadilah](https://github.com/ikbalsakata500445jensen), founder and solo developer of Vanexa AI. Vanexa Agent is currently in testing, and this game is one of the things it is being tested on: a real, shippable, twenty-region action RPG, built and debugged through the harness end to end.

Concretely, that means the bulk of the engineering here, the brutal verification loop behind it (play it, screenshot it, believe the screenshot), and most of the systems below were driven through Vanexa Agent while it runs the Muse Spark 1.3 contributor model as its provider.

Honesty requires the rest of the sentence too. This was not a single-harness build. Parts of the work also went through [Claude Code](https://github.com/anthropics/claude-code) (with Claude Opus 5 as the model, from [Anthropic](https://github.com/anthropics)) and through [OpenCode](https://github.com/sst/opencode) (also driving Muse Spark 1.3 contributor, a model by [Meta](https://github.com/meta)). If you are comparing agent harnesses, this repo is a fair specimen: one game, three harnesses, named providers, no mystery. Vanexa Agent did the heavy lifting and the project exists to prove it can. The other two did real work and get real credit.

## Under the hood

The whole game is one file, `index.html`, plus an `assets/` folder. No build step, no framework beyond Three.js for rendering. Open `index.html` and read it; the comments explain the pipeline (sprite atlases composited at load, one world scale for people, colliders anchored to measured pixels, fixed-step physics, DOM floating text over WebGL).

Run it locally with any static server from the repo root, for example `python3 -m http.server`, then open the printed address. Deploying is copying `index.html`, `_headers` and `assets/` to any static host. The live site runs on Cloudflare Pages.

`STORY.md` is the narrative bible everything derives from: premise, cast, regions, tone rules, systems. `facts.json` is the machine-readable build state. `assets/CREDITS.md` lists every third-party asset and its license.

## Art and asset licenses, please read this

The code in this repo is Apache 2.0 (see LICENSE, copyright 2026 Ikbal Fadilah). The art is a different story and it stays under its own terms:

* Hero and enemy sprites from Pixel Frog packs are CC0 public domain. Do anything with them.
* Sprites, backdrops, icons and the UI typeface from CraftPix free packs are used inside the game, which their license expressly allows. What it does not allow is reselling or repackaging the art files themselves. So: play the game, fork the game, learn from the game, but do not re-upload the PNGs as an asset pack. Full list and pack names live in `assets/CREDITS.md`.
* Music is CC0: "5 Action Chiptunes" by Juhani Junkala, and "Spooky Dungeon" by Memoraphile.
* UI icons are Lucide (ISC license).

If you reuse anything from `assets/`, you take on its license, not Apache. Check `assets/CREDITS.md` first. It is kept accurate on purpose.

## License

Apache License 2.0. See the LICENSE file. Copyright 2026 Ikbal Fadilah.
