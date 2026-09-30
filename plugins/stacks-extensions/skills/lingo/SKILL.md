---
name: lingo
description: Use when making a page multilingual in the Stacks app (or RapidWeaver) with the Lingo bundle from stacks-extensions.de, translating texts of existing stacks, adding a language, placing a language switcher, or setting up browser/location detection and the "also available in" banner. Also use when the user mentions "Lingo", "Lingo Base", "Lingo Text", "Lingo Entry"/"Lingo Eintrag", "Lingo Block", "Lingo Switch", "Lingo Solo", a page that exists in one language only, ?lang=, hreflang, or asks to translate a page built with Stacks.
metadata:
  documents-stack-version: "0.1.0"
  vendor: stacks-extensions.de
---

# Lingo

Multilingual pages without building every section once per language. The
layout exists once; texts are swapped on the server.

| Stack | ID | Job |
|---|---|---|
| Lingo Base | `de.marcello-lang.stacks.lingo-base` | Languages of the page (once, at the top) |
| Lingo Text | `de.marcello-lang.stacks.lingo-text` | Wraps any stacks and translates their texts |
| Lingo Entry | `de.marcello-lang.stacks.lingo-entry` | One text and its translations, inside a Lingo Text |
| Lingo Block | `de.marcello-lang.stacks.lingo-block` | Content that differs per language (only shown in its language) |
| Lingo Switch | `de.marcello-lang.stacks.lingo-switch` | Language switcher for visitors |
| Lingo Solo | `de.marcello-lang.stacks.lingo-solo` | This page in one language only |

The bundle `de.marcello-lang.stacks.lingo` is a hidden container. Always
place the child stacks.

## The one rule for translating: one Lingo Entry per translation unit

**Every translatable unit gets its own Lingo Entry** (a heading, a paragraph,
a button label, an alt text): the equivalent of one click on the blue plus
in the Lingo Text's entry area. **Do not** put a section's translations into
the Lingo Text's big box. Collapsed, each entry shows its original text as
one line, which is what makes the page reviewable; a big box hides that.

Entry format (the entry's text area, `textIndex: 1`):

```
Stay in the loop.
de: Bleib auf dem <span class="se-hl">Laufenden</span>.
fr: Restez informé.
```

- **First line:** the text exactly as it appears on the page.
- **Then one line per language:** `code: translation`. Codes must be listed in
  Lingo Base, otherwise the preview warns "not a language of this page".
- Put a CSS selector in brackets in front of the first line only when the same
  text appears several times and only one should change: `[.button] Learn more`.
- **An entry with only the first line means "keep as is"** (brand and product
  names, a stack's own placeholder text). It changes nothing on the page but
  tells the preview notice that the text is handled.
- **Excluding areas: `translate="no"`, the class `notranslate` or the class
  `no-lingo`.** All three work on the element itself or on any ancestor inside
  the Lingo Text, and so does the Lingo Switch. Lingo neither lists those texts
  in the notice nor replaces anything inside them (text, whole elements,
  `alt`/`title`/`placeholder`/`aria-label`/`value`), even if an entry matches.
  Which one to use:
  - `translate="no"` or `notranslate`: keep Lingo **and** the browser's own
    translation (Chrome, Safari, Google Translate) away. Right for names, code,
    prices, data. `notranslate` is the class form for a stack's
    "Custom Classes" field.
  - `no-lingo`: keep only Lingo away; the browser may still translate it.
  Through the MCP, append the class to the existing `class` value instead of
  overwriting it.
- **Characters:** the first line takes any characters. A translation without
  tags is inserted as plain text, so `< > & " ' / ;` are fine. As soon as a
  translation contains a tag it is read as HTML: write a literal `<` as `&lt;`
  and `>` as `&gt;` there. Put highlight markup where it belongs in *that*
  language (`Was jeder Stack <span class="se-hl">kann</span>.`); never assume
  the highlighted word keeps its position. The edit window marks entries with
  HTML by a small `</>` icon.
- No blank lines inside an entry. For a line break inside `<pre>`, write
  `&#10;` in the translation.

## How matching works (so entries actually hit)

1. **Whole-element text.** A text is only replaced if it is the complete text
   of its element: `Learn more` matches `<a><i class="icon"></i> Learn more</a>`
   but not the words inside `<p>Learn more about us</p>`.
2. **Sentences split across tags** (`<h2>The <span>newest</span> stacks.</h2>`):
   write the first line as the element's full text with single spaces
   (`The newest stacks.`) and give the translation its own HTML
   (`Die <span class="se-hl">neuesten</span> Stacks.`). The innermost element
   whose text matches is replaced.
3. **Attributes** `alt`, `title`, `placeholder`, `aria-label`, `value` are
   matched the same way.
4. Text a stack only creates in the browser with JavaScript cannot be reached.
   See "Data and generated content" below.
5. The original text may be in any language; the default language gets a line
   of its own only if the page text is not already in it.
6. **Text without a single letter is ignored.** Numbers, version numbers and
   numeric dates (`1.0.2`, `3`, `22.08.2026`) are never listed in the notice
   and never changed, so they need neither an entry nor `translate="no"`. As
   soon as a letter is in it (`22 Aug 2026`, `v1.0.2`, `1.1.0-beta`) it counts
   as text.
7. **A fixed label next to a changing value:** give the label an element of
   its own, `<span>Replaced by</span> <a translate="no">…</a>`. Otherwise the
   element's full text changes with every value and no entry can match it.
8. **A sentence with a link or button inside**
   (`<p>No match. Try again or <button class="reset">show all</button>.</p>`):
   one entry for the whole paragraph. First line = the full text with single
   spaces, translation = the paragraph's HTML including the inner element and
   its class. The swap happens on the server before any script runs, so event
   listeners attached by JavaScript still find the element.

## Data and generated content

- **Mark data with `translate="no"` (or `class="notranslate"`)**: everything that changes per record and
  already arrives in the right language from the data source (names, short
  texts, categories, prices, dates with month names in a Feeds template).
  Without it the notice lists every value as missing, and an entry for one
  record would never fit the next.
- **Content that is already in the page's language** (a PHP include chosen per
  language, a snippet file per language) gets `translate="no"` on its wrapper
  as well, for the same reason.
- **Text created by JavaScript**: besides Lingo Block there is a lighter way.
  Lingo Base sets `<html lang>`; the script reads
  `document.documentElement.lang` and takes its strings from a small
  dictionary (`{ en: {...}, de: {...} }`, falling back to the default
  language). Good for counters and states ("4 stacks", "newest first").
- **PHP that picks a language itself** must ask `lingo_sprache()` first. On a
  first visit the language cookie only travels with the response, not the
  request; code that reads only the cookie shows the default language on a
  page Lingo already switched.

## A page in one language only: Lingo Solo

For a page that exists in one language only (an internal page, a legal text
kept in one language), while the rest of the site stays multilingual.

- Place **Lingo Solo** on the page itself, above the page's own content, not
  inside a Lingo Text and not inside SEO Meta Tags. Field `sprache`: the
  language code, e.g. `de`.
- From its position on, Lingo works in that language. At the very end of the
  page it re-translates the Lingo Texts that ran before it (header and menu
  from a layout), rebuilds Lingo Switch with the other languages struck
  through plus a sentence in the visitor's language saying why, sets
  `<html lang>` and `Content-Language`, and removes `hreflang` and the
  "also available in" banner. The visitor's language cookie stays, so the
  other pages keep their language.
- Limit: Lingo Blocks above it do not follow (their other-language content was
  never sent).
- Do not also rewrite `<html lang>` with own PHP (for example via SEO Meta
  Tags); Lingo Solo already does it.

## Workflow through the Stacks MCP

1. **Lingo Base** at the very top of the page (or in a shared partial). Fields
   `s1`…`s8` (select, value = code, `-` = empty; `s1` is the default language),
   `erkennung` (`aus` / `browser` / `beides`), `reaktion` (`hinweis` = banner,
   `wechseln` = switch automatically), `cookieName`.
2. **Wrap each section in its own Lingo Text**: add a Lingo Text before the
   section with `stacks_add_stack` (`placement: before`), then move the section
   into the Lingo Text's **first** child slot (`stacks_move_stack`,
   `placement: inside`). Children of a Lingo Text: `[content, entries, box]`.
   Lingo Text outputs no element of its own, so the page's HTML stays the same.
   Give it a title (`default###userTitle`, e.g. "Translation: Hero").
3. **Collect the texts from the preview, don't guess them.** Open the preview
   (glasses icon) and fetch the page from the local preview server
   (`127.0.0.1:<port>`). Under each Lingo Text a yellow notice lists
   "Texts without an entry" and "Not found on the page". The notice appears on
   every local address: `localhost`, `127.0.0.1` and names ending in `.test`,
   so a locally served export of the site shows it too (useful when the
   preview lacks files referenced from the site root).
   - Work until **"Texts without an entry" is empty.**
   - **"Not found on the page" may legitimately keep entries**: texts that only
     appear in some states or records (an empty-search message, a "New" badge,
     a 404 variant, a section that only some records have). Keep those entries;
     check each listed text against that rule instead of deleting it.
4. **Add entries in page order**: first entry with `stacks_add_stack` into the
   entry slot (`placement: inside`), each further one `placement: after` the
   previous entry. Then `stacks_set_stack_text_area` (`textIndex: 1`) and
   compare the returned text with what you sent.
5. For more than a handful of entries, drive the MCP from a small script
   (stdio, `/Applications/Stacks.app/Contents/Resources/stacks-mcp`) with the
   translations in a JSON file, instead of one tool call per entry.
6. **Lingo Switch** where the old language menu was. Field `form`
   (`links` / `kurz` / `menue`), `zeigt` (`name` / `kuerzel` / `beides`),
   `klasse` for extra CSS classes to match the site's look.
7. Feeds and other data per language: use `lingo_sprache()` in PHP-capable
   fields, e.g. a Feeds JSON path
   `" . (function_exists('lingo_sprache') ? lingo_sprache() : 'en') . "`.
   If the data only has some of the page's languages, fall back explicitly,
   otherwise a language without its own branch yields an empty feed:
   `" . (function_exists('lingo_sprache') && in_array(lingo_sprache(), ['en', 'de'], true) ? lingo_sprache() : 'en') . "`.

## Pitfalls

- The Stacks app reloads templates of a bundle only on restart. MCP changes
  are lost on restart unless the project was saved (Cmd+S) first.
- In the edit window no PHP or JavaScript runs; judge translations only in
  the preview or the published page.
- `?lang=xx` selects the language and is remembered in the cookie; the URL
  without `?lang` shows the cookie's or the default language. Detection only
  runs when neither exists.
