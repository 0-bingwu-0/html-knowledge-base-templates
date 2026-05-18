# html-knowledge-base-templates

HTML templates for knowledge bases, paired with the skills that fill them in.

## Why HTML for notes

HTML used to lose because humans had to write it.

A self-contained HTML file gives you rich layout, mixed media, and interactivity — in a format that still works long after the tool that produced it disappears.

Very few formats match that combination.

We settled for less because hand-writing HTML for every reading note, meeting recap, and paper summary is not a thing humans are willing to do. Markdown won the note-taking format wars not because it's more expressive — it's strictly less — but because it's the lowest-friction text format a human can type. Obsidian, Notion, and Bear all default to Markdown or something Markdown-like for the same reason.

That constraint just disappeared. A model writing HTML isn't slower or harder than a model writing Markdown — to an LLM, both are just text. If we're not the ones hand-typing the file, there's no reason to keep absorbing Markdown's limits: no real typography, no image-text layouts, no expandable sections, no controlled layout.

Markdown isn't going anywhere. It's still the right format for quick drafts, journals, and files you'll edit by hand, and the two will coexist for a long time. But for the *finished, shareable, archival* version of a note, HTML is what you want — and the cost of producing it just collapsed.

## The missing piece

The blocker now isn't generation. Models can already do that. It's templates.

The web is overflowing with HTML for landing pages, admin dashboards, portfolio sites, and marketing kits. **HTML knowledge templates barely exist.** Drop-in templates designed for long-form reading content — typographic, content-first, dependency-free, the equivalent of a well-typeset book chapter — are surprisingly hard to find.

This repo is a collection of them. Each kit is a template plus the skill that fills it in. Drop in raw content, run a slash command, get a finished HTML page.

## What's here

Each top-level folder is a self-contained **kit** — a template + its skill(s) + a sample:

- [`podcast-question-cards/`](podcast-question-cards/) — long-form interview transcripts → Q&A knowledge cards with expandable source passages

(more kits to come)

## Contributing

Each kit follows the layout and review rules in [`CLAUDE.md`](CLAUDE.md). To add a new kit, see the **Creating a new kit** section.
