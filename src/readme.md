**S.T.I.M. - Stimulant Tolerance Immersion Mod by Expand 0.1.0**

For S.T.A.L.K.E.R. Anomaly G.A.M.M.A. Author: Expand

In G.A.M.M.A. you can skip sleep completely with coffee, energy drinks, cocaine or epinephrine. S.T.I.M. adds stimulant tolerance: rest boosters get weaker the more rest they gave you since your last sleep, so sooner or later you have to sleep.

**How it works**
- Tolerance = the rest that boosters really gave you since your last sleep. A dose taken while almost fully rested gives little rest, so it adds little tolerance.
- Full-strength zone (default 10% of full rest): until your tolerance reaches it, boosters work at 100%.
- After that their effect falls linearly and reaches 0% at the booster rest limit (default 50% of full rest). Boosters can never give you more than this between two sleeps.
- The effect drops during a dose too, so one big dose and several small ones give the same result.
- Every rest booster counts (anything with a negative eat_sleepiness, including cigarettes and tea). Weak items add little tolerance, and they are reduced in the same way.
- Sleep removes 7.5% tolerance per hour (the amount sleep restores per hour in G.A.M.M.A.). Tolerance 50% needs about 7 hours of sleep; a shorter sleep removes part of it.
- No recovery while awake.

Example with default settings (player tired enough): coffee 100% / 85% / 65% / 49% / 37%; cocaine 87% / 46% / 23% / 11%.

**Display**
- Tooltip line on rest boosters: your tolerance (100% = boosters do nothing) and the item's effect right now.
- The Rest (Sleep) row in the item stats shows what the item gives right now.
- Optional on-screen message after each dose (off by default).

**MCM (S.T.I.M. tab)**
Enable, full-strength zone, booster rest limit, tolerance removed per hour of sleep, tooltip line (off / only with tolerance / always), current value in the Rest row, message on use (off / only reduced doses / every dose), debug log.

**Requirements and compatibility**
- Needs the G.A.M.M.A. sleep system (actor_status_sleep.script from G.A.M.M.A. Sleep Balance, part of base G.A.M.M.A.).
- Works with UI Rework G.A.M.M.A. Style and with the default G.A.M.M.A. tooltips.
- Artefact and anomaly effects on sleepiness (Perk-Based Artefacts, Dynamic Anomalies Overhaul) are not changed and add no tolerance.
- The inventory sleep bar preview (Better Stats Bars, UI Rework) still shows the full value.
- Any MO2 position; file names are unique. Safe to add to an existing save. Removing it leaves one unused value in the save.

**Check**
After loading a save, the log (Anomaly\appdata\logs) shows lines starting with [STIM].

**Version history**
- 0.1.0: first test build.
