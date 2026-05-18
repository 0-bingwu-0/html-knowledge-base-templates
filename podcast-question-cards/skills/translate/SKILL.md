---
name: translate
description: Translate a rendered Q&A card HTML in podcast/notes/ into a target language. Takes a language code argument (e.g. zh, ja, es) and writes to podcast/notes-<lang>/. Preserves template structure and only swaps text content.
---

You translate a rendered Q&A card HTML page into a target language.

Goal:
Produce a localized version of an English Q&A card page without touching layout, styles, or markup — only the text content is translated.

---

USAGE

```
/translate <lang> <path-to-source-html>
```

Example:

```
/translate zh podcast/notes/lenny-2026-05-03.html
/translate ja podcast/notes/lenny-2026-05-03.html
```

Where `<lang>` is an ISO 639-1 code (`zh`, `ja`, `es`, `fr`, `de`, ...). For Chinese, default to Simplified (`zh` → zh-CN) unless `zh-TW` is given explicitly.

---

INPUT

A rendered Q&A card HTML file produced by [[digest]], typically at:

podcast/notes/{channel_slug}-{published_date}.html

---

OUTPUT FILE

Write the translated HTML to:

podcast/notes-{lang}/{channel_slug}-{published_date}-{lang}.html

Example:

- input  → `podcast/notes/lenny-2026-05-03.html`
- `/translate zh` → `podcast/notes-zh/lenny-2026-05-03-zh.html`
- `/translate ja` → `podcast/notes-ja/lenny-2026-05-03-ja.html`

Create the `podcast/notes-{lang}/` directory if it does not exist.

Do NOT paste HTML into chat.
The chat response should only say:

Created podcast/notes-{lang}/{filename}

---

WHAT TO TRANSLATE

Translate the human-readable text content:

- `<title>` and the episode title heading
- `episode-meta` items: source, guest, published date, etc.
- The `url_display` link text (keep the `href` URL itself unchanged)
- Each card's question (`.qa-question`)
- Each card's one-sentence answer (`.qa-answer`)
- Each card's source passage inside `<blockquote>`, including speaker labels

---

WHAT NOT TO TOUCH

- HTML tags, attributes, class names, ids, inline styles
- The template skeleton, CSS, and any `<style>` / `<script>` blocks
- `href` URL values (translate only the visible link text)
- Card numbering — it is CSS-generated, do not write numbers into the HTML
- The `.qa-toggle` element — it stays empty; do not add labels like "原文片段" or "Read transcript"
- Proper nouns and technical terms: **never translate or transliterate** people names, company names, product names, or technical vocabulary. Keep them verbatim in the source language — no parenthetical glosses, no romanizations, no native-form substitutions, even when an established translation exists.
- Verified spellings from the English version — do not re-romanize or re-translate names

---

LANGUAGE & STYLE

- Use natural, idiomatic phrasing in the target language. Do not translate word-for-word.
- Keep all technical vocabulary verbatim in the source language (e.g. `agency`, `product-market fit`, `RAG`). Do not translate or gloss it, even on first mention.
- Preserve the speaker's voice in `<blockquote>` source passages — keep them conversational, not formal prose. Do not "clean up" colloquialisms.
- Preserve paragraph breaks and speaker labels inside `<blockquote>` (e.g. `Host:`, `Max:`) — translate the label words but keep the structure.

---

PUBLISHED DATE

Re-render `{{published_date}}` in a form consistent with the target language:

- `zh` → `2026 年 5 月 3 日`
- `ja` → `2026年5月3日`
- `es` → `3 de mayo de 2026`
- `fr` → `3 mai 2026`
- `de` → `3. Mai 2026`
- default to the locale's conventional long date form

---

HTML HEADER

Update the document language attribute:

- `<html lang="en">` → `<html lang="{lang}">` (use the full tag where appropriate: `zh-CN`, `zh-TW`, `pt-BR`)

Keep the `<meta charset="utf-8">` and viewport meta as-is.

---

QUALITY CHECKS

- Every visible English string is translated; no stray English text remains except intentionally-kept proper nouns and technical terms.
- The translated answer still matches the question (no semantic drift).
- The source passage still supports the answer — if a translation changes the meaning, re-translate, do not rewrite the answer.
- If the source HTML has an actual error in the English text, translate faithfully first, then append a single translator note at the very end of the page in a `<p class="translator-note">…</p>` outside the card list.
