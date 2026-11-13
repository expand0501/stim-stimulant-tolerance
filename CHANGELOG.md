# Changelog - S.T.I.M. Stimulant Tolerance Immersion Mod by Expand

- 1.0.0: first release version (Expand). Same code as 0.1.1.
- 0.1.1: fix: [STIM] log lines printed raw format codes (`%.0f`, `%d`) instead of numbers, because Anomaly's
  `printf` only fills in `%s`; the mod now formats the text itself. Game files use CRLF line endings. Tested in
  0.1.0 (game log): dose scaling works and matches the formula (energy drink 100% -> 92%, adrenalin 52% -> 19%).
- 0.1.0: first test build. Tolerance from rest really received from boosters, linear effect drop between the
  full-strength zone (10%) and the booster rest limit (50%), sleep removes 7.5% per hour, tooltip line, value in the
  Rest stat row, optional on-screen message.
