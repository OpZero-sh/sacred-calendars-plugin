# Shabbat times as the Jewish Calendar service returns them

Facts in this file come from the Jewish Calendar server: its tool results and its public guide at https://jewish-calendar.mcp.opzero.sh/?page=docs. Sample values were returned by the service in November 2026.

## Source

- Data comes from Hebcal.com, licensed CC BY 4.0.
- The service states that requests are not stored. A request carries coordinates, a time zone and the candle lighting offset.
- City centre coordinates are enough for a city level answer. Do not ask for or send a home address.

## A sample result

For latitude 41.88, longitude -87.63, time zone America/Chicago, with the default offset:

| Line | Value |
| --- | --- |
| Heading | Shabbat times for 41.88, -87.63 (America/Chicago) |
| Candle lighting | 4:03pm (Fri, Nov 27, 2026) |
| Torah portion | Parashat Vayishlach (Sat, Nov 28, 2026, 18 Kislev 5787) |
| Torah reading | Genesis 32:4-36:43 |
| Haftarah | Obadiah 1:1-21 |
| Havdalah | 5:07pm (Sat, Nov 28, 2026) |
| Closing line | Calculated times; follow your community calendar. |

The same week for Jerusalem, with Asia/Jerusalem, came back in 24 hour format: candle lighting 16:15 and Havdalah 17:14.

## Defaults and options

- Candle lighting defaults to 18 minutes before sunset. `candle_minutes` accepts 10 to 60.
- The service's guide says Havdalah is given at 50 minutes after sunset, and that Hebcal applies local custom in some places, such as Jerusalem.
- There is no argument for the Havdalah offset and none for a date. The result is always for the coming Shabbat or holiday.
- `time_zone` must be an IANA name. A bare city name returns an error that suggests the right form.

## Reading the result

- The heading echoes the coordinates and the zone. It does not name the city. Add the place name yourself and say it is the place you assumed.
- Each time carries its own date. Use those dates in the answer. Do not assume Friday and Saturday, since the coming occasion may be a holiday on other days.
- The Torah portion line gives the civil date and the Hebrew date of the Shabbat. Reading references use the service's chapter and verse form.
- The Torah portion and Haftarah shown follow Hebcal's defaults for the schedule it applies. Communities differ on some Haftarah readings, and the cycle in Israel can run a week apart from the Diaspora at certain times of year. If a person reports a different reading, theirs may be right for their community.

## Limits

- Only the coming Shabbat or holiday. No past dates, no dates further ahead.
- Times are calculated from coordinates. Elevation, horizon and local rulings can shift the practical time.
- The service's terms say calculated times may differ from a community's published calendar, and to follow one's rabbi or synagogue.

## Wording

- Say "calculated" for the times.
- Name the offset used for candle lighting.
- Keep Hebcal's spelling of the portion name and add nothing to the reading references.
- Do not tell anyone what they must do or by when. Give the times and the source, and leave practice to them and their community.
