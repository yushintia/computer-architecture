# Computer Architecture (503872-004)

Markdown-driven web slides for Computer Architecture, DEU 2026-2, built
with [Marp](https://marp.app/), themed to match `shintia-template.pptx`.
Deployed via GitHub Pages, see `.github/workflows/pages.yml`.

Read `SPINE.md` first: it defines the mandatory pedagogical structure
every week's deck must follow (motivation before definition, weeks
chained via a Limits -> Pain handoff). Deck content should never drift
from that document without updating it too. `OUTLINE.md` has the full
15-week plan and chain table.

## Layout

```
SPINE.md                 standard structure, read this first
OUTLINE.md                15-week plan + Limits -> Pain chain
themes/shintia.css        Marp theme matching the pptx template
assets/deu-logo.png       extracted university logo
slides/
  _template/week-XX.md    copy this to start a new week
  _shared/roadmap.md      Act-0 roadmap table, paste into slot 2
  week01-introduction.md
  ...(weeks 2-15 not yet drafted)
materials/week01/          handout, worksheet (pair exercise), self-check quiz for Week 1
```

## Setup

Requires Node.js. First run installs marp-cli into `node_modules` via
`npx`. No separate `npm install` step needed.

```bash
npx @marp-team/marp-cli --version   # confirms marp-cli resolves
```

## Preview in a browser (live reload)

```bash
npx @marp-team/marp-cli -s slides --theme-set themes/shintia.css
```

## Zero-install alternative: VS Code

Install the **Marp for VS Code** extension, open any `slides/*.md` file,
and use the built-in preview pane. To pick up the custom theme, add to
VS Code settings:

```json
"markdown.marp.themes": ["./themes/shintia.css"]
```

## Export

```bash
npm run build:html   # -> dist/*.html, self-contained, open directly in a browser
npm run build:pdf     # -> dist/*.pdf
npm run build:pptx    # -> dist/*.pptx, for LMS upload alongside the original template
```

## Adding a new week

1. Copy `slides/_template/week-XX.md` -> `slides/weekNN-topic.md`, fill
   in all 17 spine slots (see `SPINE.md`).
2. Paste the current table from `slides/_shared/roadmap.md` into slot 2,
   bold the new current week's row.
3. Preview, check against `SPINE.md`'s hard rule: no formal definition
   before slot 8.
