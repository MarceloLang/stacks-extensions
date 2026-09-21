---
name: f6-off-canvas
description: Use when building or editing a RapidWeaver page in the Stacks app that uses the F6+ Off Canvas stack, a top bar that stays put while the Foundation 6 off-canvas menu opens, with drop zones for a logo, the main menu, an area next to the hamburger button and optionally your own button. Also use when the user mentions "F6+ Off Canvas", "F6 Off Canvas", an off-canvas bar, a hamburger menu for Foundation 6, or asks why the menu shows twice, why the bar disappears when the menu opens, or which Foundation stacks go into the bar.
metadata:
  documents-stack-version: "1.1.2"
  vendor: stacks-extensions.de
---

# F6+ Off Canvas

F6+ Off Canvas is a top bar for Foundation 6 pages. When the off-canvas menu
opens, Foundation pushes the page aside with a `transform`, and a fixed bar
inside the page would slide out of view with it. This stack keeps the bar
visible, moves it in step with the page and brings it back when the menu
closes. It also draws the hamburger button that turns into a cross.

It is **not** a menu itself. It is a bar with drop zones, and the contents are
ordinary **Foundation 6 stacks** (Weaver's Space).

Full settings table: [references/fields.md](references/fields.md). Look field
names up there rather than guessing; a wrong name fails silently (see below).

## Two rules that decide whether your first attempt works

**1. When setting a property through the Stacks MCP, use the short field name,
not the `custom.` path.** Reading a placed stack returns both a `uid`
(`knopfStil`) and a `valueKeyPath` (`custom.knopfStil`). Writing accepts only
the short one. A rejected name does not raise an error: it comes back in
`rejectedProperties` while `ok` is still true. **Always check that
`rejectedProperties` is empty and that `changedProperties` lists what you set.**

**2. "stack is not installed" usually means the wrong library folder.** The
Stacks MCP talks to the standalone Stacks app, which reads its library from
`~/Library/Application Support/Stacks/Stacks/`. RapidWeaver Classic reads a
different folder. Both libraries are only scanned at launch.

## Where the stack has to sit

The page needs Foundation's **Off Canvas** stack. It has two areas: the
**Off Canvas Panel** (the side menu) and the content area next to it.

1. Put **F6+ Off Canvas** as the **first element of the content area**, not in
   the panel and not anywhere else on the page. Placed wrongly, the stack shows
   a red notice "Error: stack in the wrong place" in the edit window.
2. The field `canvasId` must match the **Canvas ID** of the Off Canvas Panel
   exactly (default `offCanvas`, case-sensitive). If they differ, the button
   opens nothing.
3. In the Off Canvas Panel, set **On Page Load** to **Closed**. With
   "In Canvas on Large" Foundation turns the panel into normal page content
   from 1024 px up, and the vertical menu appears a second time under the bar.
4. **Which side the menu opens from is set in the Off Canvas Panel**
   (Position Left or Right), not in this stack. `knopfSeite` only decides where
   the button sits. Button right with the menu opening from the left is a valid
   combination.
5. Match `knopfBis` (up to which width the button shows, default `large`) to
   the breakpoint from which the page shows its full menu in the bar.

## The drop zones and which Foundation 6 stacks go in

| Area (label in the edit window) | Switch | Comes with | Typical content |
|---|---|---|---|
| **Logo (left)** | `logoAn` | `ws.foundation.svg` | SVG stack, an image, or **2 Columns** (Shrink / Auto) with SVG plus **Header** or **Text** for the company name |
| **Menu (centre)** | always there | `ws.foundation.menu` | the horizontal main menu |
| **Menu: right, fixed** (next to the hamburger) | `bleibtAn` | `ws.foundation.menu` | language switch, cart, account link |
| **Button** (only with `knopfStil` = `eigen`) | none | nothing, plus button only | see "Your own button" |

Every area accepts any stack by dragging; the plus button only suggests. The
area next to the hamburger exists only when the button sits on the right
(`knopfSeite` = `rechts`); with the button on the left the logo takes that role.

**Keep the menus small.** The bar is one line. Use a plain horizontal
Foundation **Menu** (no vertical menu, no large buttons) and let the
off-canvas panel hold the full menu for small screens. The height of images in
the logo area is capped by `logoHoehe` (default 40 px), so a large SVG does not
blow up the bar; text in a Header stack is not capped, pick a small heading
size or a Text stack.

## Hamburger button

`knopfStil` (label "Animation") decides what the lines do:

| Value | Meaning |
|---|---|
| `striche` | lines wipe through on hover and turn into a cross (default) |
| `baustein` | top and bottom line turn into an X, the middle one fades ("Turn into an X") |
| `eigen` | "Own button": a drop zone instead of the lines |

The box around it is set separately in the **Hamburger frame** section,
`rahmenAn`: `nein` (none), `neo`, `verlauf` (gradient), `glas`, `soft`, `ja`
(custom). The ready-made looks have their own colour fields; `ja` reveals
border width, radius, border colour (own, like the menu links, or a gradient),
background colour and an optional base. These fields only apply with the
layout `eigen`.

Line colour and border colour default to **like the menu links**
(`knopfFarbeQuelle` / `rahmenFarbeQuelle` = `menue`): on the published page the
stack reads the colour of the first ordinary link in the bar. The edit window
runs no JavaScript and shows the Site Styles link colour instead.

### Your own button

With `knopfStil` = `eigen` the button area starts empty with a plus button that
offers `ws.foundation.html`, `ws.foundation.group`, and **Burger** /
**SVG Burger** by Weaver's Space (`ws.burger.css`, `ws.burger.svg`). F6+ Off
Canvas opens the menu itself; the stack inside only shows the state. For Burger
and SVG Burger the class `is-active` is kept in sync when the menu closes by the
overlay or the Escape key. HTML or Group content is not synced.

**Burger must be set smaller than it comes.** Its defaults are sized for a
standalone button and do not fit the button box (default `knopfGroesse` 40 px).
Measured on freshly placed stacks:

| Stack | Field | Default | Set to |
|---|---|---|---|
| Burger (`ws.burger.css`) | `padding` (number-2, W/H) | `[8, 8]` | `[0, 0]`, the frame gives the space |
| | `size` (number-2, line width/height) | `[32, 4]` | `[22, 2]` |
| | `spacing` (slider, 4 to 15) | `6` | `4` or `5` |
| | `color` (color-2, Default/Active) | black | match the menu |
| SVG Burger (`ws.burger.svg`) | `size` ("Max Width", px) | `80` | `24` |
| | `stroke` (slider, 1 to 10) | `5` | keep; the stroke scales with the width, raise it if the lines get too thin |

With the CSS defaults the button measures 48 × 40 px (32 + 2 × 8 wide,
3 × 4 + 2 × 6 + 2 × 8 high), with the values above 22 × 16 px. Both Burger
stacks share the Sync ID `sync-burger` by default, so several burgers on one
page switch together; leave it unless there is a reason.

`knopfGroesse` stays the space the bar keeps free for the button; the own
button is centred in a box at least that size.

## Behaviour switches worth knowing

- `logoImMenue`: with the menu opening **from the left**, the logo stays in
  place and sits at the top of the opened menu; the main menu moves into its
  space. No effect when the menu opens from the right.
- `bleibtStehen`: the area next to the button stays in place instead of
  moving with the page; with the menu opening from the right it sits in the
  opened menu. Its contents stay usable (the real element is moved, not a copy).
- `nachruecken` (under More settings): while the menu is open the bar gives up
  the space kept for the button.

## Value formats

- Checkboxes are booleans: write `true` / `false`.
- `padding` is a number-4 array in the order **top, bottom, left, right**. Left
  or right is also the distance of the button from the window edge.
- Select fields take the stored value from the table, not the label
  (`rechts`, not "right"; `menue`, not "Like the menu links").
- Colours accept `#RRGGBB` or `#RRGGBBAA`.

## Things that look like bugs but are not

- **The button and the "Button" area look different in the edit window.** The
  edit window runs no JavaScript; menu-link colours, centring of the button and
  the logo behaviour only happen on the page and in the preview.
- **The main menu appears twice on a large screen.** The Off Canvas Panel is on
  "In Canvas on Large". Set it to Closed (see above).
- **Nothing opens.** `canvasId` does not match the panel's Canvas ID.
