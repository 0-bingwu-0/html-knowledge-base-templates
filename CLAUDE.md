# CLAUDE.md

Guidance for reviewing changes in this repo.

## What this repo is

A collection of self-contained HTML knowledge-base template **kits**. Each kit pairs a **template** (the model's HTML target) with a **skill** (the slash command that fills it in), plus a working sample that demonstrates the loop.

The repo exists because good HTML *knowledge* templates — content-first, typographic, dependency-free, the equivalent of a well-typeset book chapter — are rare in the wild. Reviewers should keep that bar in mind. A kit that ships a landing-page-style template, or a skill that doesn't leverage model strengths, is technically valid but defeats the point.

Each top-level folder in the repo is one kit.

## Standard kit layout

A kit must be drop-in usable on its own. The expected layout:

```
<kit-name>/
├── README.md              # what it does + how to run the demo
├── skills/
│   └── <verb>/SKILL.md    # one folder per slash command — a kit can ship multiple
├── template/
│   └── index.html         # HTML skeleton with {{placeholders}}
└── <data-dir>/            # inputs and outputs (e.g. podcast/transcripts, podcast/notes)
```

New kits should mirror this layout. If a new kit genuinely needs a different shape, update this file to reflect the new shared convention — do not diverge silently.

## Creating a new kit

Pick the existing kit closest to what you want to build, copy its folder to `<your-kit-name>/`, then strip out the domain-specific content (sample data, kit-specific copy in README and SKILL.md) and fill in your own. Keep the standard layout above intact.

---

## Review checklist

### 1. Required content is present

- [ ] An HTML template at `template/index.html` (or a clearly documented alternative)
- [ ] At least one processing skill under `skills/<verb>/SKILL.md` with frontmatter (`name`, `description`)
- [ ] A `README.md` that states what the kit produces and gives the exact command to run the demo
- [ ] A minimal working sample: one input file and one rendered output, so the demo runs end-to-end without extra setup

### 2. Template and skill substance

These are the substantive checks. A kit that fails here doesn't belong in this repo, even if it passes everything else.

- [ ] The template reads like a content-first knowledge page: typographic, readable line measure, no landing-page or dashboard chrome. If it looks like a marketing site, it doesn't belong here.
- [ ] The skill leverages model strengths — structural extraction from unstructured input, judgment about what's worth keeping, language-aware rewriting. A skill that just performs regex + string substitution, without any model-driven extraction or judgment, doesn't need to live in this repo.

### 3. Nothing extraneous

Reject content that does not belong in the kit:

- [ ] No personal data, credentials, API keys, or `.env` files
- [ ] No large binaries (audio, video, full PDFs) — link to the source instead
- [ ] No editor / OS junk: `.DS_Store`, `*.swp`, `__pycache__/`, `node_modules/`, IDE configs
- [ ] No half-finished drafts, scratch files, or large commented-out blocks
- [ ] No files unrelated to this kit (random downloads, unrelated experiments)

### 4. Language and basic standards

This is a public GitHub repo. Repo content stays in English so anyone can read it:

- [ ] README, SKILL.md, code comments, commit messages, and PR descriptions are in English
- [ ] Sample *input data* may be in any language (it represents real-world input), but the metadata around it — filenames, slugs, frontmatter `description`, directory names — stays in English
- [ ] Markdown is standard CommonMark; avoid exotic extensions or proprietary syntax
- [ ] File and directory names are lowercased and use hyphens, never underscores or camelCase — including as field separators. E.g. `notes-zh/` (not `notes_zh/`), `lenny-2026-05-03-zh.html` (not `lenny-2026-05-03_zh.html`), `process-podcast` (not `Process_Podcast` or `processPodcast`)
- [ ] Dates in filenames and metadata use ISO format (`YYYY-MM-DD`), not localized forms
- [ ] No mixed-language identifiers (e.g. `获取data.py`, `processFn_中文.md`)

### 5. Naming

- [ ] Slash command / skill names are short verbs where possible (`/digest`, `/translate`), not nouns (`/podcast`) and not generic (`/process`)
- [ ] Source / channel slugs in filenames are short and recognizable (`lenny`, `how-i-ai`), not the full official name
- [ ] Output filenames follow a documented pattern in the kit's README or SKILL.md

### 6. Sample data hygiene

Samples are meant to make the demo work — not to be archives:

- [ ] One representative sample per kit, not many
- [ ] Strip or generalize private content: personal email addresses, phone numbers, private URLs, internal company names that aren't relevant to the demo
- [ ] If the sample references a real public person or episode, include a link to the public source so provenance is clear
- [ ] Re-running the documented command on the sample input still produces the committed sample output (no stale outputs)

### 7. Code correctness

- [ ] All `{{placeholders}}` in the template are replaced by the processing skill — no leftover braces in rendered output
- [ ] Rendered HTML is well-formed and renders in a browser
- [ ] The demo command documented in the kit's README actually runs and produces the documented output filename

---

## How to use this file when reviewing

Walk the checklist top to bottom. Items 1–4 are blocking — if any fail, request changes. Items 5–7 are usually fixable inline and worth a comment but not necessarily a block.
