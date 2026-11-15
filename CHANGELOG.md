# Changelog - S.T.I.M. Stimulant Tolerance Immersion Mod by Expand

- 1.0.2: tooltip wording: "Stimulant tolerance: 24%, current effectiveness: 60%" / "Толерантность к стимуляторам: 24%,
  текущая эффективность: 60%" (colons instead of dashes, no trailing period).
- 1.0.1: tooltip line moved into the item's property list (last bullet, before the empty line and blocks of other
  mods such as Quest Item Tooltip). New wording: "Tolerance - 24%, effectiveness - 60%." /
  "Толерантность - 24%, эффективность - 60%." The line still shows the current value (inserted after ui_item's cache).
- 1.0.0: first release version (Expand). Same code as 0.1.1.
- 0.1.1: fix: [STIM] log lines printed raw format codes (`%.0f`, `%d`) instead of numbers, because Anomaly's
  `printf` only fills in `%s`; the mod now formats the text itself. Game files use CRLF line endings. Tested in
  0.1.0 (game log): dose scaling works and matches the formula (energy drink 100% -> 92%, adrenalin 52% -> 19%).
- 0.1.0: first test build. Tolerance from rest really received from boosters, linear effect drop between the
  full-strength zone (10%) and the booster rest limit (50%), sleep removes 7.5% per hour, tooltip line, value in the
  Rest stat row, optional on-screen message.
