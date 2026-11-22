---
name: local-shabbat
description: "Use when someone needs candle-lighting, Havdalah, or Torah portion details for the upcoming Shabbat in a particular place."
---

Use Jewish Calendar’s `shabbat_times` for the coming Shabbat or holiday. It needs latitude, longitude and an IANA time zone. Use supplied coordinates or a known city center with the locality stated. If the place is ambiguous, ask which locality the user means; a home address is unnecessary. Pass an explicit candle-lighting offset if requested.

Give the dates, local times and time zone for the returned location, the offset used when available, and the Torah portion if supplied. The tool cannot select an arbitrary past or future Shabbat by date. If a date beyond the upcoming result is requested, explain the date the returned times actually cover.
