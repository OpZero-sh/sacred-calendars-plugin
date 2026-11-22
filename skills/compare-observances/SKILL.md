---
name: compare-observances
description: "Put Christian and Jewish observances on one civil timeline and check for overlap. Use when someone is planning an event, a school or work calendar, or an interfaith gathering and needs to know what falls when in both calendars, or asks whether two observances coincide. Typical requests: 'do Passover and Easter overlap in 2027', 'what religious holidays fall in the week of April 20', 'find a date in April that avoids Holy Week and Passover', 'show Christian and Jewish holidays for next spring side by side', 'is the evening of the 21st a problem for anyone'."
---

# Compare observances

Build one dated list from two calendars: the Western church year with Orthodox Pascha, from the Liturgical Year connector, and the Jewish calendar, from the Jewish Calendar connector. Both are public, read only and need no sign in.

The two calendars count days differently. A Jewish observance begins at sundown on the evening before its listed date. A date that looks clear on a civil calendar may not be. Getting that boundary right is the point of this skill.

## When to use

- A planning window and the question of what falls in it for both traditions.
- A question about whether two named observances coincide in a given year.

For a question about one tradition only, use `church-year` or `hebrew-calendar` and call only that connector. For Shabbat times at a place, use `local-shabbat`.

## Tools

| Tool | Server | Use it for |
| --- | --- | --- |
| `moveable_feasts` | Liturgical Year | Easter, the feasts that move with it, Advent, and Orthodox Pascha for a `year` |
| `liturgical_day` | Liturgical Year | Season, day name and any major feast for one `date` |
| `church_year_sundays` | Liturgical Year | Sundays from a `date`, up to 12 per call |
| `jewish_holidays` | Jewish Calendar | Holidays and fasts from a `start_date` for a number of `days`, with `israel` and `major_only` options |
| `hebrew_date` | Jewish Calendar | The Hebrew date and events for one `date`, with `after_sunset` |

The merge rules, a worked example and an answer template are in [references/merging-two-calendars.md](references/merging-two-calendars.md). Read it before writing a merged list.

## Workflow

1. Fix the window as explicit civil dates, and the place. The tools default to today in UTC, so always pass dates. Ask whether the Jewish dates should follow the Diaspora or the Israel schedule if the place does not make it obvious. If the person cannot say, use the Diaspora schedule and state it.
2. Query each tradition on its own.
   - Christian: `moveable_feasts` for each calendar year the window touches. Add `liturgical_day` for specific dates, such as a proposed event date, to catch fixed feasts like Christmas Day.
   - Jewish: `jewish_holidays` with the window's first day as `start_date` and its length as `days`. Start one day early so that an eve falling just before the window is not missed. Leave `major_only` off for planning, so that fasts are included.
3. Normalize the Jewish entries. For each one, record the evening it begins, which is the evening of the civil date before the listed date, and the listed date itself.
4. Merge by civil date into one table. Label every row with its tradition: Western Christian, Orthodox, or Jewish with the schedule used.
5. Check overlap from the returned records only. Two observances overlap when their dated spans share a day or an evening. Similar names or a shared season are not evidence.
6. Answer the planning question. If a proposed date or evening falls inside any span, say which, for whom, and from when to when.

## Decision points

- **Western and Orthodox.** Keep Western Easter and Orthodox Pascha as separate rows. Only Pascha is returned for the Eastern calendar. Do not present Western dates for Holy Week, Ascension or Pentecost as Orthodox dates.
- **Evening events.** For an evening event, call `hebrew_date` with `after_sunset: true` for that date to see whether the evening already belongs to a holiday.
- **Which observances matter.** The data lists days. It does not say how strictly anyone keeps them or which days people will be unavailable. Present the dates and suggest the organizer ask the people or communities involved.
- **Fixed Christian feasts.** `moveable_feasts` does not list fixed dates such as Christmas or Epiphany, and saints' days and local feasts are not in the data at all. Say so if the window may contain them.
- **Other traditions.** Only these two calendars are available. If the person asks about Muslim, Hindu or other observances, say this plugin does not cover them and do not supply dates from memory as if looked up.

## Errors and empty results

- Years outside 1600 to 2400 are not supported by the church calendar.
- A Jewish listing covers at most 366 days per call. Split a longer window.
- An empty result for one tradition is a real answer. Report it with the range and schedule used.

## What the answer looks like

A table in date order, then a plain statement about overlap, then the limits.

| Civil date | Begins | Observance | Tradition |
| --- | --- | --- | --- |
| weekday and date | "at sundown the evening before" for Jewish entries, "that day" otherwise | name as returned | Western Christian, Orthodox, or Jewish (Diaspora or Israel) |

Use neutral, equal wording for both traditions. Do not describe one calendar in terms of the other.

## Examples

**"Do Passover and Easter overlap in 2027?"**
Call `moveable_feasts` with `year: 2027` and `jewish_holidays` with `start_date: "2027-03-20"` and `days: 50`. Western Easter is Sunday, March 28. Passover begins at sundown on Wednesday, April 21 and runs through Thursday, April 29 in the Diaspora. Orthodox Pascha is Sunday, May 2. Answer that in 2027 Passover does not overlap Western Easter and ends three days before Orthodox Pascha.

**"We want an evening event on Wednesday, April 21, 2027. Any conflicts?"**
Call `hebrew_date` with `date: "2027-04-21"` and `after_sunset: true`. The evening is the start of the first day of Pesach. Call `liturgical_day` for the same date for the Christian calendar. Report the Passover conflict clearly, give its span, and report what the church calendar shows for that day.

**"What falls in the last two weeks of December 2026?"**
Call `jewish_holidays` from `2026-12-17` for 16 days and `liturgical_day` for December 25. Merge and label. Note that fixed Christian dates other than those checked, and local feasts, are not listed by the tools.
