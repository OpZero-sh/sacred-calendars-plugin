---
name: church-year
description: "Look up the Western church year: the season, Sunday or day name, liturgical colour and lectionary year for a date, the dates of Easter and the feasts that move with it for a year, Orthodox Pascha, and the names of the coming Sundays. Use when someone asks what Sunday it is, what season or colour applies, when Easter, Ash Wednesday, Pentecost or Advent falls, when Orthodox Easter is, or which lectionary year a date belongs to. Typical requests: 'what Sunday of the church year is this', 'when is Ash Wednesday in 2027', 'what colour is used in Advent', 'list the Sundays of Lent', 'when is Orthodox Pascha next year', 'which lectionary year starts this Advent'."
---

# Church year

Answer questions about the Christian liturgical calendar with the Liturgical Year connector. It is public, read only and needs no sign in. Dates are computed from the Easter rules, following common Western usage, with the date of Orthodox Pascha added.

## When to use

- A date and the question "what is this day in the church year".
- A year and the question "when is Easter" or another feast that moves with it.
- A run of Sundays, such as Advent or Lent.

Use `hebrew-calendar` for Jewish dates and holidays, `local-shabbat` for Shabbat times, and `compare-observances` when both calendars are wanted on one timeline.

## Tools

All three are on the Liturgical Year server.

| Tool | Returns | Arguments |
| --- | --- | --- |
| `liturgical_day` | Season, Sunday or day name, colour, major feast if any, Sunday lectionary year and Roman weekday cycle for one date | optional `date` as `YYYY-MM-DD` |
| `moveable_feasts` | Easter and the feasts that move with it, Christ the King, the First Sunday of Advent, and Orthodox Pascha, for one year | `year`, 1600 to 2400 |
| `church_year_sundays` | The coming Sundays from a date with name, season, colour and lectionary year | optional `date` as `YYYY-MM-DD`, optional `count` (1 to 12, default 6) |

What each field means, what the calendar leaves out and where churches differ are in [references/western-church-year.md](references/western-church-year.md).

## Workflow

1. Turn the request into an explicit date or year. The tools default to today in UTC, which can be a day off from the person's local date. When the request is relative, such as "this Sunday" or "today", work out the date in the person's own time zone if you know it and pass it as `YYYY-MM-DD`. If you do not know their date, say which date you used.
2. Pick the call.
   - One day: `liturgical_day`.
   - A feast in a given year: `moveable_feasts` with that year. A church season can span two calendar years, so for "next Easter" in late autumn use the following year.
   - A series of Sundays: `church_year_sundays` from the starting date. If the date is itself a Sunday, that Sunday is first in the list. For more than 12 Sundays, call again from the day after the last one returned.
3. Answer with the weekday and full date, the name as returned and the tradition it belongs to.

## Decision points

- **Easter.** If someone asks "when is Easter" without saying which, give Western Easter and Orthodox Pascha together, each labeled. `moveable_feasts` returns both.
- **Orthodox and Eastern churches.** The only Eastern date returned is Pascha. Seasons, Sunday names, colours and lectionary years are Western. Say so if the person belongs to an Eastern church, and do not present Western names as theirs. A date you work out by counting from Pascha is your own calculation and must be labeled that way.
- **Readings.** The tools give the lectionary year letter, not the readings. Do not state appointed readings as if the tool returned them. Point the person to their church's lectionary.
- **Saints' days and local feasts.** Not included. The result itself says customs vary and to check the parish calendar. Pass that on when a local feast might apply.
- **Colour.** Report it as returned, including alternatives such as purple or blue. Local use decides.

## Errors and empty results

- A year outside 1600 to 2400 returns an error stating the supported range. Say that the range is a limit of the service.
- A malformed date: reformat as `YYYY-MM-DD` and retry once.

## What the answer looks like

One or two sentences for a single date, or a short table for a list. Always the weekday and the full date. Name the tradition for anything that differs between churches. End with the caveat about local custom only when it is likely to matter.

## Examples

**"What Sunday of the church year is November 29, 2026?"**
Call `liturgical_day` with `date: "2026-11-29"`. Answer: the First Sunday of Advent, in the season of Advent, colour purple or blue, Sunday lectionary Year B, which begins that day.

**"When are Western Easter and Orthodox Pascha in 2027?"**
Call `moveable_feasts` with `year: 2027`. Give both dates with weekdays, labeled Western Easter and Orthodox Pascha.

**"List the Sundays of Lent in 2027."**
Call `moveable_feasts` with `year: 2027` to find Ash Wednesday, then `church_year_sundays` from that date with `count: 6`. Return the Sundays in Lent and Palm Sunday as a table with dates and colours.
