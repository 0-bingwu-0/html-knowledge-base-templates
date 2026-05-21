# lecture-case-cards

Turn a corpus of course lecture transcripts into a single browsable HTML "atlas" of company case studies, with one card per company.

The sample corpus shipped here is Stanford **CS183B — How to Start a Startup** (Sam Altman, Fall 2014): 20 lectures of guest speakers (founders of Airbnb, Stripe, Facebook, PayPal, LinkedIn, Pinterest, Twitch, DoorDash, Teespring, Wufoo, Palantir, etc.) using real companies as teaching examples. The skill extracts every company that gets a *narrative* — founding story, scrappy early tactic, illustration of a named principle — and renders it into one card with five fixed fields:

- **Company name**
- **Mentioned in** (which lectures)
- **Context at the time** (what the company looked like when the speaker described them)
- **What happened later** (the outcome — IPO, acquisition, scale, fade)
- **Pattern** (the generalizable startup lesson the speaker was illustrating)

## Layout

```
lecture-case-cards/
├── README.md
├── skills/
│   └── extract-startup-ideas/SKILL.md   # transcripts → case cards
├── template/
│   └── index.html                       # HTML skeleton for the cards
└── course/
    ├── transcripts/                     # input: one .md per lecture
    └── notes/                           # output: rendered HTML atlas
```

## See what the output looks like

A pre-baked example is committed so you can preview the result before running anything:

- corpus: `course/transcripts/Lecture01-*.md` … `Lecture20-*.md` (20 lectures)
- rendered atlas: `course/notes/startup-ideas-cs183b-all.html` (24 case cards)

Open the HTML file in a browser to read it.

## Try it yourself

Re-run the full extraction against the committed corpus:

```
/extract-startup-ideas
```

After a couple of minutes you'll see `Created course/notes/startup-ideas-cs183b-all.html — N companies across L lectures.` Open it to compare against the committed sample.

To extract a narrower scope, pass a filter:

```
/extract-startup-ideas Lecture 8 only
/extract-startup-ideas Airbnb only
/extract-startup-ideas just the do-things-that-don't-scale pattern
```

The output filename follows `course/notes/startup-ideas-{scope-slug}.html`, e.g. `startup-ideas-lecture-08.html`.

## Adding a new course

Drop the lecture transcripts as Markdown into `course/transcripts/`, one file per lecture:

```
course/transcripts/Lecture01-<short-topic>.md
course/transcripts/Lecture02-<short-topic>.md
…
```

Then update the seed-grep regex inside `skills/extract-startup-ideas/SKILL.md` with the companies you'd expect to see in the new course, and run `/extract-startup-ideas`.

## Source

The sample transcripts are the publicly available course materials from Stanford CS183B (Fall 2014). Original course site: <https://startupclass.samaltman.com/>. No edits beyond light formatting for Markdown.
