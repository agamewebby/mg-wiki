# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

A Myasthenia Gravis (MG) knowledge base consisting of:

- **`raw/`** — source research files: markdown notes, PDFs, and AI-generated research documents. These are the primary inputs to the wiki.
- **`wiki/`** — a patient-facing wiki compiled from the raw sources. 21 markdown pages covering symptoms, causes, all treatment categories, diagnosis, lifestyle, crisis management, and the research pipeline.

There is no build system, no tests, and no code. The "workflow" is editorial: new research lands in `raw/`, then gets synthesised into `wiki/`.

## Keeping the wiki in sync

Use the `/mg-wiki-sync` skill to update the wiki from raw sources. It:

1. Detects which `raw/` files are newer than `wiki/index.md` (the sync timestamp)
2. Reads changed files and maps content to wiki pages
3. Updates affected wiki pages without duplicating existing content
4. Creates new wiki pages if needed
5. Updates the `*Last updated: YYYY-MM-DD (sync N)*` line in `wiki/index.md`

After syncing, commit and push:
```bash
git add wiki/ && git commit -m "wiki: sync N — brief description of what changed"
git push
```

## Adding new research

Drop files into `raw/` then run `/mg-wiki-sync`. Supported formats: `.md` and `.pdf` (the Read tool handles PDFs natively).

To generate new research using the Gemini CLI:
```bash
gemini -p "<research query>"
```
Save the output as a `.md` file in `raw/` before syncing.

## Wiki structure and conventions

Every wiki page follows this structure:
- H1 title
- Brief intro paragraph
- H2 major sections, H3 sub-topics
- `## Related pages` section at the bottom with `[Page Title](filename.md)` links

Internal links use the format `[Page Title](filename.md)` — no subdirectory prefix needed since all wiki pages are siblings.

**Tone:** Warm and accessible — written for patients and carers, not medical professionals. Explain medical terms on first use.

**No duplication:** If the same information belongs on multiple pages, write it once on the most relevant page and cross-link from others.

## Raw-to-wiki topic mapping

| Raw content topic | Wiki page(s) |
|---|---|
| What MG is, overview, NMJ | `what-is-mg.md` |
| Types, classifications, antibodies | `types.md` |
| Symptoms, muscle groups, fatiguability | `symptoms.md` |
| Causes, pathophysiology, immune mechanisms, T-cells, Tregs | `causes.md` |
| Diagnosis, tests, EMG | `diagnosis.md` |
| Treatments overview | `treatments.md` |
| Pyridostigmine, symptomatic | `treatments-symptomatic.md` |
| Steroids, azathioprine, mycophenolate | `treatments-immunosuppression.md` |
| Biologics, FcRn inhibitors, complement inhibitors, rituximab | `treatments-biologics.md` |
| Thymectomy | `treatments-surgical.md` |
| IVIG, plasmapheresis, crisis management | `treatments-acute.md` |
| CAR-T, gene therapy, pipeline drugs | `treatments-emerging.md` |
| Myasthenic crisis, triggers, hospital | `myasthenic-crisis.md` |
| Drugs to avoid, interactions | `drugs-to-avoid.md` |
| Diet, alcohol, exercise, lifestyle | `diet-lifestyle.md` |
| Skin, immunosuppressant side effects | `skin-immunosuppressants.md` |
| Daily living, tips, practical advice | `living-with-mg.md` |
| Research, clinical trials, future outlook | `research-future.md` |
| Anaesthesia | `anaesthesia.md` |
| Pregnancy | `pregnancy-and-mg.md` |

## GitHub

Repository: `agamewebby/mg-wiki`
Branch: `main`
