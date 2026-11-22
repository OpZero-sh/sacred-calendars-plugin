---
name: compare-observances
description: "Use when checking church seasons, Christian feasts, a Hebrew date, Jewish holidays, or overlap between observances."
---

Resolve the requested civil date or year. For a relative date, use the person’s local date when known, then send an explicit ISO date; the tools otherwise default to UTC. Use `liturgical_day` for one day, `moveable_feasts` for the year and `church_year_sundays` for a series of Sundays.

Use `hebrew_date` for a conversion and set `after_sunset` when the event is in the evening after local sunset. Use `jewish_holidays` with the requested start date, span and Israel or Diaspora calendar. If the convention would change the answer, label the assumption or show both.

Merge returned events by civil date and label each tradition. Preserve distinctions such as Western Easter and Orthodox Pascha; use the specific rite or rule reported by the source. For evening boundaries, describe when an observance begins and what civil day the listed date represents. For a single-tradition request call only its connector.
