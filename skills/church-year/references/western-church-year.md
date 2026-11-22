# The Western church year as the Liturgical Year service returns it

Facts in this file come from the Liturgical Year server: its tool results and its public guide at https://liturgical-year.mcp.opzero.sh/?page=docs. Sample values were returned by the service in November 2026.

## Source and scope

- Dates are computed on the service from the published Easter rules. No third party data is used.
- The calendar follows common Western usage, covering the Revised Common Lectionary and Roman usage. The date of Orthodox Pascha is added.
- Supported years: 1600 to 2400.
- With no date given, the tools use today in UTC.
- The service states that requests are not stored.

## Fields in a `liturgical_day` result

| Field | Meaning | Sample |
| --- | --- | --- |
| Date line | Weekday and full civil date | Sunday, November 29, 2026 |
| Season | The season of the church year | Advent. Christmas. Season after Epiphany. Lent. Holy Week. Season after Pentecost (Ordinary Time). |
| Day | The Sunday's name, a named day, or a general weekday label | First Sunday of Advent. Ash Wednesday. Christmastide. Ordinary Time. |
| Color | The usual liturgical colour, sometimes with an alternative | Purple or blue in Advent. Purple in Lent. White at Christmas. Green in Ordinary Time. |
| Feast | Present only on a major feast | Christmas Day, the Nativity of the Lord |
| Sunday lectionary year | A, B or C in the three year Sunday cycle | Year B |
| Roman weekday cycle | Year I or Year II of the two year weekday cycle in Roman usage | Year II |

Every result ends with the service's reminder that customs vary between churches and that the parish calendar decides local feasts.

Weekdays that are not named days get a general label. The days between Ash Wednesday and the First Sunday in Lent come back as "Lent, week 0". Report such a day in plain words, for example "the Thursday after Ash Wednesday, in Lent".

## What `moveable_feasts` lists for a year

In the order returned for 2027:

| Entry | 2027 date |
| --- | --- |
| Ash Wednesday | Wednesday, February 10 |
| Palm Sunday | Sunday, March 21 |
| Maundy Thursday | Thursday, March 25 |
| Good Friday | Friday, March 26 |
| Easter Day | Sunday, March 28 |
| Orthodox Pascha | Sunday, May 2 |
| Ascension Day | Thursday, May 6 |
| Pentecost | Sunday, May 16 |
| Trinity Sunday | Sunday, May 23 |
| Corpus Christi (Roman, Thursday) | Thursday, May 27 |
| Christ the King | Sunday, November 21 |
| First Sunday of Advent | Sunday, November 28 |

The 2027 dates are a sample. Always call the tool for the year asked about. All entries except Orthodox Pascha are Western dates. Ascension Day, Pentecost and Trinity Sunday in the list count from Western Easter.

## What `church_year_sundays` returns

Each Sunday has its name, season, colour and lectionary year. Names can carry a second name in parentheses where usage differs, such as "The Baptism of the Lord (First Sunday after Epiphany)", "Last Sunday after Epiphany (Transfiguration Sunday in the Revised Common Lectionary)", "Palm Sunday (the Sunday of the Passion)" and "Christ the King (Reign of Christ)". Keep the parenthesis when the person's tradition is unknown.

The list starts with the given date if it is a Sunday, otherwise with the next Sunday. One call returns at most 12.

## The lectionary year

- The Sunday lectionary year changes on the First Sunday of Advent. In live results, Christ the King on November 22, 2026 is in Year A, and the First Sunday of Advent a week later is in Year B.
- The Roman weekday cycle is a separate two year cycle and is reported separately.
- The service returns the letter of the year only. It does not return readings. Lectionaries are published by church bodies, and the readings must come from the person's own lectionary.

## What is not included

- Appointed readings, psalms and collects.
- Saints' days, patronal feasts and other local observances.
- Transferred feasts. Where a church moves a feast to the nearest Sunday, the service still reports the traditional day. Corpus Christi, for example, is listed on its Thursday.
- The Eastern cycle apart from the date of Pascha: no Eastern seasons, Sunday names, fasts or fixed feasts, and nothing for churches that keep fixed feasts by the Julian calendar.

## Where churches differ

State these as differences of practice, not as right and wrong.

- **Easter.** Western churches and most Orthodox churches compute Easter by different calendars, so the dates often differ and sometimes coincide. Give both when the person's tradition is unknown.
- **Names of Sundays.** Sundays after Epiphany and after Pentecost are counted and named in several ways, and some traditions use the term Ordinary Time.
- **Colours.** Blue or purple in Advent is one common variation. There are others, and some churches use no liturgical colours.
- **Whether a calendar is kept at all.** Many churches keep only Christmas and Easter, or no fixed calendar. Offer the information without assuming the person's church follows it.
