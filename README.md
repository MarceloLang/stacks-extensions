# Stacks Extensions — Claude marketplace

A Claude Code marketplace for the RapidWeaver stacks sold at
[stacks-extensions.de](https://stacks-extensions.de/).

The Stacks app ships an MCP server, so Claude can build RapidWeaver pages
directly. What Claude cannot do is guess what a stack's settings are called:
the settings of a stack are not readable from its bundle, and a wrongly named
setting is rejected without an error message. The plugin in this repository
supplies those names, their accepted values, and the pitfalls, one skill per
stack.

## Installing

```
claude plugin marketplace add MarceloLang/stacks-extensions
claude plugin install stacks-extensions@stacks-extensions
```

Updating later:

```
claude plugin update stacks-extensions@stacks-extensions
```

Give the full `plugin@marketplace` name; the short form is refused. Claude has
to be restarted afterwards.

Not a git user? The same plugin is offered as a single `.plugin` file in the
download area of the shop. Open it and confirm, no commands involved.

## What is in here

| Path | |
|---|---|
| `.claude-plugin/marketplace.json` | the marketplace manifest |
| `plugins/stacks-extensions/` | the plugin itself, one skill per stack |

The skill files are generated from each stack's own `Info.plist` when a version
is released, so the settings they list cannot drift from the version being
shipped.

## Licence

MIT. The stacks themselves are sold separately; this only documents them.
