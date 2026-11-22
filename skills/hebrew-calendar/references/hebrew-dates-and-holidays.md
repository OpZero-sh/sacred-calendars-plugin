# Hebrew dates and Jewish holidays as the Jewish Calendar service returns them

Facts in this file come from the Jewish Calendar server: its tool results and its public guide at https://jewish-calendar.mcp.opzero.sh/?page=docs. Sample values were returned by the service in November 2026.

## Source and scope

- Data comes from Hebcal.com and is licensed CC BY 4.0. Credit it as "Jewish calendar data by Hebcal.com" when reproducing listings at length.
- The service keeps a cached copy of the public data and states that requests are not stored.
- With no date given, the tools use today in UTC.
- A holiday listing covers at most 366 days per request.
- The service's terms say that times and dates are calculated and may differ from a community's published calendar, and to follow one's rabbi or synagogue.

## A `hebrew_date` result

| Part | Sample |
| --- | --- |
| Summary line | Sat, Nov 28, 2026 is 18 Kislev 5787. |
| Hebrew date | 18 Kislev 5787 |
| In Hebrew | The same date in Hebrew script |
| Events | Parashat Vayishlach on a Shabbat. A holiday name on a holiday, such as Pesach I. |

The events line lists what falls on the day, such as a holiday or, on Shabbat, the weekly Torah portion.

## The day begins at sunset

A Hebrew calendar day starts at sunset and runs to the next sunset. One civil date therefore touches two Hebrew dates.

A live example:

| Call | Result |
| --- | --- |
| `jewish_holidays`, Diaspora | Erev Pesach on Wed, Apr 21, 2027, 14 Nisan 5787. Pesach I on Thu, Apr 22, 2027, 15 Nisan 5787. |
| `hebrew_date` for 2027-04-21 with `after_sunset: true` | 15 Nisan 5787, with the event Pesach I |

So the date printed beside a holiday is the civil date of its daytime. The observance begins at sundown on the civil date before. An entry named Erev marks that eve.

Rules for answers:

- State the evening an observance begins and the day it is listed on. "Begins at sundown on Wednesday, April 21, 2027. The first day is Thursday, April 22."
- For an event planned in the evening, check both the civil date and the following Hebrew day. An evening event on the date before a listed holiday falls inside the holiday.
- Shabbat follows the same pattern every week: it begins Friday evening and ends Saturday night.
- Use `after_sunset: true` only when the time in question is after local sunset. The tool does not know the place or the hour.

## Israel and the Diaspora

The `israel` argument selects the schedule. The default is the Diaspora schedule. The two differ in the number of festival days.

Live results for Pesach in 2027:

| Schedule | Listed days | Days marked CH''M |
| --- | --- | --- |
| Diaspora | Pesach I to VIII, Thu, Apr 22 to Thu, Apr 29 | III to VI |
| Israel | Pesach I to VII, Thu, Apr 22 to Wed, Apr 28 | II to VI |

CH''M is Hebcal's abbreviation for Chol HaMoed, the intermediate days of a festival.

For the autumn festivals of 2027 the Diaspora listing has Shmini Atzeret on Sat, Oct 23 and Simchat Torah on Sun, Oct 24 as separate days, and its description notes that in Israel the two are combined.

Rules for answers:

- Name the schedule used in every holiday answer.
- If the person's location is unknown and the schedules differ for the dates asked about, show both.
- Individual practice can differ from the schedule of the place. If someone says how they observe, follow what they say.

## What `major_only` changes

Without it, a range includes minor fasts, Rosh Chodesh and special Shabbatot as well as the major holidays. In the 2027 sample, the Fast of the First Born (Ta'anit Bechorot) appears beside Erev Pesach in the full listing. With `major_only: true` the list is limited to major holidays and their eves. Use the full list for planning, where a fast day or a new month may matter, and the short list for a quick answer.

## A sample of how a holiday season is listed

Diaspora, autumn 2027, `major_only: true`:

| Entry | Civil date | Hebrew date |
| --- | --- | --- |
| Erev Rosh Hashana | Fri, Oct 1, 2027 | 29 Elul 5787 |
| Rosh Hashana 5788 | Sat, Oct 2, 2027 | 1 Tishrei 5788 |
| Rosh Hashana II | Sun, Oct 3, 2027 | 2 Tishrei 5788 |
| Erev Yom Kippur | Sun, Oct 10, 2027 | 9 Tishrei 5788 |
| Yom Kippur | Mon, Oct 11, 2027 | 10 Tishrei 5788 |
| Erev Sukkot | Fri, Oct 15, 2027 | 14 Tishrei 5788 |
| Sukkot I | Sat, Oct 16, 2027 | 15 Tishrei 5788 |
| Shmini Atzeret | Sat, Oct 23, 2027 | 22 Tishrei 5788 |
| Simchat Torah | Sun, Oct 24, 2027 | 23 Tishrei 5788 |

The rows between Sukkot I and Shmini Atzeret are left out here. These dates are a sample. Always call the tool for the dates asked about.

Each entry also carries a one line description from Hebcal. Use it as the description of the day. The entry for Erev Yom Kippur, for instance, says that the fast begins at sundown and continues for 25 hours.

## What the data does not say

- Which days carry restrictions on work, travel or writing, and how strictly a given community keeps them.
- Local customs, community events, or the times of services.
- Sunset or nightfall times. Those depend on place. `shabbat_times` gives candle lighting and Havdalah for the coming Shabbat or holiday at given coordinates.
- A conversion from a Hebrew date to a civil date. The tools go from Gregorian to Hebrew only.

When a question turns on any of these, say that the calendar data does not settle it and suggest asking a rabbi or the person's synagogue.

## Spelling

Names are transliterated in Hebcal's spelling: Rosh Hashana, Pesach, Sukkot, Shmini Atzeret, Kislev, Tishrei. Other spellings are common and equally valid. Keep the returned spelling in data and add a familiar English name where it helps a general reader, such as Passover for Pesach or the Day of Atonement for Yom Kippur.
