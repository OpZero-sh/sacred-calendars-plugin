---
name: hebrew-calendar
description: "Convert a civil date to the Hebrew calendar and list Jewish holidays, fasts, Rosh Chodesh and special Shabbatot in a date range, for the Diaspora or Israel. Use when someone asks for the Hebrew date, when a Jewish holiday or fast falls, what the Torah portion is on a date, or which observances fall in a planning window. Typical requests: 'what is the Hebrew date today', 'when is Passover in 2027', 'when does Yom Kippur start', 'what Jewish holidays are in October', 'is anything on the Jewish calendar the week of April 20', 'what is this week's parasha'."
---

# Hebrew calendar

Answer questions about Hebrew dates and Jewish observances with the Jewish Calendar connector. It is public, read only and needs no sign in. The data comes from Hebcal.

Two facts shape every answer. A Hebrew day runs from sunset to sunset, so an observance begins on the evening before the civil date listed for it. And the holiday schedule differs between Israel and the Diaspora.

## When to use

- Converting a Gregorian date to its Hebrew date.
- Finding when a holiday or fast falls, or what falls in a range of dates.
- Finding the Torah portion connected to a date.

Use `local-shabbat` for candle lighting and Havdalah times at a place. Use `church-year` for Christian dates and `compare-observances` to set both calendars side by side.

## Tools

Both are on the Jewish Calendar server.

| Tool | Returns | Arguments |
| --- | --- | --- |
| `hebrew_date` | The Hebrew date for a Gregorian date, in English and Hebrew, with that day's events such as a holiday or the Torah portion | optional `date` as `YYYY-MM-DD`, optional `after_sunset` (default false) |
| `jewish_holidays` | Holidays, fasts, Rosh Chodesh and special Shabbatot in a range, each with its civil date, Hebrew date and a one line description | optional `start_date` as `YYYY-MM-DD`, `days` (1 to 366, default 60), `israel` (default false, meaning the Diaspora schedule), `major_only` (default false) |

How to read the listed dates, how the two schedules differ and what the data leaves out are in [references/hebrew-dates-and-holidays.md](references/hebrew-dates-and-holidays.md). Read it before answering a question about when an observance starts.

## Workflow

1. Turn the request into explicit dates. The tools default to today in UTC, which can be a day off from the person's local date. For "today" or "this week", work out the date where the person is if you know it, and pass it as `YYYY-MM-DD`. Otherwise say which date you used.
2. For a conversion, call `hebrew_date`. Set `after_sunset: true` when the moment in question is after local sunset, because the Hebrew date has then already moved to the next day. If the time of day matters and is unknown, give the daytime date and add that after sunset it becomes the next Hebrew day.
3. For a holiday, call `jewish_holidays` with a `start_date` shortly before the expected season and enough `days` to cover it. Use `major_only: true` when the person wants the main holidays and not every fast, new month and special Shabbat.
4. Choose the schedule. Use `israel: true` for someone in Israel. Otherwise the Diaspora schedule applies. If you do not know where the person observes and the answer differs, show both or state which you used.
5. Explain the start. A holiday listed on a civil date begins at sundown on the evening before. Entries named Erev mark that eve. For a fast that runs from sundown to nightfall, give both the evening it begins and the day it is observed.

## Decision points

- **"When is Passover?"** Give the evening it begins, the listed first day, and the last day under the schedule used. Do not give only the first listed date.
- **A Hebrew date to a civil date.** The tools convert from Gregorian to Hebrew only. A holiday can be found by listing a range. For an arbitrary Hebrew date, such as an anniversary, say that this connector cannot convert it directly. You may narrow it down by converting candidate civil dates, and you should say that is what you did.
- **More than a year.** One call covers at most 366 days. For a later year, set `start_date` in that year.
- **Practice.** The listing names the days. It does not say which days carry restrictions on work, or how a given community keeps them. Customs differ between communities and families. For anything that turns on practice, suggest asking a rabbi or the person's synagogue.
- **Spelling.** Holiday names come transliterated in Hebcal's spelling, such as Rosh Hashana and Pesach. Keep the returned spelling and add the common English name when it helps, such as Passover.

## Errors and empty results

- No entries in a range: say so, with the range and schedule used. With `major_only` set, try again without it before saying nothing falls there.
- A malformed date: reformat as `YYYY-MM-DD` and retry once.

## What the answer looks like

- The civil date with its weekday, the Hebrew date, and the name as returned.
- For any observance, when it begins in the evening and which schedule was used.
- A short table when several dates are listed.
- Credit Hebcal when listing data at length. The data is licensed CC BY 4.0.

Keep the tone factual and respectful. Describe an observance in the service's own short terms and do not explain someone's own tradition to them unless they ask.

## Examples

**"When is Passover in 2027?"**
Call `jewish_holidays` with `start_date: "2027-04-15"`, `days: 20` and `major_only: true`. The Diaspora result lists Erev Pesach on Wednesday, April 21, and Pesach I through VIII from Thursday, April 22 to Thursday, April 29. Answer that Passover begins at sundown on Wednesday, April 21, 2027 and ends at nightfall on Thursday, April 29 in the Diaspora, and that in Israel it is seven days, ending on Wednesday, April 28.

**"What is the Hebrew date for the evening of April 21, 2027?"**
Call `hebrew_date` with `date: "2027-04-21"` and `after_sunset: true`. The result is 15 Nisan 5787, the first day of Pesach. Mention that before sunset the same civil day is 14 Nisan.

**"What is this week's Torah portion?"**
Call `hebrew_date` for the coming Saturday's date. The events line names the parasha. For the readings and local times, use `local-shabbat`.
