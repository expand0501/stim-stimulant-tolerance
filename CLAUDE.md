# S.T.I.M. - Stimulant Tolerance Immersion Mod by Expand

Goal: rest boosters must not let the player skip sleep. They lose effect the more rest they gave since the last
sleep. Simple and lightweight, event-driven only. Shipped readme: `src/readme.md`.

## Files
- `src/gamedata/scripts/stim_tolerance.script`: all logic (log tag `[STIM]`).
- `src/gamedata/scripts/stim_tolerance_mcm.script`: MCM menu (id `stim_tolerance`, single page).
- `src/gamedata/configs/mod_system_stim_tolerance.ltx`: fake sections `stim_rest_0..13`
  (eat_sleepiness = -0.0005 * 2^k).
- `src/gamedata/configs/text/{eng,rus}/st_stim_tolerance.xml`: strings (rus = Windows-1251).

## Version
In `mod.json`, readme title + history, script header, both text files (comment line).

## How it works (keep)
- Sleep system: `actor_status_sleep.script` from G.A.M.M.A. Sleep Balance (wins in both profiles; same on `dev2`).
  Hidden `last_sleep` 0..10000, no setter. Item use adds `eat_sleepiness * 2000`. `create()` is called from vanilla
  `game_difficulties` on_game_load and registers `actor_on_item_use` by module name, so replacing
  `actor_status_sleep.actor_on_item_use` in our `on_game_start` makes it register our wrapper. First update also
  swaps a registered original for the wrapper (only when the sleep difficulty factor is on).
- Reduced dose = original function fed our fake sections (binary steps), same trick as Perk-Based Artefacts and
  Dynamic Anomalies Overhaul. Fake items from other mods are Lua tables and pass through (only userdata counts).
- Tolerance = rest really received (get_last_sleep before/after). Effect 100% below zone, linear to 0 at limit,
  integrated over the dose: `x' = W - (W - x) * exp(-n / W)`, W = limit - zone.
- Sleep (`actor_on_sleep(hours)`): tolerance -= hours * rate. No recovery while awake (Expand: against the goal).
- Multiplier assumed 2000, learned from the first dose not cut by the sleepiness floor.
- Tooltip: wraps `ui_item.item_description` (no other mod patches it; engine looks it up by name every call; Lua
  tooltip goes through `ui_item.get_obj_desc`) and `ui_item.get_sec_desc` (DOGMA also wraps it, chain-safe).
  Stat row: `utils_ui.stats_table.booster.eat_sleepiness.value_functor` = ours, keeps a previous functor; re-ensured
  from the description hook because ish_item_stats / sota rebuild the table.
- Tooltip line position (1.0.1, Expand's request): last bullet of the property list. GAMMA's `build_desc_footer`
  returns `str .. <generated bullets (sleepiness/thirst/harm...)> .. " \\n"`, and Quest Item Tooltip / others append
  their blocks after it. We also wrap `build_desc_footer`: it only remembers the text up to that closing " \\n"
  ("head", ring of 8). `item_description` / `get_sec_desc` (uncached, outside ui_item's per-id/per-section cache)
  insert the fresh line at the end of a matching head; no match -> append at the end as before. Works in any wrapper
  order as long as footer wrappers keep the input as prefix (all GAMMA ones do; Perk-Based Artefacts prepends `\\n`
  only for artefacts). Last result cached by (input string, line).
- Wording (1.0.2): "Толерантность к стимуляторам: X%, текущая эффективность: Y%" / "Stimulant tolerance: X%, current effectiveness: Y%" (no trailing period).
- Tooltip shows tolerance as % of the limit (100% = boosters do nothing), because the Rest row uses different scales
  (Accurate Defense Values: 8750 = 100%; UI Rework: 10000 = 100%).
- Use message: `actor_menu.set_msg` (center screen, not PDA). Off by default (Expand). No other item-use script in
  either profile shows a center message.

- Logging: Anomaly's `printf` only fills in `%s`, so `log`/`dbg` format with `string.format` first (0.1.1 fix).
- Game files are CRLF in the working copy (repo stores LF, `.gitattributes` `text=auto`). The Edit tool may write
  LF: check with `file` before building.

## Test results
- 0.1.0 in profile `v31.1 - radiation rework` (Expand: "works fine so far", log 2026-11-13): dose scaling matches
  the formula exactly (energy drink 900 -> 900 / 825; adrenalin 4000 -> 2070 / 743; small item 100 -> 30),
  multiplier 2000. Fake sections apply. No errors.

- 1.0.2, run automatically 2026-11-26 (suite `stim`, `tests.md`; profile `Claude Test`, installed zip
  `S.T.I.M._..._1.0.2` = src, save `claude_test`; runs 20261126-133740 `basics`, -134330 10 scenarios,
  -134811 `floor`, `tooltip`, `sleep_real` with -Isolated). Final: 13 scenarios PASS (basics 18 checks, dose_curve 31,
  floor 5, sleep 7, sleep_real 5, settings 9, disabled 6, tooltip 13, message 5, saveload 9, no_mcm 4), 0 FAIL,
  0 UNCLEAR, no Lua errors / FATAL (log-triage). First 10-scenario launch had 2 FAILs, both **test bugs**
  (verified): `zero_nothing` read sleepiness 600 ms late (+30 sleep tick), `stat_row_off` expected a number where the
  mod returns nil on purpose (winning `utils_ui.get_stats_value`, HD Inventory Framework UI Patch GAMMA, then shows
  the full value). Seen in the log (**verified**): every dose = formula within 1 point (energy drink 900 -> 900 / 825
  / 660 ...; 10 doses = one 10x dose; 0 at the limit; adrenalin 3111 from 0, 1580 at 2500), floor counts only rest
  received, mul stays 2000, sleep callback and a real forced sleep (2 h, early wake) remove hours * rate, MCM zone /
  limit / invalid pair / rate / disabled / no MCM, tolerance kept over save/load with the wrapper still registered,
  tooltip line once, numbers right, placed as the last property bullet (after GAMMA's sleepiness / thirst bullets),
  modes 0/1/2, stat row value scaled, message modes 0/1/2. Not covered: how it looks on screen, base GAMMA profile.

## Open items
- 1.0.1/1.0.2 (tooltip line moved into the property list + new wording; 1.0.2 = final wording): placement and
  numbers pass the in-game suite (see Test results); not yet looked at by Expand on screen.
- 1.0.0 = first release version (Expand's call), same code as 0.1.1 (log formatting + CRLF).
- Git Bash `sed -i` strips CR on this PC: fix line endings with PowerShell (cp1251-safe) after shell edits.
- Sleep reduction and save/load of tolerance: seen in the in-game suite 2026-11-26 (not yet in one of Expand's games). Expand reported no
  problems, but the tooltip line / Rest row under UI Rework were not confirmed one by one.
- Expand reported that "ilrathCXV's Meat Spoiling Timer in Tooltips" needs a patch for UI Rework; cause not found
  (our hook is on a different function). Waiting for Expand's details.
- Preview sleep bars (Keybinds fixes' better stats bars, UI Rework sota bars) still show the full value.
