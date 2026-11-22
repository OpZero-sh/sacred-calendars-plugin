# Use Sacred Calendars with your assistant

Look up a church season, a Hebrew date or an upcoming holy day, and put observances from both calendars on the same civil timeline.

## ChatGPT and Codex

[Download the full portable package](https://raw.githubusercontent.com/OpZero-sh/sacred-calendars-plugin/downloads/sacred-calendars.zip). The full ZIP includes all connections for clients that support multi-server packages. ChatGPT’s developer dashboard connects one remote server per plugin. Use these individually packaged connections there. Each includes a workflow for that service.

[Liturgical Year](https://raw.githubusercontent.com/OpZero-sh/sacred-calendars-plugin/downloads/sacred-calendars--church.zip) · [Jewish Calendar](https://raw.githubusercontent.com/OpZero-sh/sacred-calendars-plugin/downloads/sacred-calendars--jewish.zip)

For a publisher or developer setup, open the OpenAI developer dashboard, choose **Upload plugin**, upload the one-connection ZIP and connect the declared MCP endpoint. People with an existing directory listing can install it directly in ChatGPT. For an OAuth-protected service select OAuth and complete its browser sign-in. Choose no authentication for a public service. Rebuild the archives from a checkout with `python3 scripts/build_openai.py ../plugin-zips`.

[OpenAI package guide](https://developers.openai.com/plugins/build/plugins) · [Upload and connection setup](https://developers.openai.com/plugins/deploy/submission)

## Claude

In Claude Code run `/plugin marketplace add OpZero-sh/plugins`, then `/plugin install sacred-calendars@opzero`. In Claude chat or Cowork, add the OpZero marketplace if available to your account and connect the services in the installed plugin’s **Connectors** tab.

## Grok Build

From a checkout of this repository, run `grok --plugin-dir .`. Open `/plugins` or `/mcps` to check the loaded capabilities. Grok Build reads the Claude-compatible plugin, its skills and MCP configuration. [Grok Build plugins](https://docs.x.ai/build/features/skills-plugins-marketplaces)

## Grok API

Preview a request locally with Python 3. Add `XAI_API_KEY` in your environment and omit `--dry-run` to send it. Use `--model` to select a model enabled for your account. The example requests a focused set of product tools; its tool list is in [grok-servers.json](integrations/grok-servers.json).

```sh
python3 integrations/grok_example.py --dry-run 'When are Western Easter and Orthodox Pascha in 2027?'
```

[Remote MCP tools in the xAI API](https://docs.x.ai/developers/tools/remote-mcp)

## Muse Code

From the repository root, validate and install the native plugin. Approve its public MCP connections, then start a new Muse session.

```sh
muse plugins validate .
muse plugins install .
muse plugins approve sacred-calendars
```

[Muse Code plugins](https://meta-models.github.io/muse-code-sdk/next/guides/plugins/reference/manifest/)
