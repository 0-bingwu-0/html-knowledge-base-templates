---
name: digest
description: Read a full YouTube / podcast transcript from podcast/transcripts/ and extract high-quality Q&A knowledge cards, rendered into podcast/notes/ using the template at template/index.html.
---

You read a full YouTube transcript and extract high-quality Q&A knowledge cards.

Goal:
Turn a long-form conversation into punchy, standalone question-answer cards with expandable transcript evidence.

Use the HTML template in:

template/index.html

Do not invent a new layout.
Only replace placeholders and repeat the QA card block.

---

INPUT FILE

Read the transcript from:

podcast/transcripts/{channel_slug}-{published_date}.md

Example: `podcast/transcripts/lenny-2026-05-03.md`

---

OUTPUT FILE

Write the rendered HTML to:

podcast/notes/{channel_slug}-{published_date}.html

Rules:
- `channel_slug`: short lowercased slug of the source/channel name (e.g. "Lenny's Podcast" → `lenny`, "How I AI" → `how-i-ai`). Strip apostrophes, replace spaces with hyphens, drop punctuation. Prefer a short recognizable form over the full channel name.
- `published_date`: ISO format `YYYY-MM-DD`. Verify from the video / podcast page if not explicitly given.
- If `published_date` cannot be verified, fall back to `{channel_slug}-{episode-slug}.html` using a short hyphenated slug of the episode title.

Example: `podcast/notes/lenny-2026-05-03.html`

Do NOT paste HTML into chat.
The chat response should only say:

Created podcast/notes/{filename}

---

INPUT

The input may include:
- episode title
- source / show name
- guest name and role
- published date
- original URL
- full transcript

Use metadata exactly as provided.
Do not invent missing metadata.
If a metadata field is missing, omit that <li> entirely from the episode-meta list.

---

METADATA CORRECTNESS

Before writing the HTML, sanity-check metadata against the original source:

- **Episode title**: use the exact original title from the video / podcast page. Do not paraphrase, rewrite, translate, or "improve" it. If the URL is provided, fetch/search to confirm the canonical title.
- **Published date**: must appear in the rendered page (inside `episode-meta`), not only in the filename. Verify from the video / podcast page if not explicitly given. Render it in a readable form consistent with the page's language (e.g. "May 3, 2026" for English pages, "2026 年 5 月 3 日" for Chinese pages).
- **Guest name and other proper nouns** (people, companies, products): transcripts are auto-generated and frequently misspell names phonetically. Identify likely misspellings (especially the guest and anyone referenced repeatedly) and verify the correct spelling from the video description, episode notes, or a web search. Apply corrections consistently across both metadata and every source passage.

If you cannot verify a name with reasonable confidence, keep the transcript spelling and do not guess.

---

CARD SELECTION

Extract only topics that are:

- substantively discussed
- concretely tied to real companies, technologies, industries, policies, products, markets, roles, or social changes
- understandable without watching the episode
- still interesting after the episode is forgotten

Prefer fewer strong cards over many weak ones.

Skip:

- filler
- biography
- generic life advice
- one-off tangents
- vague trend talk
- repeated points
- shallow summaries

Merge duplicate kernels across the episode.
Keep the clearest version with the richest supporting exchange.

---

QUESTION RULES

Each question should:

- be 8–18 words
- be one sentence
- end with "?"
- feel like a debate prompt or strong headline
- create a real contested answer space

Avoid:

- vague essay prompts
- "A or B?" framing
- smuggled assumptions
- jargon-only wording

---

ANSWER RULES

Write ONE sharp declarative sentence.

Rules:

- 10–25 words
- no hedging
- no "the speaker argues"
- no balance framing
- concrete and opinionated
- faithfully reflect the video's stance

---

SOURCE PASSAGE

Each card must include the FULL supporting transcript exchange.

Start where the topic is introduced.
End when the conversation meaningfully moves on.

Include:

- host questions
- guest answers
- back-and-forth
- clarifications
- disagreements

Do not paraphrase transcript text.
Err on the side of MORE context.

When the transcript misspells a verified name, silently correct it inside the source passage too — do not annotate or [sic] it.

---

HTML RENDERING RULES

Use the template file exactly.

Replace these top-level placeholders:

- {{episode_title}}   (the exact original title — never rewritten)
- {{source}}
- {{guest}}
- {{published_date}}   (always rendered in the page, in a form consistent with the page's language)
- {{url}}
- {{url_display}}   (short display text for the link, e.g. "youtube.com/watch")
- {{card_count}}
- {{cards}}

If a metadata field is missing, delete its entire <li> from the episode-meta list. Do not leave a placeholder or an empty bullet behind. The published date is required and should always be present in the meta list when known.

For each card, render one QA card block using this exact structure:

<li class="qa-item">
  <div class="qa-num"></div>
  <details class="qa-body">
    <summary class="qa-summary">
      <div class="qa-header-row">
        <h2 class="qa-question">{{question}}</h2>
        <span class="qa-toggle" aria-hidden="true"></span>
      </div>
      <p class="qa-answer">{{answer}}</p>
    </summary>
    <blockquote>{{source_passage}}</blockquote>
  </details>
</li>

Per-card field rules:

- {{question}}: the question text only, no quote marks, no prefix
- {{answer}}: the one-sentence answer, no quote marks, no prefix
- {{source_passage}}: the full transcript exchange, with speaker labels preserved
- The toggle (.qa-toggle) is a CSS-rendered + icon. Do not add any text inside it. Do not add labels like "Read the transcript" or "原文片段".

Other rules:

- preserve speaker labels in the source passage (e.g. "Host:", "Max:")
- preserve meaningful paragraph breaks inside <blockquote> using blank lines
- escape HTML-sensitive characters in all rendered text: & → &amp;, < → &lt;, > → &gt;. For apostrophes in names like "Lenny's", use &rsquo; for typographic quality
- do not use the "open" attribute on <details>
- card numbering (01, 02, …) is generated automatically by CSS — do not write numbers into the HTML
- do not generate cards without clear transcript evidence
