---
name: replica-brand
description: Use when naming and rebranding an app clone with its own identity, palette, logo brief, voice and original-brand remnant checks.
---

# replica-brand

Nothing launches under the original's identity. This skill is the line
between "a clone" and "your app".

Bundled tool in this skill folder:

```bash
python3 <skill-root>/sweep.py . --avoid "Original Name,Its Company" --domains original.com --colors "#006bff"
python3 <skill-root>/sweep.py . --config replica/brand.json        # same, from the brand file
```

Writes `replica/brand.md` and `replica/brand.json` (`avoid`, `domains`,
`colors`, used by `sweep.py`, `listing.py` and replica-deploy).

## Step 1: the name

Read the angle from `replica/fixes.md`. Generate 20 candidates across styles:
descriptive (Booklink), compound (Slotwise), invented (Calvo), metaphor
(Harbor), verb (Book). Then cut to 5 with these filters:

- **Not confusingly similar to the original** in sound, look or meaning, and
  not to any other app in the same category. That is the test trademark
  offices use, so it is the test here. No puns on their name, no "-ly" twin.
- Short, spellable after hearing it once, no awkward meaning in big languages.
- Says something about the angle, or at least does not fight it.

## Step 2: the checks, run, not assumed

For each of the 5, a row per check. Mark each **to run**, or the result with
the date it was run. Never write "available" for a check nobody ran.

| check | where |
| --- | --- |
| US trademark | tmsearch.uspto.gov, the app's class (usually 9 and 42) |
| EU trademark | euipo.europa.eu eSearch, or TMview for many offices |
| Canada | ised-isde.canada.ca trademarks database |
| global | WIPO Global Brand Database |
| domain | `whois name.com`, or the registrar's search |
| App Store and Play | search the exact name |
| handles | X, Instagram, TikTok, GitHub |
| the web | search "name + category" |

These are screening checks, not legal clearance. Before spending money on
the name, a trademark lawyer should do a proper search.

## Step 3: palette

A new palette, written into the same token roles replica-design set up.
Pick a primary brand hue from a different family than the original's (if
theirs is blue, yours is not a nearby blue). Then:

```bash
python3 <replica-design-root>/contrast.py replica/design/tokens.json
```

Zero AA failures. Add the original's brand colours to `brand.json` so the
sweep catches any that survive.

## Step 4: logo brief

Not a logo, a brief for whoever makes it (the user, a designer, an image
model):

- the idea in one line, tied to the name and angle
- mark type: wordmark, symbol plus wordmark, or monogram
- must work at 16px (favicon) and as a 1024px app icon
- deliverables: SVG, app icon 1024x1024 with no transparency for iOS,
  favicon set, social image 1200x630
- **must not resemble the original's mark**: no shared shape, colour pair or
  letterform trick. Put the original's logo next to the drafts and check.

## Step 5: voice

Three words for how it sounds, with what each does not mean ("direct, not
blunt"). Five do and don't pairs. Then rewrite the 10 most-seen strings in
the clone (sign up, empty states, the main button, the confirmation, the
error) in that voice. All fresh, none echoing the original's phrasing.

## Step 6: the sweep

Replace every placeholder name, colour and string. Then:

```bash
python3 <skill-root>/sweep.py . --config replica/brand.json
```

It searches file contents and file names for the original's name (also inside
identifiers like `CalendlyEmbed`), domains and colours, skipping
`node_modules`, build output and the `replica/` planning folder. Exit 1 means
something is left. Fix until it says clean. Also check by eye: the favicon,
the page titles, the email templates, the OG image, the app icon.

## Output

`replica/brand.md` (name with checks, palette, logo brief, voice),
`replica/brand.json`, updated tokens, rewritten strings, and a clean sweep.
Next: `@replica-launch`.


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
