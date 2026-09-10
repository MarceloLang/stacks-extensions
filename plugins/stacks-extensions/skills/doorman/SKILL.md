---
name: doorman
description: Use when building or editing a RapidWeaver page that uses the Doorman stack in the Stacks app — putting a login in front of a page, managing two-factor (TOTP) codes, or setting Doorman's appearance, security and button options. Also use when the user mentions "Doorman", a login stack, a TOTP or authenticator stack, or asks why a Doorman page shows a setup form instead of a login.
metadata:
  documents-stack-version: "1.0.2"
  vendor: stacks-extensions.de
---

# Doorman

Doorman puts a login in front of a page and manages the two-factor codes (TOTP)
of the user's services behind it. Everything runs on their own server, nothing
is handed to a third party.

- Login with a password, stored as a hash
- Two-factor codes worked out on the server, with an expiry ring and one-click copy
- Add accounts by key or QR code, rename them, move them to an archive
- Change the password while running, or reset it from the stack settings

Full settings table: [references/fields.md](references/fields.md). Look field
names up there rather than guessing — a wrong name fails silently (see below).

## Two rules that decide whether your first attempt works

**1. When setting a property through the Stacks MCP, use the short field name,
not the `custom.` path.** Reading a placed stack returns both a `uid`
(`label`) and a `valueKeyPath` (`custom.label`). Writing accepts only the
short one.

```
stacks_set_stack_properties  →  {"heading": "My codes", "editMode": "2"}   correct
stacks_set_stack_properties  →  {"custom.heading": "My codes"}             silently ignored
```

A rejected name does not raise an error. It comes back in `rejectedProperties`
while `ok` is still true. **Always check that `rejectedProperties` is empty and
that `changedProperties` lists what you set.**

**2. "stack is not installed" usually means the wrong library folder.** The
Stacks MCP talks to the standalone Stacks app, which reads its library from
`~/Library/Application Support/Stacks/Stacks/`. RapidWeaver Classic reads a
different folder inside its group container. A Doorman installed only for
RapidWeaver Classic is invisible to the MCP. Both libraries are only scanned at
launch, so after copying the bundle across, the app has to be restarted.

## Building a Doorman page

1. Add the stack: `stacks_add_stack` with `stackUid`
   `de.marcello-lang.stacks.doorman`. Every later call wants the returned `uid`
   of the placed instance instead.
2. Doorman takes over the page it sits on, so give it **its own page**. Do not
   nest it inside a layout or column stack; it renders its own login and, in
   full-screen mode, its own complete document.
3. Set `heading` (the title above the code list) and, if the theme should do the
   styling, `styleMode`. Leave the rest at its defaults unless asked.
4. Read the result back with `stacks_get_stack_properties` to confirm.

### Choosing `styleMode`

| Value | Meaning | Use when |
|---|---|---|
| `own` | Doorman brings its own dark look | default, works anywhere |
| `functional` | only function, no appearance | the theme (e.g. Foundation) should style it |
| `fullscreen` | replaces the whole page | a bare login gate with no theme around it |

`functional` also hides the colour fields, since they would have no effect.

### The button colour levels

`editMode` is a staged switch stored as a **string of a digit**, not a word:
`"0"` off, `"1"` colours, `"2"` colours plus hover, `"3"` colours, hover and
border. Each level reveals more fields; anything above the current level stays
disabled. Set the level first, then the colours.

Turning it back to `"0"` restores the built-in colours. The values the user
picked are kept and come back unchanged when the level is raised again.

## What the customer's server must provide

- PHP 8.1 or newer, with sessions and output buffering
- A data folder next to the page that PHP may write to. Doorman creates it
  itself and closes it off with its own `.htaccess`.

If the folder is not writable, the page says so instead of showing a login.

## Things that look like bugs but are not

- **The RapidWeaver preview always shows the setup form and never saves.** That
  is deliberate: the preview runs in a temporary folder, so nothing is stored.
  Publish to see the real behaviour.
- **A published page asks to set a password again.** The data folder was wiped
  or renamed. Check `dataDir` and whether the last publish cleared it.
- **`resetAuth` deletes the stored password** on the next request on the server
  and only takes effect after publishing. Never switch it on without saying so
  plainly; it locks the user out of their own codes until they set a new
  password.
