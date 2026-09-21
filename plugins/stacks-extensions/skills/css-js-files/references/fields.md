# CSS & JS Files: settings

This bundle has no settings of its own. It installs the stacks below, each with its own settings. Stack id of each one is given under its heading.

## CSS File: settings

Stack version 1.0.5 (build 105), stack id `de.marcello-lang.stacks.css-file`.

The **Field** column is the name to use when writing with `stacks_set_stack_properties`. Reading returns the same name as `uid`, alongside a `valueKeyPath` of `custom.<field>`. That longer form is for reading only, writing with it is silently rejected.

| Field | Label | Group | Type | Default | Shown when | Meaning |
|---|---|---|---|---|---|---|
| `default###userTitle` | Title | Notes | input | `` |  | Shows on the pill above the stack, including when it is collapsed. This is purely for the overview inside the app: it does not appear on the website or in the generated files. That is what the comment is for. |
| `marke` | Comment | Notes | input | `` |  | A short text that goes into the generated file as a comment above the block and is named in the error message. Helps you find a block again when several of them sit in the same file. Unlike the title, it is published. |
| `ordner` | More code | View | button | `false` |  | Shows an area with a plus below the code, which puts another block of the same kind inside it: JavaScript under JS File, CSS under CSS File. Once a block sits inside, the area stays visible even without this button, because its code still goes into the generated file. A block that already sits inside another gets no area of its own; it does not nest deeper than one level. |
| `allesZu` | Hide everything | View | button | `false` | `ordner` == `true` | Shows only the header of every block in this area, the way it looks through a partial. Clicking a block opens it for editing, clicking elsewhere closes it again. The code stays stored and goes into the generated file unchanged. |
| `ansicht` | Line numbers | View | checkbox | `1` |  | Shows a column of line numbers next to the code while you edit. The code then no longer wraps but scrolls sideways, so the numbers match the lines. Nothing changes on the website. |
| `zeigen` | Show code | View | checkbox | `1` |  | Shows or hides the code area while you edit. Hidden, only a slim line is left; the code itself stays stored and goes into the file unchanged. Show it again to edit it. |
| `partialZu` | Closed in partial | View | checkbox | `1` |  | Hides the code as soon as the block sits on a page through a partial. The header with title and comment stays, so you still see what is inside. Inside the partial itself everything is shown and edited as usual. Neither the stored code nor the generated file changes. |
| `hoehe` | Maximum height | View | number | `0` |  | Limits the height of the code area while you edit; beyond that it scrolls. 0 means no limit, then the whole code is shown. |
| `uiLang` | Language | General | input | `en` |  | Language of all texts: “de” or “en”. In the English package this is set to “en” automatically. |
| `medienWahl` | Media query | General | select | `immer` |  | Wraps your rules in a media query. The sizes follow the Foundation 6 breakpoints: small up to 40em, medium from 40em to 64em, large from 64em. "All" leaves the rules unbound, "Custom" unlocks the field below. The stack writes the @media in front for you. |
| `medien` | Custom query | General | input | `` | `medienWahl` == `eigen` | Only takes effect when the field above is set to "Custom". Write it without the word @media, for example "screen and (min-width: 900px)". The stack puts that in front for you. |
| `banner` | Banner | Error warning | select | `0` |  | Shows a red banner at the bottom of the page when a block has broken the generated file. Switched on, the block adds a small check script to the page source; only that way does the warning work when the page script file itself has aborted. "Local only" means the preview and local addresses, "Everywhere" shows it online as well and names the switch to turn it off. Off by default; without the banner the hint goes to the developer console only. |

### Accepted values for the dropdown fields

Set the **value**, not the label.

**`medienWahl`**: Media query

| Value | Label |
|---|---|
| `immer` | All |
| `screen and (max-width: 39.99875em)` | Small only |
| `screen and (max-width: 63.99875em)` | Small + medium |
| `screen and (min-width: 40em) and (max-width: 63.99875em)` | Medium only |
| `screen and (min-width: 40em)` | Medium + large |
| `screen and (min-width: 64em)` | Large only |
| `screen and (prefers-color-scheme: dark)` | Dark mode |
| `screen and (prefers-color-scheme: light)` | Light mode |
| `(hover: none) and (pointer: coarse)` | Touch device |
| `screen and (orientation: portrait)` | Portrait |
| `screen and (orientation: landscape)` | Landscape |
| `print` | For print |
| `only screen and (-webkit-min-device-pixel-ratio: 2)` | Retina |
| `eigen` | Custom |

**`banner`**: Banner

| Value | Label |
|---|---|
| `0` | Off |
| `lokal` | Local only |
| `immer` | Everywhere |

## JS File: settings

Stack version 1.0.5 (build 105), stack id `de.marcello-lang.stacks.js-file`.

The **Field** column is the name to use when writing with `stacks_set_stack_properties`. Reading returns the same name as `uid`, alongside a `valueKeyPath` of `custom.<field>`. That longer form is for reading only, writing with it is silently rejected.

| Field | Label | Group | Type | Default | Shown when | Meaning |
|---|---|---|---|---|---|---|
| `default###userTitle` | Title | Notes | input | `` |  | Shows on the pill above the stack, including when it is collapsed. This is purely for the overview inside the app: it does not appear on the website or in the generated files. That is what the comment is for. |
| `marke` | Comment | Notes | input | `` |  | A short text that goes into the generated file as a comment above the block and is named in the error message. Helps you find a block again when several of them sit in the same file. Unlike the title, it is published. |
| `ordner` | More code | View | button | `false` |  | Shows an area with a plus below the code, which puts another block of the same kind inside it: JavaScript under JS File, CSS under CSS File. Once a block sits inside, the area stays visible even without this button, because its code still goes into the generated file. A block that already sits inside another gets no area of its own; it does not nest deeper than one level. |
| `allesZu` | Hide everything | View | button | `false` | `ordner` == `true` | Shows only the header of every block in this area, the way it looks through a partial. Clicking a block opens it for editing, clicking elsewhere closes it again. The code stays stored and goes into the generated file unchanged. |
| `ansicht` | Line numbers | View | checkbox | `1` |  | Shows a column of line numbers next to the code while you edit. The code then no longer wraps but scrolls sideways, so the numbers match the lines. Nothing changes on the website. |
| `zeigen` | Show code | View | checkbox | `1` |  | Shows or hides the code area while you edit. Hidden, only a slim line is left; the code itself stays stored and goes into the file unchanged. Show it again to edit it. |
| `partialZu` | Closed in partial | View | checkbox | `1` |  | Hides the code as soon as the block sits on a page through a partial. The header with title and comment stays, so you still see what is inside. Inside the partial itself everything is shown and edited as usual. Neither the stored code nor the generated file changes. |
| `hoehe` | Maximum height | View | number | `0` |  | Limits the height of the code area while you edit; beyond that it scrolls. 0 means no limit, then the whole code is shown. |
| `uiLang` | Language | General | input | `en` |  | Language of all texts: “de” or “en”. In the English package this is set to “en” automatically. |
| `ziel` | Target | General | select | `seite` |  | “Page script file” appends the code to the shared JavaScript file of the page. “Its own file” puts it into a file of its own next to the page and loads it from there; an error in the code then breaks that file only. |
| `zeitpunkt` | Execution | General | select | `dom` |  | When the code runs. “DOM ready” fits almost every case. “Immediately” only if the code is meant to run before the page is built. “Page loaded” also waits for images and embedded content. |
| `banner` | Banner | Error warning | select | `0` |  | Shows a red banner at the bottom of the page when a block has broken the generated file. Switched on, the block adds a small check script to the page source; only that way does the warning work when the page script file itself has aborted. "Local only" means the preview and local addresses, "Everywhere" shows it online as well and names the switch to turn it off. Off by default; without the banner the hint goes to the developer console only. |

### Accepted values for the dropdown fields

Set the **value**, not the label.

**`ziel`**: Target

| Value | Label |
|---|---|
| `seite` | Page script file |
| `datei` | Its own file |

**`zeitpunkt`**: Execution

| Value | Label |
|---|---|
| `dom` | DOM ready |
| `sofort` | Immediately |
| `load` | Page loaded |

**`banner`**: Banner

| Value | Label |
|---|---|
| `0` | Off |
| `lokal` | Local only |
| `immer` | Everywhere |
