# Stacks Extensions for Claude

Helps Claude build RapidWeaver pages with the stacks from
[stacks-extensions.de](https://stacks-extensions.de/), driving the Stacks app
through its built-in MCP server.

Without this plugin, Claude has to guess what a stack's settings are called.
The settings of a commercial stack are not readable from the bundle, and a
wrongly named setting is rejected without an error message. This plugin carries
the exact field names, the accepted values and the pitfalls for each stack.

## What is covered

| Skill | Stack |
|---|---|
| `doorman` | Doorman — a login in front of a page, plus two-factor (TOTP) codes |

More stacks follow.

## Requirements

- The **Stacks app** (standalone), with its MCP server registered in Claude.
- The stack itself, installed in the library the Stacks app reads:
  `~/Library/Application Support/Stacks/Stacks/`. A stack installed only for
  RapidWeaver Classic sits in a different folder and stays invisible to the app.

## Installing

Either add the marketplace and install from it, which also brings updates:

```
claude plugin marketplace add MarceloLang/stacks-extensions
claude plugin install stacks-extensions@stacks-extensions
```

Or install the `.plugin` file from the download area: open it and confirm.
That way needs no git, but updates have to be fetched by hand.

## Updating

```
claude plugin update stacks-extensions@stacks-extensions
```

Give the full `plugin@marketplace` name. The short form is refused with
"Plugin not found". Claude has to be restarted afterwards for the new version
to take effect.

If you installed the `.plugin` file instead, download the current one and open
it again.

## Licence

MIT. The stacks themselves are sold separately; this plugin only documents them.
