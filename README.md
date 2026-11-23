# Sacred Calendars

Look up a church season, a Hebrew date or an upcoming holy day, and put observances from both calendars on the same civil timeline.

[Connect with Claude, ChatGPT, Muse Code, or Grok](PROVIDERS.md)

Plan a community event around Passover and Easter, find the Sundays in Advent, or get candle lighting and Havdalah times for the coming Shabbat. Calendar entries keep their own traditions and local timing, so an evening observance is easy to distinguish from the civil date printed on an invitation.

## Try it

- “When are Western Easter and Orthodox Pascha in 2027?”
- “When does Passover begin and end in 2027?”
- “List the major Jewish holidays in the Diaspora during April 2027 and show which overlap Holy Week.”
- “What time is candle lighting for the coming Shabbat in Chicago? Use 41.88, -87.63 and America/Chicago.”

## Get started

In Claude Code, run these commands in a session and reload plugins if prompted.

```text
/plugin marketplace add OpZero-sh/plugins
/plugin install sacred-calendars@opzero
```

In Claude chat or Cowork, open the installed plugin’s Connectors tab and connect Liturgical Year and Jewish Calendar. Both are public and need no sign in.

## What is included

### Skills

| Skill | What it does |
| --- | --- |
| `church-year` | Gives the season, Sunday name, colour and lectionary year for a date, the dates of Easter and the feasts that move with it, Orthodox Pascha, and the coming Sundays. |
| `hebrew-calendar` | Converts a civil date to the Hebrew calendar and lists Jewish holidays, fasts, new months and special Shabbatot for the Diaspora or Israel, with the evening each one begins. |
| `local-shabbat` | Gives candle lighting and Havdalah times and the Torah portion for the coming Shabbat or holiday at a place. |
| `compare-observances` | Puts both calendars on one civil timeline, labels each entry by tradition, and checks for overlap, including evening starts. |

Each skill folder has a reference file with the data source, field meanings, verified sample results and limits the skill relies on.

### Agent

`calendar-researcher` is a read only researcher for planning questions that need several lookups. It queries each calendar on its own, records when each observance begins, and returns one dated table with overlaps and a list of what the data does not cover.

### Hooks

None. Every tool in this plugin is read only, so there is nothing to confirm or guard.

## What the plugin connects to and runs

The plugin talks to two remote MCP servers run by OpZero. It contacts no other host during normal use, and it runs no scripts on your machine.

| Connector | Host | Sign in | What it receives |
| --- | --- | --- | --- |
| Liturgical Year | `liturgical-year.mcp.opzero.sh` | None | The date or year you ask about |
| Jewish Calendar | `jewish-calendar.mcp.opzero.sh` | None | The date or date range, the Israel or Diaspora choice, and for Shabbat times the coordinates, time zone and candle lighting offset you supply |

Both services state that they do not store requests. City centre coordinates are enough for a city level answer, so there is no need to give a home address. The church calendar is computed on the server. The Jewish Calendar server draws its data from Hebcal and keeps a cached copy of that public data.

The repository also holds settings files for other assistants. Claude does not run them, and nothing in the plugin calls them. The two scripts that use them are not in this repository. They live in the catalog repository, [OpZero-sh/plugins](https://github.com/OpZero-sh/plugins).

- The catalog's `tools/build_openai.py` builds ZIP packages for ChatGPT and Codex from this repository's skills, license, the product icon and `integrations/openai`. It reads local files and writes ZIP files to the folder you name. It uses no network.
- The catalog's `tools/grok_example.py` is an optional example for the xAI API. It reads `integrations/grok-servers.json` and `XAI_API_KEY` from your environment and sends one request to `api.x.ai` only when you run it yourself without the dry run flag. With the dry run flag it prints the request and sends nothing.
- The JSON files under `integrations/` are settings for those assistants. They list the same two hosts.

## Sources and limits

- Church year: computed from the Easter rules, following common Western usage, for the years 1600 to 2400. Orthodox Pascha is the only Eastern date. Readings, saints’ days and local feasts are not included. Customs vary between churches.
- Jewish calendar: data from Hebcal.com, licensed CC BY 4.0. Dates and times are calculated and may differ from a community’s published calendar, which takes precedence. Shabbat times are available only for the coming Shabbat or holiday.
- The plugin covers these two calendars only.

## In use

Examples from the connected services in Claude.

![A Gregorian date and its Hebrew equivalent](media/hebrew-date.webp)

- [The first Sunday of Advent](media/advent.webp)
