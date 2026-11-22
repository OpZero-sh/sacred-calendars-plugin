---
name: use-church
description: "Look up the Western church year: the season, Sunday name, colour and lectionary year for a date, the date of Easter and the feasts that move with it, Orthodox Pascha, or a series of coming Sundays."
---

Liturgical Year is public and read only. It computes the calendar from the Easter rules, following common Western usage, for the years 1600 to 2400.

1. For one day, call liturgical_day with date as YYYY-MM-DD. It returns the season, the Sunday or day name, the colour, a major feast if there is one, the Sunday lectionary year and the Roman weekday cycle.
2. For a year, call moveable_feasts with year. It lists Ash Wednesday, Palm Sunday, Maundy Thursday, Good Friday, Easter Day, Orthodox Pascha, Ascension Day, Pentecost, Trinity Sunday, Corpus Christi, Christ the King and the First Sunday of Advent.
3. For a run of Sundays, call church_year_sundays with a starting date and count, up to 12.

Always pass an explicit date. The tools default to today in UTC, which can differ from the person's local date. Say which date you used when the request was relative.

Give the weekday and full date with every answer. When someone asks when Easter is without saying which, give Western Easter and Orthodox Pascha together and label each. Pascha is the only Eastern date returned: seasons, Sunday names, colours and lectionary years are Western, so do not present them as Orthodox usage.

The tools return the lectionary year letter and not the readings. Do not state appointed readings as if the tool returned them. Saints' days, local feasts and transferred feasts are not included. Report colours as returned, including alternatives such as purple or blue. Customs vary between churches, and the person's own parish calendar decides.
