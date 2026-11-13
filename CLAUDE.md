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
- Tooltip shows tolerance as % of the limit (100% = boosters do nothing), because the Rest row uses different scales
  (Accurate Defense Values: 8750 = 100%; UI Rework: 10000 = 100%).
- Use message: `actor_menu.set_msg` (center screen, not PDA). Off by default (Expand). No other item-use script in
  either profile shows a center message.

## Open items
- 0.1.0 not tested in game yet. Check: tooltip line under UI Rework (profile `v31.1 - radiation rework`), Rest row
  value, dose scaling with debug log, sleep reduction, save/load.
- Expand reported that "ilrathCXV's Meat Spoiling Timer in Tooltips" needs a patch for UI Rework; cause not found
  (our hook is on a different function). Waiting for Expand's details.
- Preview sleep bars (Keybinds fixes' better stats bars, UI Rework sota bars) still show the full value.
