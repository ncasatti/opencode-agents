---
name: html-generator
description: Builds standalone HTML documentation pages styled with the "Brutalist Command" terminal aesthetic. The agent writes complete, self-contained HTML directly — no build step, no runtime, no dependencies beyond the CDN-loaded Tailwind and Space Grotesk references inside each file. Three page archetypes are supported `landing` (project entrypoint / readme), `reference` (API or CLI docs), and `architecture` (system specs / ADRs). Use when the User asks to render documentation as HTML, generate a static doc site, produce a styled documentation portal, or create a single-page HTML doc with the Brutalist Command theme.
version: 2.0.0
---

# Static HTML Generator

This skill is a design system, not a build tool. The agent is the builder: it writes `.html` files directly using the patterns defined in `theme/`. There is no script, no `npm install`, no runtime — every output file is a self-contained, browser-ready HTML document that loads its CSS via the Tailwind CDN.

## Theme Path (Reference Only)

The theme lives at a fixed absolute path. The agent reads from it; it never copies the files into the project.

- Design bible: `~/.the-grid/programs/skill/html-generator/theme/DESIGN.md`
- Snippet library: `~/.the-grid/programs/skill/html-generator/theme/COMPONENTS.md`
- Full-page examples: `~/.the-grid/programs/skill/html-generator/theme/examples/{readme,reference,architecture}.html`
- Visual references: `~/.the-grid/programs/skill/html-generator/theme/assets/*.png`

## Standard Project Layout (Mandatory)

Every project consuming this skill adopts:

```
docs/
  index.html          ← landing page (readme archetype)
  pages/              ← secondary pages
    reference.html    ← reference archetype
    architecture.html ← architecture archetype
    <other>.html
```

Every output is a complete `.html` file. There is no separate Markdown source directory and no build artifact directory — the HTML *is* the source. Commit the whole `docs/` tree to the repo. This layout is compatible with GitHub Pages (`Settings → Pages → Source: /docs`).

## Quick Start

| Content type | Archetype | Hero variant | CRT overlay |
|---|---|---|---|
| Project README / landing | `landing` | Solid cyan headline | No |
| API reference / CLI docs | `reference` | Side-bordered with crumb | No |
| Architecture / ADR / system spec | `architecture` | White headline + cyan period | Yes |

## Discovery Protocol (Agent-First)

The agent gathers requirements before producing any file. It generates content dynamically from the conversation; pre-existing HTML files are honored when present.

### Phase 1 — Content Audit

Resolve all five before writing any file:

1. Does `docs/html/` already contain rendered `.html` files? If yes → offer to use them as-is, regenerate from scratch, or extend them.
2. What is the subject? (project, tool, topic being documented)
3. What pages are needed? (e.g., landing + reference, or landing + architecture + reference)
4. Which archetype fits each page? (`landing`, `reference`, `architecture`)
5. Any specific sections, content, or constraints to include or exclude?

### Phase 2 — Execution

1. Create `docs/` and `docs/pages/` if missing.
2. For each requested page:
   - Open the matching `theme/examples/<archetype>.html` as a structural reference.
   - Open `theme/COMPONENTS.md` to copy the exact snippet patterns needed.
   - Open `theme/DESIGN.md` for any color, typography, or spacing decision not covered by a snippet.
   - Write the complete `.html` file directly. No external CSS, no JS bundles, no build step. Tailwind and Space Grotesk are loaded inline via CDN inside the file.
3. Cross-link the pages: every secondary page links back to `../index.html` ("Return to Entry Point") and the landing page links forward to each secondary page.
4. Report output paths to the User.

### Sample Discovery Dialogue

> **Agent:** I do not find any `.html` files in `docs/`. What are we documenting? Give me the subject and a rough list of pages.
> **User:** My CLI tool `clingy` — landing page and a command reference.
> **Agent:** Two pages. `docs/index.html` as the landing using the `landing` archetype, and `docs/pages/reference.html` using the `reference` archetype. Sections I'd include on the landing: prerequisites, install sequence, navigation cards. On the reference: command flags, exit codes, and a contracts strip. Confirm the sections or add what is missing.
> **User:** Include installation, quickstart, and all the flags. Go.
> **Agent:** Writing `docs/index.html` with the cyan-headline hero, prerequisites card, three-step install grid, and four navigation tiles — then `docs/pages/reference.html` with the side-bordered hero, flag list, and three contract cards. Standalone HTML, no build step.

## Archetype Selection Map

| Archetype | Use for | Layout signature | Reference file |
|---|---|---|---|
| `landing` | Landing pages, project entrypoints, general docs | TopNavBar + SideNavBar + cyan-headline hero + bento card grid + footer | `theme/examples/readme.html` |
| `reference` | API docs, technical references, CLI docs | TopNavBar + SideNavBar + side-bordered hero + bento (endpoints, flags, contracts) | `theme/examples/reference.html` |
| `architecture` | System specs, ADRs, design docs | SideNavBar + TopNavBar + cyan-period hero + bento (overview, directory map, data flow) + CRT overlay + vignette | `theme/examples/architecture.html` |

## Build Recipe (per page)

For every `.html` file the agent produces, follow this sequence:

1. **Boilerplate.** Start from the matching `theme/examples/<archetype>.html`. Replace placeholder titles, copy, and links with the User's content.
2. **Hero.** Pick the hero variant from `COMPONENTS.md §4` that matches the archetype. Do not mix variants.
3. **Body.** Drop in the prose paragraphs, then assemble the bento grid using snippets from `COMPONENTS.md §5`. Keep the 12-column rhythm; vary column spans to create asymmetry.
4. **Specialty blocks.** Add reference-specific (endpoints, flag list, contracts) or architecture-specific (directory tree, data flow, CRT overlay) blocks from `COMPONENTS.md §7–§11`.
5. **Footer.** Pick `§10a` for landing pages or `§10b` for versioned reference / architecture pages.
6. **Cross-links.** Confirm every internal link resolves to a real sibling file.

## Theme Contract — "The Brutalist Command"

The User will see:
- Background `#050505`, surface panels `#0A0A0A`, accent cyan `#00FFFF`.
- Strict monospace-feeling typography (Space Grotesk family), uppercase headers, cyan period accents.
- Zero rounded corners, no easing curves — `transition-duration: 0ms` everywhere; `transition-none` is the default Tailwind class.
- `architecture` archetype adds a global CRT scanline overlay and corner vignette.
- Tonal stacking instead of shadows. The "No-Line" rule: layout boundaries are background shifts, not 1px lines. The only sanctioned hairline is `border-[#4B5563]/15` for ghost borders inside panels.

Reference: `theme/DESIGN.md` for the full design system; `theme/COMPONENTS.md §1` for the color token table.

## Operational Constraints

- **Self-contained output.** Every `.html` file must work when opened directly in a browser with no companion files. CSS is loaded via the Tailwind CDN inside the file; fonts via Google Fonts; no local JS bundles.
- **No build step.** Do not introduce `package.json`, `node_modules`, build scripts, or watchers.
- **No frameworks.** No React, no Vue, no static-site generators. Plain HTML and Tailwind utility classes only.
- **Version control.** Never staged or committed by this skill. All `git` actions remain manual.
- **Idempotency.** Re-running the agent for the same page must produce equivalent output for equivalent input. Do not add timestamps or random IDs to the markup unless the User asks.

## Theme Files Reference

| File | Role |
|---|---|
| `theme/DESIGN.md` | The design bible — palette, typography, elevation, do/don't. |
| `theme/COMPONENTS.md` | The snippet library — copy-ready HTML fragments with usage notes. |
| `theme/examples/readme.html` | A complete rendered landing page. Open it side-by-side while building. |
| `theme/examples/reference.html` | A complete rendered reference page. |
| `theme/examples/architecture.html` | A complete rendered architecture page. |
| `theme/assets/*.png` | Screenshots of the rendered examples. |

End of line.
