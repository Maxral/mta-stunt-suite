# Complete Manual — Stunt System + Stunt Tools (v1.0.0)

[Versão em Português](MANUAL_COMPLETO_PT.md) · [README](../README.md)

## Contents

1. [Overview](#1-overview)
2. [Installation and ACL](#2-installation-and-acl)
3. [Themes, languages and font](#3-themes-languages-and-font)
4. [stunt_tools — F7 Hub](#4-stunt_tools--f7-hub)
5. [Saves and Warps](#5-saves-and-warps)
6. [Training shortcuts and tools](#6-training-shortcuts-and-tools)
7. [Spectator mode](#7-spectator-mode)
8. [Segmented Replay / TAS](#8-segmented-replay--tas)
9. [Replay Gallery and Player](#9-replay-gallery-and-player)
10. [Ghost mode, 3D trail and A-B loop](#10-ghost-mode-3d-trail-and-a-b-loop)
11. [Cut editor](#11-cut-editor)
12. [Admin panel: /configwarp](#12-admin-panel-configwarp)
13. [stunt_system — Arena Manager](#13-stunt_system--arena-manager)
14. [Settings & Difficulties](#14-settings--difficulties)
15. [Stunt notes](#15-stunt-notes)
16. [F2 map, radar and CV Zones](#16-f2-map-radar-and-cv-zones)
17. [Command reference](#17-command-reference)
18. [Auto-Update](#18-auto-update)
19. [Data files and backups](#19-data-files-and-backups)
20. [Troubleshooting](#20-troubleshooting)

---

## 1. Overview

- **`stunt_system`** runs the *arena*: loads the map's stunts, tracks completions, records and ranking, draws the F2 map and provides the Arena Manager.
- **`stunt_tools`** handles *training and creation*: saves/warps, replay recording and playback, Ghost mode, freecam and utilities.

Each resource works alone. When both run, **language, theme and font are synchronized** in both directions.

## 2. Installation and ACL

See the [README](../README.md#installation). In short:

- Folders into `resources/`, `refresh`, `start stunt_system`, `start stunt_tools`.
- Admin accounts in the ACL group **Admin**.
- Resources granted `function.fetchRemote` (and `function.restartResource`) for auto-update.
- **Disable other Freecam/CamHack scripts that use `H`.**

## 3. Themes, languages and font

- **Languages:** `PT | EN` selector at the left of the menu header. **The default on first join is English (EN)**; a manual choice is saved and shared by both resources. New languages: copy `lang/en.xml` to `lang/xx.xml`.
- **Themes** (F7 → Settings → THEME, or the THEME button in Settings & Difficulties; applies to both resources):
  | Theme | Look |
  |---|---|
  | **Hybrid** (default) | Modern look with the compact layout and vector icons of Minimalist. |
  | **Modern** | Dark Glass panels with orange accents. |
  | **Minimalist** | Compact bars, icon buttons with tooltips, sliding switches. |
  | **Classic** | Native MTA controls with the basic skin. |
- **Font:** Default → Segoe UI → Bahnschrift → Calibri (Settings → FONT).
- **Version badge:** both menu footers show `v1.0.0` in discreet gray, read from `meta.xml`. For Admins, when GitHub has a newer version, it becomes `v1.0.0 • New version available` in orange.

## 4. stunt_tools — F7 Hub

Open with **F7** (closes every hub window if one is already open).

- **Player list** with ID, name, vehicle and **Status** (AFK, in replay, etc.).
- Buttons: **TELEPORT** (warp to the selected player's save), **COPY SAVE**, **WATCH**, **HELP**, **SETTINGS / KEYS**, **REPLAYS** (Gallery), **MY WARP: PRIVATE**, **/CV COMMAND**.
- **ADM gear** (Admin only): opens the `/configwarp` panel.
- Footer: description of the hovered button, version and credits.

### Settings (keys)

Default keys (all rebindable; `Backspace` clears a key; APPLY AND SAVE writes them):

| Action | Key | Action | Key |
|---|---|---|---|
| Save (`/sw`) | `1` | Record Replay | `F10` |
| Back (`/lw`) | `2` | Stop Ghost | `L` |
| Delete (`/dw`) | `3` | Open Gallery | `F4` |
| Private | `4` | Freecam + Teleport | `H` |
| Bike Auto-Tap | `Left Shift` | Repair / Flip Vehicle | `R` |
| Invisible Objects | `I` | Install / Refill Nitro | `N` |
| Hide Players | `O` | Engine On / Off | `J` |
| Transparent Players | `K` | | |

Options applied instantly (saved automatically): **Auto-Tap mode** (hold/toggle), **Speedometer HUD**, **Camera reset on /lw**, **GHOST 3D TRAIL** (ON/OFF, default ON), **THEME**, **FONT**, **RESTORE DEFAULTS**.

## 5. Saves and Warps

| Command | Key | Function |
|---|---|---|
| `/save` or `/sw` | `1` | Saves position, rotation, velocity and vehicle |
| `/warp` or `/lw` | `2` | Returns to the last save |
| `/delwarp` or `/dw` | `3` | Deletes the last save |
| `/sw 1` … `/sw 5` / `/lw 1` … `/lw 5` | — | **Fixed training slots** (login required; stored in your account) |
| `/privado` | `4` | Toggles MY WARP private (others cannot copy/teleport) |
| `/copiarsave` / `/cwarp` | — | Copies the save of the player you watch (or `[id/name]`) |

In **Play Mode** (dimension 0) `/sw` only saves while the vehicle is nearly stopped (up to 5 km/h) and on the ground; staff (Admin / SuperModerator / Moderator) save freely. History keeps up to 20 saves per player (configurable).

## 6. Training shortcuts and tools

- `/cv [name or ID]`, `/v` — spawn a vehicle (respects the CV Zone in Gamemode); `/del` — removes your vehicle; `/gm` or `/ghostmode` — toggles **collision with other players and vehicles** (default: on = no collision, "ghostmode").
- `/timeset [hour]` (e.g. `17:30`) and `/w [id]` — time and weather **for your game only**; the clock is frozen at 12:00 by default.
- `/stanthud` or `/stunthud` — speedometer HUD (KM/H, MPH, gear/RPM, nitro). Off by default.
- **`I`** Invisible Objects · **`O`** Hide Players · **`K`** Transparent Players (`O` and `K` replace each other).
- **`H`** Freecam + Teleport · **`R`** repair/flip · **`N`** nitro · **`J`** engine.
- `/objdebug` — diagnoses how the map hides objects (alpha, scale, dimension); `/fixdim [id or name]` — **staff only**: ends the player's watch/replay and moves them and their vehicle to dimension 200 (editor) or 0 (Play).

## 7. Spectator mode

`/watch [id or name]` or the F7 **WATCH** button. The camera follows the player; you are parked (frozen, invisible, no collision). `Backspace` or `/watch` exits and returns you to the same spot and vehicle. Respects MY WARP PRIVATE. In Play Mode you must be stopped and on the ground to begin.

## 8. Segmented Replay / TAS

- **`F10`** starts recording your inputs. Each **save (`/sw`)** becomes a checkpoint and each **warp (`/lw`)** discards the failed attempt and rewinds the recording to the save, so **only the clean run remains**.
- `F10` again finishes: name it and choose **SAVE LOCAL (.CSV)**, **SAVE AND PUBLISH TO THE GALLERY** or **DISCARD**.
- You can **continue a recording** from a replay (CONTINUE FROM HERE / CONTINUE RECORDING), **clone to draft** and **join replays**.
- `/gravarstunt <id>` or `/gravarstunt l<index>` — opens a replay (published by id, or from the local list by index) in the player in recording/queue mode (Cinema Mode).

## 9. Replay Gallery and Player

Open with **F4**, `/replays` or the F7 REPLAYS button.

- Tabs: **All**, **My Replays (local)**, **General Gallery**, **Drafts**, **Published**; creator filter and sorting (newest, oldest, longest/shortest, name); search by name/creator/vehicle.
- Actions: **WATCH** (double-click), **CONTINUE**, **CLONE**, **JOIN**, **PUBLISH**, **RENAME**, **EXPORT .CSV**, **DELETE** (with confirmation), open folder.
- **Player:** `Space` play/pause · `←/→` −3 s/+3 s · click the bar to seek · speeds 0.1x–4x · **LOOP** · `K` **FOLLOW/FLYCAM** camera · `H` hides the UI · `Esc`/`Backspace` exits.
  - **FOLLOW:** GTA camera following the car (`V` changes distance).
  - **FLYCAM:** `WASD` moves, `Q/E` down/up, `Shift` fast, `Ctrl` slow, scroll changes speed.
  - Applies the recording's time and weather and restores yours on exit. Diamonds on the timeline mark saves.
- **A-B loop:** key **L** (or the **A-B** button): 1st press sets **A**, 2nd sets **B** and starts the loop, 3rd clears it.
- **Playlist:** `|<` previous / next `>|` following the list you clicked WATCH from; **Cinema Mode** (queue) for recording sequences.

## 10. Ghost mode, 3D trail and A-B loop

In the Gallery pick a mode and click **RACE AGAINST (GHOST)**. You keep driving while a translucent, collision-free, silent car replays the run.

| Mode | Behavior |
|---|---|
| **Sync with Warp + Loop** | On start the server puts you at the starting line with an auto-save; the ghost waits for you to accelerate and **launches with you on every `/lw`**. |
| **Continuous Loop Only** | The ghost runs non-stop, ignoring warps. |
| **Record Queue (Cinema Mode)** | Continuous playlist for recording. |

**3D trail (`GHOST 3D TRAIL`):** a continuous 3D line shows the ghost's exact path on the ground and in the air, fading from tail (cyan, transparent) to head (orange, opaque). It is cleared on every loop restart, so no lines cross the map. **ON/OFF**, default **ON**, in the Gallery's Ghost row and in **F7 → Settings**; your choice is saved.

**A-B section:** set **A** and **B** in the player, exit it and start the Ghost **of the same replay**. The ghost loops **only inside A–B**: it starts exactly at A and restarts at A when it reaches B; Sync mode also launches from A. Without A-B it uses the automatic start and runs to the end. The bottom card shows `A-B 00:05 → 00:09` and the section progress. The A-B is remembered while the game stays open.

To stop: **`L`**, `/stopghost` or **STOP GHOST**.

## 11. Cut editor

In the player, the **scissors** button opens the editor over the timeline: drag **[ START** and **END ]** to trim the ends and use **+ SECTION** to create sections to remove (draggable handles; right-click removes). **APPLY CUT** saves a **`_cut` copy**; the original stays untouched.

## 12. Admin panel: /configwarp

Admin only (**ADM** gear in F7 or `/configwarp`). Changes apply live to everyone and are saved to `config_warp.json`:

| Option | Default | Effect |
|---|---|---|
| Settle time (ms) | 400 | Time frozen at the point before `/lw` releases (0–1500) |
| Save velocity | ON | `/lw` restores linear/angular velocity |
| `/lw` cooldown (s) | 0 | Delay between two `/lw` (0–10) |
| Allow copy | ON | COPY SAVE button, `/copiarsave`, `/cwarp` |
| Max saves | 20 | Per-player history (1–50) |
| Allow mid-air save | ON | `/sw` while falling |
| Repair on `/lw` | ON | Fixes the vehicle when warping |
| Editor returns to point | ON | Map Editor F6: ON = leaving edit mode returns you to the point you were at before editing; OFF = you go where the editor camera was |

**SAVE SETTINGS** writes; **RESTORE DEFAULTS** resets everything.

## 13. stunt_system — Arena Manager

Open with **`Alt+F2`** or `/stunts` (same key closes).

- List of the **active arena's** stunts (tagged `[STUNTAGE]` in the map) with name, vehicle, value, difficulty (name color) and type (touch, 3s, challenge). Filter bar: **Search**, **Type** (Touch / 3s / Challenge), **Status** (In Test / Tested), **Difficulty**, **Progress** (Pending / Completed), **Sort by** and **Clear**. Summary bar: arena, total, tested and in test.
- **Double-click** (or `Enter`) teleports to the selected stunt — **staff only** (ACL groups Admin / SuperModerator / Moderator, holders of the `resource.stunt_system.manage` right, or the `command.kick` permission). Footer: `Showing N of M stunts`.
- Buttons: **SYNC MAP** (reloads stunts from the map file, with confirmation), **TESTED / IN TEST** (staff), **TESTED MARKERS** (show/hide in purple), **MARK PENDING** (reset your progress on the stunt), **SETTINGS**.
- Language selector and version badge in the header/footer.

## 14. Settings & Difficulties

Side panel of the Manager:

- **Difficulty ranges:** ceilings in `$` (increasing; *Demonic* = above *Very Hard*'s ceiling). Only **staff** (same criteria) can edit; saving updates all online players.
- **Resource mode (Admin only):** **FULL GAMEMODE** (real money, account balance, F2 RANKING, spawn at peds and CV Zone on `/cv`) or **CREATOR (PLUGIN)** (creation tools only, no money/ranking/forced spawn/`/cv` lock).
- **THEME** and **FONT** (also apply to stunt_tools).
- **RESET MY PROGRESS:** erases only your completed stunts in the current arena.

## 15. Stunt notes

**Right-click** a stunt in the list to open the **Add / Edit / Remove Note** menu. Only **staff** can edit; the text is cleaned (no line breaks or `#RRGGBB` codes) and limited to **100 characters**. The note is stored per arena and shown in orange/white right under the selected stunt, for every player.

## 16. F2 map, radar and CV Zones

- **`F2`** toggles the custom arena map (`F11` = native map). Scroll = zoom; drag = pan. Drawers **VEHICLES**, **STUNTS** (search; double-click teleports — staff) and **RANKING** (Top Stunters and Top Record Holders; Gamemode only).
- Blue **CV** icon: teleports to the CV Zone's Spawn Point.
- Player arrow on the map and radar.
- **CV Zones:** spawn peds + green cylinder configured in `[STUNTAGE]` arenas.

## 17. Command reference

**stunt_system:** `/stunts` (opens/closes the Manager), `/blips` (recreates blips), `/blipsize [1-25]` (blip size), `/mvs` or `/markvehiclestunts` (vehicle filter for stunts on radar/F11), `/mark` (tracks a player on radar/F11), `/resetstunts` (recreates markers and blips and reloads server state — does **not** erase progress), `/resetstunt [name]` (resets **your** progress on that stunt; with `all` at the end, **Admin only**, resets for everyone), `/resetallstunts` (resets all **your** stunts in the active arena), `/stuntarena` (shows the active arena; staff: `/stuntarena [name]` forces the name, `/stuntarena off` returns to auto-detection), `/stuntdiag [name]` (staff: diagnoses the copies of a stunt), `/cvdiag` (diagnoses the `/cv` lock for you), **`/atualizarstunt`** (Admin).

**stunt_tools:** `/sw` `/save` · `/lw` `/warp` · `/dw` `/delwarp` · `/privado` · `/copiarsave` `/cwarp` · `/watch` · `/cv` `/v` · `/del` · `/gm` `/ghostmode` · `/timeset` · `/w` · `/stanthud` `/stunthud` · `/replays` · `/stopghost` · `/gravarstunt` · `/replaysync [file.csv]` (staff: syncs the `replays_publicos/` folder or imports one file) · `/configwarp` (Admin) · `/objdebug` · `/fixdim` (staff) · **`/atualizartools`** (Admin).

## 18. Auto-Update

Details in the [README](../README.md#auto-update). In short: check 5 s after start and every 6 h via `fetchRemote`; console message and Admin chat notice (with changelog and instructions); `/atualizarstunt` and `/atualizartools` download the files in `version.json`, **back up to `_backup_update/`**, replace and restart the resource. Network/ACL errors are silent (one console line).

## 19. Data files and backups

Never overwritten by the updater: `stunts.db`, `saves_stunt.db`, `replays.db`, `config_warp.json`, `replays_publicos/`, `replays/`, `saves/`. Player preferences live on the **client** (`binds.xml`, `hub_lang.xml`/`stunt_lang.xml`, `fonte_pref.xml`). Update backups: `<resource>/_backup_update/<timestamp>_v<version>/` — to roll back, copy the files back and `/restart`.

## 20. Troubleshooting

| Symptom | Likely cause / fix |
|---|---|
| Console: *Auto-update disabled* | Missing `function.fetchRemote` in the resources' ACL. |
| `/atualizar…` cannot reach GitHub | No internet, GitHub down, or the `manifesto` URL still has `Maxral/mta-stunt-suite`. |
| `H` does not open freecam | Another resource uses `H`; disable it or rebind. |
| Ghost ignores A-B | Set A-B in the player **of the same replay** and close the player before starting the Ghost. |
| "New version" badge missing | Only ACL Admins get the notice; check the group and the 6 h check. |
| Initial language is English | That is the default; use the `PT / EN` selector (it is saved). |
