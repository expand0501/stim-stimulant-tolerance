# S.T.I.M. in-game tests (tools\autotest, suite `stim`)

Runner: `tools\autotest\mod\gamedata\scripts\zzz_claude_autotest_stim.script`. Each scenario starts from a fresh load of `claude_test`.
Proof = the mod's own state read through upvalues (tolerance, zone/limit/rate points, mul) plus the sleep script's `get_last_sleep()`,
compared with the runner's own copy of the formula (`x' = W - (W - x) * exp(-n / W)`).

| Scenario | Setup / action | Proof | UNCLEAR when |
|---|---|---|---|
| basics | none | wrapper source = stim_tolerance; stim_rest_0..13 values; defaults table = runner copy; deliver() on 7 inputs; MCM menu 14 entries; 33 eng strings; `[STIM] loaded ... scaling on` | - |
| dose_curve | tol 0, sleepiness 8000 before each, 10 energy drinks, then one at the limit, adrenalin at 0 and 2500 | rest received and tolerance growth = formula (+-1); first dose full; effect falls; 10 doses = one 10x dose; nothing at limit; mul stays 2000 | no booster section |
| floor | sleepiness 200 / 0, energy drink | tolerance grows only by rest really received; mul not learned | no booster |
| sleep | tolerance 3000, `actor_on_sleep` 2 h / 10 h; MCM rate 20 / 1; 0 h | tolerance - h * rate, floor 0 | - |
| sleep_real (-Isolated) | tol 3000, sleepiness 8000, `ui_sleep_dialog.sleep_forced(3)` | tolerance = 3000 - hours actually slept * 750; next dose follows formula | no actor_on_sleep in 60 s |
| settings | MCM zone 0 / limit 20; zone 30 / limit 10; limit 100 | zone/limit points; doses follow formula | - |
| disabled | MCM off, tol 4900 | full dose, tolerance unchanged, no tooltip line; on again -> reduced | - |
| tooltip | tol 0 / 2000, tooltip_line 1 / 2 / 0, non-booster, stat_row on/off | line once, 40 % / formula %, wording, place before the property list's closing line, item tooltip, stat row functor and value | footer head never seen (place) |
| message | use_message 0/1/2 at tol 0 / 3000 | center message with the effect text or none | - |
| saveload | 3 doses, save `claude_autotest`, load | same tolerance, loaded line, wrapper still in place, next dose reduced per formula | - |
| no_mcm | every MCM value missing | mod defaults in effect, dose follows formula | - |

For Expand (not automated): how the tooltip line looks under UI Rework / other tooltip mods, the Rest row bars (known: preview bars show the
full value), the center message on screen, Russian text on screen, a dose taken through the inventory with use animations.
