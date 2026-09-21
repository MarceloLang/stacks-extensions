# F6+ Off Canvas: settings

Stack version 1.1.2 (build 112), stack id `de.marcello-lang.stacks.f6-off-canvas`.

The **Field** column is the name to use when writing with `stacks_set_stack_properties`. Reading returns the same name as `uid`, alongside a `valueKeyPath` of `custom.<field>`. That longer form is for reading only, writing with it is silently rejected.

| Field | Label | Group | Type | Default | Shown when | Meaning |
|---|---|---|---|---|---|---|
| `default###userTitle` | Title | Notes | input | `` |  | Shows on the pill above the stack, including when it is collapsed. This is purely for the overview inside the app: it does not appear on the website. |
| `canvasId` | Off-canvas ID | General | input | `offCanvas` |  | The name of the off-canvas stack this button opens. You find it there in the “Name” field. It has to match exactly, upper and lower case included. |
| `zindex` | z-index | General | number | `150` |  | How far to the front the bar sits. Higher means on top of other things. If something covers the bar, an image while scrolling for example, this value is too low: many stacks put themselves at 100 to 110. While the menu is open the stack moves the bar behind the panel by itself. |
| `padding` | Padding | General | number-4 | `8, 8, 8, 8` |  | Inner spacing of the bar in pixels, top, bottom, left and right set separately. Left or right is also the distance of the menu button from the window edge. |
| `klasse` | CSS class | General | input | `` |  | Your own class on the bar, in case you want to style it yourself. Leave empty if you do not need it. |
| `breite` | Content width | General | number | `0` |  | Maximum width of the bar’s content in pixels, centered. 0 means full width. Set it to the content width of your page, and the menu and the area next to the button line up with the rest of the content. |
| `layout` | Layout | Appearance | select | `eigen` |  | Ready-made look for the bar and the menu button. Custom: the colors below. Foundation: top bar background and link colors from Site Styles (site-wide values, not a single Menu Styles preset). Neo-Brutal look: tinted bar with a thick line, yellow button with border and hard shadow. Glass: translucent, blurred bar and a round glass button. |
| `knopfSeite` | Alignment | Appearance | select | `rechts` | `knopfAn` == `true` | Which side the hamburger menu sits on, right or left. |
| `bgFarbe` | Background | Appearance | color | `rgba(241,239,113,1.00)` | `layout` == `eigen` | Color of the bar. For “transparent” set the opacity to 0. |
| `bgFarbeScroll` | Color when scrolled | Appearance | color | `rgba(248,248,248,1.00)` | `scrollModus` != `aus` | Color once the page has been scrolled. |
| `schwelle` | From pixel | Appearance | number | `10` | `scrollModus` != `aus` | After how many scrolled pixels the change kicks in. |
| `textModus` | Text colours | Appearance | select | `theme` |  | Theme: text and links keep the colours the menu or the theme brings along, for example through Foundation's Menu Styles. Custom: text and link colour for everything in the bar from the field below, with any layout. |
| `textFarben` | Text | Appearance | color-2 | `rgba(15,15,15,1.00), rgba(15,15,15,0.65)` | `textModus` == `eigen` | Text colour and link colour on hover. |
| `scrollModus` | When scrolled | Appearance | select | `eigen` |  | From a certain scroll height the bar changes color and gets a shadow. Only pick “with GSAP” if GSAP is on the page anyway (Joe Workman’s stacks bring it along); if it is missing, the stack uses its own JavaScript. |
| `schatten` | Shadow | Appearance | checkbox | `true` | `scrollModus` != `aus` | A fine shadow under the bar once the page has been scrolled. |
| `schattenMass` | Shadow size | Appearance | number-3 | `4, 13, -8` | `schatten` == `true` | Downward offset, blur and spread of the shadow in pixels. A negative spread pulls the shadow back under the bar, so it only shows as a fine edge at the bottom. |
| `schattenFarbe` | Shadow colour | Appearance | color | `rgba(0,0,0,0.60)` | `schatten` == `true` | Colour and opacity of the shadow. |
| `gsapLaden` | If GSAP is missing | Appearance | select | `nein` | `scrollModus` == `gsap` | What to do when GSAP is not on the page. “From your own folder” takes it from rw_common/plugins/stacks/gsap/, where Joe Workman’s stacks put it. “From someone else’s server” fetches it from the web, and that server learns the addresses of your visitors. |
| `logoAn` | Add logo area? | Logo | checkbox | `true` |  | A drop zone at the left of the bar, for a logo or a wordmark. Freshly placed it already holds a Foundation SVG stack. It wraps around its content, the menu next to it takes the rest. Switched off it is not created at all: what sits inside stays out of the page source and is hidden in the edit window. Nothing is lost, it all comes back when you switch it on again. |
| `logoImMenue` | Logo stays put when the menu opens | Logo | checkbox | `false` | `logoAn` == `true` | Works when the off-canvas menu opens from the left (position Left in the Off Canvas Panel), whether the menu button is on the left or the right. Off: when the menu opens, the logo moves right with the page. On: the logo stays in place and so sits at the top of the opened menu; the main menu moves into the space where the logo was. If the menu opens from the right, the switch changes nothing. |
| `logoBreite` | Width | Logo | number | `0` | `logoAn` == `true` | Fixed width of the area. 0 means as wide as its content. A fixed width pays off when several pages should line up even though the logos differ in width. |
| `logoEinheit` | Unit | Logo | select | `px` | `logoAn` == `true` | Unit of the width. Pixels stay the same, rem follows the page font size and grows when the visitor enlarges it. |
| `logoAbstand` | Gap | Logo | number | `24` | `logoAn` == `true` | Gap in pixels between the logo and the menu next to it. |
| `logoHoehe` | Height | Logo | number | `40` | `logoAn` == `true` | Largest height for images and graphics in the logo area, in pixels. That way the bar decides its own height, however big the image someone drops in. The aspect ratio is kept, the width follows the height. 0 lifts the limit, then whatever the content brings applies. |
| `knopfAn` | Use hamburger menu | Hamburger menu | checkbox | `true` |  | Shows the menu button that opens the off-canvas menu and turns into a cross. Off if you use a button of your own. |
| `knopfStil` | Animation | Hamburger menu | select | `striche` | `knopfAn` == `true` | What the lines do. Wiping lines: they wipe across on hover and turn into a cross when the menu opens. Turn into an X: the top and bottom lines turn into an X, the middle one fades out. Own button: a drop zone with a plus button that offers HTML and Group from Foundation as well as Burger and SVG Burger by Weaver's Space; any stack can be dragged in. You set the box around it under Hamburger frame, it applies to all three. |
| `knopfBis` | Show up to | Hamburger menu | select | `large` | `knopfAn` == `true` | From which screen width the button disappears. Pick it to match “In Canvas For” of the off-canvas stack. |
| `knopfGroesse` | Box size | Hamburger menu | number | `40` | `knopfAn` == `true` | Edge length of the button in pixels. Below 44 it gets tight for fingers. With your own button this is the space the bar keeps free for it. |
| `knopfFarbeQuelle` | Line colour | Hamburger menu | select | `menue` | `layout` == `eigen` | Custom: the colour from the field below. Like the menu links: the lines get the same colour as the links in the menu of the bar. On the page the stack reads the colour of the first link, in the edit window it shows the link colour from Site Styles. |
| `knopfFarbe` | Color | Hamburger menu | color | `rgba(15,15,15,1.00)` | `knopfFarbeQuelle` == `eigen` | Colour of the lines and the cross. |
| `knopfHoverAn` | Hover colors | Hamburger menu | checkbox | `false` | `layout` == `eigen` | A different colour for the lines and the cross on hover. The fill on hover is set under Hamburger frame and works without this switch. |
| `knopfFarbeHover` | Lines on hover | Hamburger menu | color | `rgba(15,15,15,1.00)` | `knopfHoverAn` == `true` | Color of the lines and the cross on hover. |
| `strichDicke` | Line weight | Hamburger menu | number | `2` | `knopfAn` == `true` | Thickness of the lines and the cross in pixels. Applies to the Wiping lines and Brick styles. |
| `knopfMehr` | More settings | Hamburger menu | checkbox | `false` | `knopfAn` == `true` | Shows the rarely used settings: line length, cross on hover, content moves up and the screen reader label. Hidden, they keep working with their values. |
| `strich` | Line length | Hamburger menu | number | `18` | `knopfMehr` == `true` | Length of the three lines, in pixels. |
| `kreuzLang` | Cross on hover | Hamburger menu | number | `115` | `knopfMehr` == `true` | How much longer the lines of the cross get while the mouse rests on the button, in percent. 100 means no difference. Without a mouse it always stays at the normal length. |
| `nachruecken` | Content moves along | Hamburger menu | checkbox | `true` | `knopfMehr` == `true` | The button keeps space free in the bar. While the menu is open it gives that space back, and whatever sits at the right of the bar moves along. |
| `ariaLabel` | Label | Hamburger menu | input | `Open menu` | `knopfMehr` == `true` | For screen readers; it is not visible. |
| `rahmenAn` | Frame | Hamburger frame | select | `ja` | `layout` == `eigen` | None: the button stands without a box, just the lines or your own button. Neo-brutal look: a fill with a thick line, rounded corners and a hard shadow. Gradient: a fill with a colour gradient, white lines. Glass: translucent with a blur behind it, round. Soft UI: light, as if pressed out of the background. For these four the colours can be changed below. Custom: set line, radius, fill and bottom edge yourself. The custom settings stay stored, even while a ready-made look is selected. |
| `neoFarben` | Colours | Hamburger frame | color-2 | `rgba(255,210,63,1.00), rgba(17,17,17,1.00)` | `rahmenAn` == `neo` | Colours of the neo-brutal look: the fill and the colour of the line and hard shadow. |
| `verlaufLookFarben` | Colours | Hamburger frame | color-3 | `rgba(99,102,241,1.00), rgba(168,85,247,1.00), rgba(236,72,153,1.00)` | `rahmenAn` == `verlauf` | The three colours of the gradient, diagonally from top left to bottom right. The shadow follows the start and end colour. |
| `glasFarben` | Colours | Hamburger frame | color-2 | `rgba(255,255,255,0.55), rgba(255,255,255,0.70)` | `rahmenAn` == `glas` | Colours of the glass look. The fill needs transparency, otherwise the blur behind it cannot show. |
| `softFarben` | Colours | Hamburger frame | color-3 | `rgba(232,236,242,1.00), rgba(255,255,255,0.90), rgba(163,177,198,0.60)` | `rahmenAn` == `soft` | Colours of Soft UI: the fill, the light at the top left and the shadow at the bottom right. It works best when the fill matches the colour of the bar. |
| `rahmenDicke` | Border width | Hamburger frame | number | `1` | `rahmenAn` == `ja` | Width of the line around the box in pixels. 0 means no line. |
| `rahmenRundung` | Radius | Hamburger frame | number | `3` | `rahmenAn` == `ja` | Corner radius in pixels. Half the box size makes a circle. |
| `rahmenFarbeQuelle` | Border colour | Hamburger frame | select | `menue` | `rahmenAn` == `ja` | Custom: the colour from the field below. Like the menu links: the same colour as the links in the menu of the bar. Gradient: the line gets a gradient of two colours in the chosen direction. |
| `rahmenFarbe` | Colour | Hamburger frame | color | `rgba(15,15,15,1.00)` | `rahmenFarbeQuelle` == `eigen` | Colour of the line around the box. |
| `rahmenVerlaufRichtung` | Direction | Hamburger frame | select | `schraeg` | `rahmenFarbeQuelle` == `verlauf` | Direction of the gradient in the line: left to right, top to bottom, diagonally from top left to bottom right, or from the centre, with the start colour in the middle and the end colour on both sides. |
| `rahmenVerlaufFarben` | Gradient | Hamburger frame | color-2 | `rgba(99,102,241,1.00), rgba(236,72,153,1.00)` | `rahmenFarbeQuelle` == `verlauf` | Start and end colour of the gradient in the line. |
| `flaecheAn` | Background colour | Hamburger frame | select | `keine` | `rahmenAn` == `ja` | None: the box is transparent inside. Custom: a colour below, for normal and on hover. The colours stay stored even while this is set to None. |
| `knopfFlaeche` | Colour | Hamburger frame | color-2 | `rgba(255,255,255,0.00), rgba(255,255,255,0.00)` | `flaecheAn` == `farbe` | Background colour of the box, normal and on hover. The hover colour is laid over the normal one: transparent changes nothing, semi-transparent tints, opaque replaces. |
| `sockelAn` | Base | Hamburger frame | checkbox | `false` | `rahmenAn` == `ja` | A darker edge along the bottom that the box stands on like a building brick. Switched on, height and colour appear below. |
| `kante` | Base height | Hamburger frame | number | `4` | `sockelAn` == `true` | Height of the base in pixels. The lines move up by half the height so they sit centred on the face. |
| `kanteFarbe` | Base colour | Hamburger frame | color | `rgba(201,147,0,1.00)` | `sockelAn` == `true` | Colour of the base, usually a darker shade of the background colour. |
| `bleibtAn` | Show area | Left of the hamburger menu | checkbox | `true` |  | A second drop zone next to the menu button, for example for a language switch or a cart. It moves with the page when the menu opens and stays visible at the edge of the menu. Switched off, the area is not created at all: what sits inside it stays out of the page source and is hidden in the edit window too. Nothing is lost, it all comes back when you switch the area on again. Only with the menu button on the right: on the left, the logo takes over this role. |
| `bleibtStehen` | Stays put when the menu opens | Left of the hamburger menu | checkbox | `false` | `bleibtAn` == `true` | Off: when the menu opens, the area moves with the page and keeps its distance from the edge of the menu. On: it stays in place next to the menu button; if the menu opens from the right, it sits at the top of the opened menu. Whatever is inside stays usable. |
| `bleibtAbstand` | Spacing | Left of the hamburger menu | number | `8` | `bleibtAn` == `true` | Distance in pixels to the menu button and, while the menu is open, to the edge of the panel. |
| `stapeln` | Stacked | View | checkbox | `false` |  | Puts the menu, the area next to the button and the menu button below each other in the edit window instead of side by side. Helps when the window is narrow and everything is squeezed. It changes nothing on the website, there they always sit side by side. |
| `inhaltZeigen` | Show content | View | checkbox | `true` |  | Shows or hides the bar and its drop zones while you edit. Hidden, only a slim line is left; everything inside stays stored and appears on the website unchanged. Show it again to edit it. |
| `uiLang` | Language | General | input | `en` |  | Language of all texts: “de” or “en”. The English package has “en” here automatically. |

## Accepted values for the dropdown fields

Set the **value**, not the label.

**`layout`**: Layout

| Value | Label |
|---|---|
| `eigen` | Custom |
| `foundation` | Foundation (Site Styles) |
| `neo-brutal` | Neo-Brutal look |
| `glas` | Glass |

**`knopfSeite`**: Alignment

| Value | Label |
|---|---|
| `rechts` | right |
| `links` | left |

**`textModus`**: Text colours

| Value | Label |
|---|---|
| `theme` | Theme |
| `eigen` | Custom |

**`scrollModus`**: When scrolled

| Value | Label |
|---|---|
| `aus` | leave it alone |
| `eigen` | with its own JavaScript |
| `gsap` | with GSAP ScrollTrigger |

**`gsapLaden`**: If GSAP is missing

| Value | Label |
|---|---|
| `nein` | use its own JavaScript |
| `lokal` | load from your own folder |
| `cdn` | load from someone else’s server |

**`logoEinheit`**: Unit

| Value | Label |
|---|---|
| `px` | Pixels (px) |
| `rem` | Font sizes (rem) |

**`knopfStil`**: Animation

| Value | Label |
|---|---|
| `striche` | Wiping lines |
| `baustein` | Turn into an X |
| `eigen` | Own button |

**`knopfBis`**: Show up to

| Value | Label |
|---|---|
| `large` | below 1024 px (large) |
| `medium` | below 640 px (medium) |
| `immer` | always show |

**`knopfFarbeQuelle`**: Line colour

| Value | Label |
|---|---|
| `eigen` | Custom |
| `menue` | Like the menu links |

**`rahmenAn`**: Frame

| Value | Label |
|---|---|
| `nein` | None |
| `neo` | Neo-brutal look |
| `verlauf` | Gradient |
| `glas` | Glass |
| `soft` | Soft UI |
| `ja` | Custom |

**`rahmenFarbeQuelle`**: Border colour

| Value | Label |
|---|---|
| `eigen` | Custom |
| `menue` | Like the menu links |
| `verlauf` | Gradient |

**`rahmenVerlaufRichtung`**: Direction

| Value | Label |
|---|---|
| `horizontal` | Horizontal |
| `vertikal` | Vertical |
| `schraeg` | Diagonal |
| `mittig` | From the centre |

**`flaecheAn`**: Background colour

| Value | Label |
|---|---|
| `keine` | None |
| `farbe` | Custom |

