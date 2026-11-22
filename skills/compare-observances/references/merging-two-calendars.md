# Merging the church year and the Jewish calendar on one timeline

Facts in this file come from the Liturgical Year and Jewish Calendar servers: their tool results and their public guides at https://liturgical-year.mcp.opzero.sh/?page=docs and https://jewish-calendar.mcp.opzero.sh/?page=docs. Sample values were returned by the services in November 2026.

## What each side can and cannot supply

| | Church year (Liturgical Year) | Jewish calendar (Jewish Calendar) |
| --- | --- | --- |
| Source | Computed from the Easter rules. No third party data. | Hebcal.com, CC BY 4.0 |
| Scope | Common Western usage, plus the date of Orthodox Pascha | Holidays, fasts, Rosh Chodesh, special Shabbatot. Diaspora or Israel schedule. |
| Range | Years 1600 to 2400 | Up to 366 days per request |
| Day boundary | Civil dates | Each listed date is the civil date of the daytime. The observance begins at sundown the evening before. |
| Not included | Readings, saints' days, local and transferred feasts, the Eastern cycle other than Pascha | Which days carry work restrictions, community custom, local times other than the coming Shabbat |
| Default date | Today in UTC | Today in UTC |

Both services state that requests are not stored.

## Merge rules

1. **Pass explicit dates to every call.** Never rely on the default, since the two services and the person may be on different sides of midnight.
2. **Query each tradition separately.** Do not infer one calendar from the other. The two are computed by unrelated rules.
3. **Give every Jewish entry two points in time:** the evening it begins and the civil date it is listed on. An entry named Erev already marks the eve. For multi day festivals, record the first evening and the last listed day.
4. **Label every row with its tradition.** Use Western Christian, Orthodox, and Jewish with Diaspora or Israel. Western dates serve Catholic and Protestant churches alike, with local variation.
5. **Keep Western Easter and Orthodox Pascha apart.** They are separate rows even in a year when the dates coincide.
6. **Decide overlap from spans, not from names.** Two observances overlap if any evening or day is shared.
7. **State the schedule and the place assumed.** If Diaspora and Israel differ for the window, say how.
8. **State what was not checked.** Fixed Christian feasts appear only if a date was looked up with `liturgical_day`. Local feasts and other religions' calendars are not available.

## A worked example from live results: spring 2027

Returned by `moveable_feasts` for 2027 and by `jewish_holidays` for the Diaspora:

| Civil date | Begins | Observance | Tradition |
| --- | --- | --- | --- |
| Sun, Mar 21, 2027 | that day | Palm Sunday | Western Christian |
| Thu, Mar 25, 2027 | that day | Maundy Thursday | Western Christian |
| Fri, Mar 26, 2027 | that day | Good Friday | Western Christian |
| Sun, Mar 28, 2027 | that day | Easter Day | Western Christian |
| Wed, Apr 21, 2027 | daytime | Erev Pesach, and the Fast of the First Born | Jewish (Diaspora) |
| Thu, Apr 22, 2027 | at sundown on Wed, Apr 21 | Pesach I | Jewish (Diaspora) |
| Thu, Apr 29, 2027 | continues from Apr 22 | Pesach VIII, the last day | Jewish (Diaspora) |
| Sun, May 2, 2027 | that day | Orthodox Pascha | Orthodox |

Reading it:

- Passover in 2027 begins at sundown on Wednesday, April 21 and its last day in the Diaspora is Thursday, April 29. On the Israel schedule the last day is Wednesday, April 28.
- Western Holy Week and Easter fall more than three weeks earlier and do not overlap Passover.
- Orthodox Pascha falls three days after the last day of Passover in the Diaspora.
- An evening event on Wednesday, April 21 falls on the first night of Passover, although the civil calendar shows the holiday on April 22. `hebrew_date` for that date with `after_sunset: true` confirms it: 15 Nisan 5787, Pesach I.

Other years differ. Always run the calls for the year in question.

## Answer template

```
Window: <first date> to <last date>. Jewish dates use the <Diaspora | Israel> schedule.

| Civil date | Begins | Observance | Tradition |
| ... |

Overlap: <plain statement, naming the days or evenings shared, or that none are>.
For your date: <whether the proposed day or evening falls inside any span, and whose>.
Not covered: readings, saints' days and local feasts, the Orthodox calendar apart from Pascha, how individual communities keep each day, and other religions' calendars.
Sources: church year computed by Liturgical Year. Jewish calendar data by Hebcal.com (CC BY 4.0).
```

## Tone

- Describe each observance in its own terms, with the name the service returned. Add a familiar English name where a general reader needs it.
- Do not explain one tradition through the other, and do not suggest that one calendar is derived from, or fulfilled by, the other.
- Do not guess who will or will not attend an event. Give the dates and suggest the organizer ask.
- Customs vary within each tradition. Where it matters, say that the person's own community calendar decides.
