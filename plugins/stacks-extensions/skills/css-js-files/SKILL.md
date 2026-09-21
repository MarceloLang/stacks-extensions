---
name: css-js-files
description: Use when building or editing a page in the Stacks app (or RapidWeaver) with the CSS File or JS File stack from the CSS & JS Files bundle, putting your own CSS or JavaScript into the page's own files instead of the page source, grouping several code blocks with "More code", or keeping a page with a lot of custom code tidy in the edit window. Also use when the user mentions "CSS File", "JS File", "CSS & JS Files", files/stacks.css, files/stacks.js, or asks why a code block shows up empty in the published file.
metadata:
  documents-stack-version: "1.0.5"
  vendor: stacks-extensions.de
---

# CSS & JS Files

The bundle installs two stacks that work the same way:

- **CSS File** (`de.marcello-lang.stacks.css-file`) takes CSS.
- **JS File** (`de.marcello-lang.stacks.js-file`) takes JavaScript.

The code goes into the stack's **text area**, and on publish it lands in the
page's own files (`files/stacks.css`, `files/stacks.js`), not in the HTML
source. A stack placed in a **layout** writes to the layout's shared file
instead, which every page using that layout loads from the cache.

The bundle itself (`de.marcello-lang.stacks.css-js-files`) is a hidden
container with no settings. Always place the two child stacks, never the
bundle.

Full settings tables: [references/fields.md](references/fields.md). Look field
names up there rather than guessing.

## Rules for working through the Stacks MCP

**1. Write the code with `stacks_set_stack_text_area`, not as a property.**
Use `textIndex: 1`. The text arrives unchanged (`<`, `&`, quotes, line breaks).
Read it back with `stacks_get_stack_text_areas` and compare: that is the only
reliable check that nothing got lost on the way.

**2. Use the short field name when setting properties** (`marke`, not
`custom.marke`). A rejected name does not raise an error, it comes back in
`rejectedProperties` while `ok` is still true. Check that list every time.

**3. Long code: send it from a file, not by retyping it.** For several blocks
or more than a few kilobytes, keep the code in files and send each file's
content as the `text` argument unchanged. Retyped CSS picks up small mistakes
that break the whole generated file.

**4. The edit window runs no JavaScript.** What you see there proves nothing
about the published result. Export the page and read the generated
`files/stacks.css` / `files/stacks.js`.

## Recommended layout for a page with a lot of custom code

This is the arrangement that keeps a large page readable in the edit window
while every block stays findable. Use it whenever a page gets more than two
or three code blocks.

1. **One CSS File as the head of a group.** Give it a clear title (Notes >
   Title, field `default###userTitle`, for example "CSS of this page") and
   switch on **More code** (`ordner`, a button: set it with
   `stacks_set_stack_boolean`, index 1, value `true`).
2. **Every further CSS block goes into that area**, one CSS File per topic
   (tokens, base, header, one per section). The head block's first child slot
   is the "More code" area; move the blocks there with `stacks_move_stack`,
   `placement: inside`. Their order in the area is their order in the
   generated file, the head block's own code comes first.
3. **Give every block a title and a comment** (`marke`). The title is for the
   edit window only; the comment is published as a comment above the block
   in the generated file and named in error messages.
4. **Do the same for JavaScript** with a JS File as the head and one block per
   feature. Each block runs in its own function, so one block cannot see
   another block's variables.
5. **Put both groups into a Folder stack** (Starter Pack, `ws.starterpack.folder`,
   content area is its second child slot, turn off "Add Swatches") near the
   top of the page, **and switch on "Hide everything"** (`allesZu`, a button,
   index 1, `true`) on both head blocks. Only the header line of each block
   stays visible, with title and comment. To edit a block, switch "Hide
   everything" off again.

   Do not use "Closed in partial" (`partialZu`) for this. It only closes the
   code when the block sits on a page **through a partial**, and a Folder is
   not a partial.
6. **Folder or partial?** Use a partial only for code that really belongs on
   several pages (tokens, header, footer). Code for a single page belongs in a
   Folder on that page; in a partial it would be loaded on every page that
   uses the partial.

## Media queries and loading

- **CSS File: `medienWahl`** wraps the block in a media query that follows the
  Foundation 6 breakpoints; `eigen` unlocks `medien` for your own query (write
  it without `@media`). Use this instead of writing `@media` around the whole
  block by hand.
- **JS File: `zeitpunkt`** decides when the code runs (`dom` fits almost
  always). **`ziel`** `datei` gives the block its own file, so a syntax error
  breaks only that file and not the whole page script.

## When a block shows up empty or broken

- **Syntax error in one block breaks the whole generated file.** Switch on the
  **Banner** (`banner`, `lokal` for local previews only): the page then names
  the block that tore the file. Without it the message is only in the
  browser console.
- **Something inside a condition or a comment that looks like a Stacks macro**
  (text between percent signs) is evaluated by Stacks. Keep such text out of
  your code comments.
