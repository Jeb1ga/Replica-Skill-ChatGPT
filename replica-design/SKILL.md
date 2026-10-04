---
name: replica-design
description: Use when rebuilding a clone design system, defining color roles, type, spacing, accessible components and design tokens.
---

# replica-design

Reads `replica/recon.md` and the screenshots in `replica/screens/`. Writes
`replica/design/tokens.json` (template in this folder), `tokens.css`, the
Tailwind mapping, and `replica/design/components.md`.

```bash
python3 <skill-root>/contrast.py replica/design/tokens.json     # every text pair, WCAG ratio
```

## The rules

What you rebuild is the **system**: the roles, the scale, the patterns, the
way a form or a modal behaves. Those are not ownable, and users expect them.
What you never take:

- **Logos, icons, illustrations, photos, sounds.** Use an open icon set
  (Lucide, Phosphor, Heroicons, Tabler, all MIT or similar) and make or
  commission your own illustrations. Do not trace theirs.
- **Licensed fonts.** If the original uses a paid or proprietary font, pick
  an open one with the same job: Inter, Geist, IBM Plex, Manrope, Source Serif.
- **Their copy.** Every label and empty state gets written fresh.
- **Their brand colour.** Record it as a role (`accent`), use a neutral
  placeholder now, and replica-brand gives you your own. The signature colour
  plus the signature layout is trade dress, and it changes before launch.

## Step 1: measure, do not guess

From the screenshots (zoom in, use a colour picker on the user's machine):

- **Colour roles**, not colours: bg, surface, border, border-input, text,
  text-muted, accent, on-accent, danger, success, warning. Count how many
  greys the app really uses. Usually 5 to 7.
- **Type scale**: sizes, line heights, weights. Snap to a scale (12, 14, 16,
  20, 28, 40 is common). Note the font category, not the font file.
- **Spacing**: measure gaps between elements. It is almost always a 4 or 8
  base. Write the scale.
- **Radius, shadow, motion**: two or three of each.
- **Layout**: max content width, grid, breakpoints, sidebar width, header height.

## Step 2: write the tokens

Fill `tokens.json`. Keep the role names. replica-brand only changes values.
Generate `tokens.css` as custom properties and map them into Tailwind's theme
so components use `bg-surface text-muted`, never raw hex.

Add a `pairs` list for every text and background combination the app uses,
then:

```bash
python3 <skill-root>/contrast.py replica/design/tokens.json
```

AA is the floor: 4.5:1 for body text, 3:1 for large text and for input
borders and focus rings. It exits 1 on a failure. Fix it in the tokens, not
per component.

## Step 3: component specs

For every component in the recon list, one block in `components.md`:

```
Button
  variants  primary, secondary, ghost, danger
  sizes     sm 32px, md 40px, lg 48px
  states    default, hover, active, focus-visible (2px ring, accent), disabled, loading
  tokens    bg accent, text on-accent, radius md, font sm/600
  a11y      real <button>, visible focus, loading keeps the label for screen readers
  used on   S02, S07, S09
```

Every state the recon saw, plus the ones it should have: focus, disabled,
loading, error, empty. Keyboard and screen reader behaviour is part of the
spec.

## Step 4: build the primitives

Build the components in code once, in isolation (a `/design` route or
Storybook), before any screen. Use an accessible base if the stack has one
(Radix, shadcn/ui, React Aria). Screenshot the page. That is the design system
check.

## Output

`tokens.json`, `tokens.css`, the Tailwind config, `components.md`, the
primitives built, and a contrast report with zero AA failures. Next:
`@replica-build`.


## ChatGPT execution contract


Apply these adaptations throughout this workflow:

- Discover available tools. Use web search for public research and current facts, GitHub for repository work, and browser interaction under its access rules. Never invent tools, visits, screenshots, reviews or checks.
- Use Sites building and hosting skills for complete websites when applicable. Preserve existing repository stacks, including native Kotlin or Swift. Verify current API, pricing, store and hosting requirements from official sources; reference defaults and lint limits are starting points.
- Study public pages, screenshots, docs and authorized account views. Write implementation fresh. Exclude proprietary code, private endpoints, target identity and licensed content.
- Resolve `<skill-root>` to this skill's actual directory. Run Python tools with `python3 <skill-root>/<tool>.py` from the project directory. Run `--help` for exact arguments. Tools use the standard library. Templates and tools are in this skill folder; themes.json is beside reviews.py. Copy templates into the project before editing; leave installed resources unchanged.
- Keep project evidence in `replica/`. Save standalone deliverables with the Library skill. Keep repository-backed project files in their repository.
- Preserve source links, collection dates, sample sizes and uncertainty. Follow quotation limits; use short cited excerpts rather than redistributing whole reviews. Never use competitor reviews as testimonials.
- Record features as yes, partial, no or skip with reasons. A partial must-have blocks shipping. Missing screenshots mean no measured layout score. A final shippable verdict also requires verified core flows, feature score 80+, and no open S1/S2 bugs. Scores alone do not establish readiness.
- Use test credentials and payment test mode. Keep secrets out of chat, output and tracked files. Follow the account and credential handling rules of actual tools.
- Complete authorized work without repeated confirmations. Finish a reviewable preflight before asking for any new approval. Publish within existing authorization. Do not send outreach, buy domains or make real purchases without explicit authorization.


For tools belonging to another stage, resolve that named skill independently from the installed skill catalog, or use the sibling folder in this source repository. Do not assume installed skills retain neighboring folder names. If the other skill is unavailable, report that dependency and continue independent work.
