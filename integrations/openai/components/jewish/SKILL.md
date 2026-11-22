---
name: use-jewish
description: "Convert a civil date to the Hebrew calendar, list Jewish holidays and fasts in a date range for the Diaspora or Israel, or get candle lighting and Havdalah times and the Torah portion for the coming Shabbat at a place."
---

Jewish Calendar is public and read only. The data comes from Hebcal (CC BY 4.0).

1. For a conversion, call hebrew_date with date as YYYY-MM-DD. Set after_sunset to true when the moment is after local sunset, because the Hebrew day has then already moved to the next date. The result lists the day's events, such as a holiday or, on Shabbat, the Torah portion. The tool converts from Gregorian to Hebrew only.
2. For holidays, call jewish_holidays with start_date, days (up to 366), israel set to true for the Israel schedule and false for the Diaspora, and major_only when only the main holidays are wanted. Name the schedule in the answer. If the person's location is unknown and the schedules differ, show both.
3. For Shabbat times, call shabbat_times with latitude, longitude and an IANA time zone such as America/Chicago. A bare city name is rejected. candle_minutes sets the minutes before sunset for candle lighting, 10 to 60, default 18. City centre coordinates are enough, so do not ask for a home address. The tool returns only the coming Shabbat or holiday, not an arbitrary date.

Always pass explicit dates. The tools default to today in UTC.

A Jewish observance begins at sundown on the evening before the civil date listed for it, and entries named Erev mark that eve. When someone asks when a holiday is, give the evening it begins, the first listed day and the last day under the schedule used. For Shabbat times, give each time with its own date, name the time zone and the offset used, and include the Torah portion and readings if returned.

Times and dates are calculated. A community's published calendar may differ and takes precedence. The data does not say which days carry restrictions on work or how a community keeps them, so suggest asking a rabbi or synagogue when a question turns on practice. Keep the returned spelling of names and add a familiar English name, such as Passover for Pesach, where it helps.
