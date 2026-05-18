# podcast-question-cards

Turn long-form interviews / podcasts into Q&A card HTML pages.

## Layout

```
podcast-question-cards/
├── README.md
├── skills/
│   ├── digest/SKILL.md            # transcript → question cards (English by default)
│   └── translate/SKILL.md         # question cards → translated cards
├── template/
│   └── index.html                 # HTML skeleton for the cards
└── podcast/
    ├── transcripts/               # input: raw transcript markdown
    ├── notes/                     # output: question cards (English by default)
    └── notes-<lang>/              # output: translated cards (e.g. notes-zh/)
```

## See what the output looks like

A pre-baked example is committed so you can preview the result before running anything:

- transcript: `podcast/transcripts/lenny-2026-05-03.md`
- question cards: `podcast/notes/lenny-2026-05-03.html`
- translated Chinese question cards: `podcast/notes-zh/lenny-2026-05-03-zh.html`

Open either HTML file to read the cards — click `+` on any card to expand the supporting transcript.

## Try it yourself

A second transcript is included so you can run the pipeline end-to-end:

```
/digest podcast/transcripts/lenny-2026-05-11.md
```

After ~30 seconds you'll see `Created podcast/notes/lenny-2026-05-11.html`. Open it to read the cards you just generated.

To produce a translated version, pass a language code:

```
/translate zh podcast/notes/lenny-2026-05-11.html
```

This writes `podcast/notes-zh/lenny-2026-05-11-zh.html`. Replace `zh` with any ISO 639-1 code (`ja`, `es`, `fr`, …) to translate into other languages.

## Adding a new episode

Save the YouTube auto-captions (or any transcript) as markdown at:

```
podcast/transcripts/<channel-slug>-<YYYY-MM-DD>.md
```

Then run the same `/digest` command. You don't need to fill in metadata by hand — the skill looks up the episode online.
