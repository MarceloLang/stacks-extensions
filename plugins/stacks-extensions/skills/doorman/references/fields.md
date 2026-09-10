# Doorman — settings

Stack version 1.0.2 (build 102), stack id `de.marcello-lang.stacks.doorman`.

The **Field** column is the name to use when writing with `stacks_set_stack_properties`. Reading returns the same name as `uid`, alongside a `valueKeyPath` of `custom.<field>` — that longer form is for reading only, writing with it is silently rejected.

| Field | Label | Group | Type | Default | Shown when | Meaning |
|---|---|---|---|---|---|---|
| `styleMode` | CSS scope | General | select | `own` |  | How much styling the stack brings along. “Theme styles” = function only, your theme (Foundation, for instance) does the design. |
| `heading` | Heading | General | input | `Your two-factor codes` |  | Heading above the list of codes, after signing in. |
| `bgColor` | Background | General | color | `#171b21` | `styleMode` != `functional` | Background colour of the login card. Meant for dark shades, the text on it is light. |
| `headColor` | Headings | General | color | `#e8eaed` | `styleMode` != `functional` | Colour of the headings. Overrides what the theme sets (Foundation, for instance). |
| `footColor` | Footer | General | color | `#9aa3af` | `styleMode` != `functional` | Text colour of the note below the card. |
| `editMode` | Editing | Buttons | select | `0` | `styleMode` != `functional` | How much can be set. Each level reveals further rows. |
| `b2` | Main button | Buttons | color-2 | `#243464, #e0e4eb` | `editMode` >= `1` |  |
| `b2h` | Hover | Buttons | color-2 | `#243464, #e0e4eb` | `editMode` >= `2` |  |
| `b2b` | Border | Buttons | color-2 | `rgba(0,0,0,0.0), rgba(0,0,0,0.0)` | `editMode` >= `3` |  |
| `b3` | Hollow button | Buttons | color-2 | `#171b21, #e8eaed` | `editMode` >= `1` |  |
| `b3h` | Hover | Buttons | color-2 | `#171b21, #e8eaed` | `editMode` >= `2` |  |
| `b3b` | Border | Buttons | color-2 | `#262c34, #262c34` | `editMode` >= `3` |  |
| `b1` | Other buttons | Buttons | color-2 | `#6ea0ff, #0b1220` | `editMode` >= `1` |  |
| `b1h` | Hover | Buttons | color-2 | `#6ea0ff, #0b1220` | `editMode` >= `2` |  |
| `b1b` | Border | Buttons | color-2 | `rgba(0,0,0,0.0), rgba(0,0,0,0.0)` | `editMode` >= `3` |  |
| `b4` | Sign-out button | Buttons | color-2 | `#171b21, #e8eaed` | `editMode` >= `1` |  |
| `b4h` | Hover | Buttons | color-2 | `#171b21, #e8eaed` | `editMode` >= `2` |  |
| `b4b` | Border | Buttons | color-2 | `#262c34, #262c34` | `editMode` >= `3` |  |
| `border` | Border | Buttons | number-2 | `1, 10` | `editMode` >= `3` | Border width and corner radius in pixels. The width applies to every button alike, so they stay the same size. |
| `brandShow` | Banner image | Login | select | `none` |  | An optional image above the login. None by default. |
| `brandUrl` | Address | Login | link | `` | `brandShow` == `url` | Address (URL) of an image that sits online. |
| `brandImage` | Image | Login | image | `` | `brandShow` == `file` | An image file, dragged in or chosen. |
| `dataDir` | Folder name | Security | input | `doorman-data` |  | This is where the keys (secrets.json) and the login data (auth.json) are kept. It is closed off with an .htaccess of its own. |
| `pwMin` | Password length | Security | slider | `6` |  | The login password must have at least this many characters. |
| `resetAuth` | Password | Security | button | `off` |  | Deletes the stored password (auth.json) the next time the page is opened on the server. Takes effect only after publishing. |
| `uiLang` | Language | General | input | `en` |  | Language of all texts: “de” or “en”. The English package uses “en” automatically. |

## Accepted values for the dropdown fields

Set the **value**, not the label.

**`styleMode`** — CSS scope

| Value | Label |
|---|---|
| `own` | Own styling |
| `functional` | Theme styles (function only) |
| `fullscreen` | Full screen (covers the theme) |

**`editMode`** — Editing

| Value | Label |
|---|---|
| `0` | Off |
| `1` | Colours |
| `2` | Colours + hover |
| `3` | Colours + hover + border |

**`brandShow`** — Banner image

| Value | Label |
|---|---|
| `none` | No banner image |
| `url` | External image address |
| `file` | Drag and drop |

