---
name: local-shabbat
description: "Get candle lighting and Havdalah times and the Torah portion for the coming Shabbat or holiday at a particular place. Use when someone asks when Shabbat starts or ends where they are, what time to light candles, when Havdalah is, or what this week's parasha and haftarah are. Typical requests: 'what time is candle lighting in Chicago this Friday', 'when does Shabbat end in Jerusalem', 'Shabbat times for 41.88, -87.63', 'what is the Torah portion this week', 'candle lighting 40 minutes before sunset in Jerusalem'."
---

# Local Shabbat times

Return candle lighting and Havdalah times for the coming Shabbat or holiday at a location, with the Torah portion, using the Jewish Calendar connector. It is public, read only and needs no sign in. The data comes from Hebcal.

Times are calculated. A community's own published calendar may differ, and it takes precedence.

## When to use

- Someone needs the start or end time of the coming Shabbat or holiday in a named place.
- Someone asks for this week's Torah portion and readings.

Use `hebrew-calendar` for dates of holidays and Hebrew date conversion. This skill cannot give times for an arbitrary past or future date.

## Tool

`shabbat_times` on the Jewish Calendar server.

| Argument | Required | Notes |
| --- | --- | --- |
| `latitude` | yes | Decimal degrees, north positive |
| `longitude` | yes | Decimal degrees, east positive, so the Americas are negative |
| `time_zone` | yes | An IANA name such as `America/Chicago` or `Asia/Jerusalem`. A bare city name is rejected. |
| `candle_minutes` | no | Minutes before sunset for candle lighting, 10 to 60. Default 18. |

What the result contains, the defaults behind it and its limits are in [references/shabbat-times.md](references/shabbat-times.md).

## Workflow

1. Settle the place. Use coordinates the person supplies. If they name a city, use the city centre coordinates and its IANA time zone, and state the place you used. A city level answer does not need a street address, so do not ask for one.
2. If the place is ambiguous, such as Springfield or Portland, ask which one. If the person gives only a country or a large region, ask for a city, because times vary across it.
3. Pass `candle_minutes` only when the person asks for a specific offset or names a custom that uses one. Otherwise leave the default.
4. Call `shabbat_times`.
5. Report the candle lighting time with its date, the Havdalah time with its date, the time zone, the offset used, and the Torah portion with its Torah and Haftarah readings if returned.

## Decision points

- **A date other than the coming Shabbat.** The tool returns only the coming Shabbat or holiday. If someone asks about a later week, say so, give the dates the result actually covers, and do not estimate later times.
- **A holiday in the coming days.** The result may be for a holiday instead of, or as well as, Shabbat. Read the dates and labels in the result and report them as they are.
- **Community custom.** Customs for candle lighting and for the end of Shabbat differ. If the person follows their synagogue's calendar, that calendar governs. Offer the calculated times as a reference.
- **High latitudes and unusual cases.** Where sunset is very late, very early or absent, calculated times may be missing or impractical. Report what was returned and suggest asking a local rabbi.
- **Reading the clock.** Times come back in the local time of the zone you passed, in the format the service uses for that region, either 12 hour or 24 hour. Keep the format and name the zone.

## Errors and empty results

- "Unknown time zone": pass the IANA name, such as `America/Chicago`, and retry.
- Coordinates out of range: latitude runs from -90 to 90 and longitude from -180 to 180. A common slip is a missing minus sign for western longitudes.
- `candle_minutes` outside 10 to 60 is rejected. Tell the person the allowed range.

## What the answer looks like

```
Shabbat in <place> (<time zone>)
Candle lighting: <time>, <weekday, date>  (<N> minutes before sunset)
Havdalah: <time>, <weekday, date>
Torah portion: <name>. Torah reading: <reference>. Haftarah: <reference>.
Calculated times from Hebcal. Follow your community's calendar where it differs.
```

Keep the last line. Do not add greetings or commentary on observance unless the person's own message invites it.

## Examples

**"What time is candle lighting for the coming Shabbat in Chicago? Use 41.88, -87.63 and America/Chicago."**
Call `shabbat_times` with those three values. Report candle lighting on Friday and Havdalah on Saturday with their dates, name the time zone, say the default of 18 minutes before sunset was used, and give the Torah portion.

**"When does Shabbat end in Jerusalem this week?"**
Use the city centre, about 31.78 and 35.22, with `Asia/Jerusalem`. Report the Havdalah time and date as returned, in 24 hour format, and note that local custom in Jerusalem may differ from the calculated time.

**"Candle lighting in Portland three weeks from now?"**
Ask which Portland. Then explain that the tool gives only the coming Shabbat, offer those times, and suggest checking again nearer the date or consulting a published community calendar.
