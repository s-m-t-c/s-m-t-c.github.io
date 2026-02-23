# Documentation

This document is internal project documentation for `/Users/seachu/Documents/s-m-t-c.github.io`.
It is intentionally not rendered into the public website.

## 1) Intent and Ethos

- Keep the site fast, static, and legible first.
- Prioritize text clarity over UI complexity.
- Keep dependencies light and avoid client-side framework overhead.
- Use progressive disclosure for depth: start concise on the homepage, then reveal detail only when needed.
- Preserve a human editorial voice; avoid "platform-like" interaction patterns.

Design references discussed for direction:
- [Gwern design principles](https://gwern.net/design#principles)
- [Fabien Sanglard](https://fabiensanglard.net/)
- [Dan Luu](https://danluu.com/)

## 2) Architecture Snapshot

Stack:
- Jekyll (static generation)
- Sass (`style.scss` + `_sass/*`)
- Data-driven homepage content from YAML

Core files:
- `/Users/seachu/Documents/s-m-t-c.github.io/index.html`:
  - Renders About section.
  - Iterates section definitions from `_data/home_sections.yml`.
- `/Users/seachu/Documents/s-m-t-c.github.io/_includes/timeline-section.html`:
  - Filters entries by section key.
  - Sorts by configured field and direction.
  - Renders each entry in a clean list with year metadata.
- `/Users/seachu/Documents/s-m-t-c.github.io/_data/home_sections.yml`:
  - Controls section ordering, labels, and sort behavior.
- `/Users/seachu/Documents/s-m-t-c.github.io/_data/projects.yml`:
  - Single source of truth for research/art timeline entries.
- `/Users/seachu/Documents/s-m-t-c.github.io/_includes/about_intro.html`:
  - Canonical short bio used by both homepage and about page.

## 3) Content Data Model

Each project entry in `_data/projects.yml` currently uses:
- `id`: stable unique key.
- `section`: `research` or `art_sound`.
- `year`: display year.
- `sort_date`: machine-sortable date key for ordering.
- `featured`: boolean flag for Featured curation.
- `featured_rank`: manual ordering key for Featured entries.
- `content_html`: inline HTML content rendered on homepage.

Rationale:
- A single list supports multiple views (chronological timeline, curated featured set, and future project pages).
- `featured` and `featured_rank` decouple editorial priority from date order.

## 4) Design Language and Guardrails

Typography and rhythm:
- Keep body text comfortably readable across desktop/mobile.
- Maintain a restrained heading scale and consistent vertical spacing.
- Underlined links are the default affordance, with visible hover/visited states.

Layout:
- Single-column reading experience with low cognitive overhead.
- Avoid dense cards/grids unless a specific content type requires them.
- Preserve whitespace between entries to keep scanning easy.

Accessibility:
- Do not depend on color alone for interaction cues.
- Keep contrast strong and touch targets readable on mobile.
- Keep markup semantic and avoid decorative complexity that reduces clarity.

## 5) Featured Section Plan (Scalable)

Goal:
- Highlight a small set of important projects independent of recency.

Recommended rollout:
1. Data-only curation (already supported):
   - Mark entries with `featured: true`.
   - Set `featured_rank` for manual order.
2. Homepage Featured block:
   - Add a section that reads from the same `_data/projects.yml`.
   - Render 3-5 entries with one-line context.
3. Deep detail layer:
   - Add optional detail pages for major projects.
   - Keep homepage concise and route richer media/text to project pages.

Guideline:
- Keep timeline chronological.
- Keep Featured editorial.
- Do not force all content into one ordering system.

## 6) Editing Workflow

Add/update an entry:
1. Edit `/Users/seachu/Documents/s-m-t-c.github.io/_data/projects.yml`.
2. Set `section`, `year`, `sort_date`, and `content_html`.
3. Optionally set `featured` and `featured_rank`.
4. Preview locally with:
   - `./bin/serve`
   - or `BUNDLE_PATH=vendor/bundle bundle exec jekyll build`

Adjust section ordering/sorting:
1. Edit `/Users/seachu/Documents/s-m-t-c.github.io/_data/home_sections.yml`.
2. Reorder list items or change `sort_by` / `sort_direction`.

## 7) Near-Term Backlog

- Implement a homepage Featured block that uses existing `featured` fields.
- Add per-project pages for "big" projects with photos/media and longer text.
- Define a minimal project-page template so content can grow without visual drift.
- Consider optional inline "expand" details on homepage only if it stays readable on mobile.
