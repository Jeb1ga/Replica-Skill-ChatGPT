---
name: replica-recon
description: Use when rebuilding an app and mapping its screens, flows, components, inferred data model and features from public sources or authorized account views.
---

# replica-recon

Everything else in the pack builds from what this skill writes. A bad recon
map means a bad clone, so take the time here.

Output goes in the user's project:

```
replica/recon.md        the recon map (template: recon-map.md in this folder)
replica/features.csv    the feature matrix (template: features.csv in this folder)
replica/screens/        reference screenshots of the original. Never shipped.
```

## The rules, before anything else

This skill rebuilds **functionality and UX patterns**, clean-room style. It
studies what the app does and how a user moves through it. It does not take
anything the app owns.

- **Public sources and the user's own account only.** Never log into an
  account that is not the user's, never ask for a password, never get past a
  paywall or a login by any trick.
- **Reading, not scraping.** No crawlers, no bulk downloads, no loops. If a
  browser tool is connected to the user's own browser, read pages at human
  speed with the user present.
- **No source code, no private APIs.** Do not read or save the app's
  JavaScript bundles, decompile its binary, or log its network calls to copy
  endpoints. Public API docs are fine to read.
- **Check the terms.** Some products' terms forbid using an account to build a
  competing product. If the user's account is under terms like that, say so
  and work from public sources only.
- **Screenshots are reference.** They live in `replica/screens/`, are used to
  compare layouts, and never go into the clone.

## Step 1: scope

Use supplied context for these three scope choices. Ask only for missing information that changes the result; otherwise state reasonable assumptions and proceed:

1. **Which app, which platform.** Web, iOS, Android, desktop.
2. **Which slice.** "All of Notion" is not a project. "Notion's pages, blocks
   and sharing" is. Default to the core loop: the one flow users pay for.
3. **Who it is for.** The user's own business, a niche, a product to sell.

## Step 2: list the sources

Build a sources table first, with a URL on every row. In order of value:

| source | what it gives you |
| --- | --- |
| help center / docs | the most complete feature list there is, and the settings |
| pricing page | which features matter (they gate them) |
| changelog | what was added recently, what the team thinks is important |
| app store listing | screenshots of every key screen, the pitch, ratings |
| public walkthrough videos | real flows, click by click |
| marketing site | positioning, the core loop in their words |
| the user's own account | the real thing, every state, driven by the user |
| public API docs | the data model, almost for free |

## Step 3: screen inventory

One row per screen. IDs are stable: S01, S02... Every other file refers to them.

`ID | screen | route or how you get there | purpose | key components | states seen`

States matter: empty, loading, filled, error, permission denied, mobile. An
empty state you did not record is an empty state you will not build.

## Step 4: user flows

F01, F02... Each one is a goal and the screens it passes through:

```
F01 Guest books a meeting
    S07 booking page -> S08 pick a time -> S09 details form -> S10 confirmed
    edge: no slots this week, time zone differs, slot taken while filling the form
```

Count the clicks on the happy path. It becomes the number to beat.

## Step 5: components

Every repeated UI part: buttons, inputs, date pickers, modals, tables, toasts,
nav. Name, variants, states, which screens use it. This becomes
replica-design's component list.

## Step 6: inferred data model

Entities, fields and relationships, each with its evidence and a confidence:

```
Booking  id, event_type_id, start_at, end_at, guest_name, guest_email,
         status (confirmed | cancelled | rescheduled), answers (json)
         evidence: S09 form fields, S10 confirmation, help article "Cancel a booking"
         confidence: high
```

Mark guesses as guesses. replica-architect turns this into a real schema.

## Step 7: feature matrix

Write `replica/features.csv` (columns: feature, area, priority, original,
clone, notes). Priority is must / should / could. `clone` starts at `no` for
every row and gets filled in during the build. replica-diff scores it.

## Step 8: what cannot be cloned

List it honestly, as `skip` rows with a reason: licensed content (a music
catalogue, a stock library), the network and its users, data the app owns,
partner deals, hardware, regulated licences (banking, health). "Clone any
app" means the features and the flow, not what the app owns.

## Step 9: size it

Screens, flows, entities, and the hard parts (realtime, sync, payments,
calendar or email integrations, offline). Give a size: S (a weekend), M (a
few weeks), L (a quarter), XL (rescope it). No promises of a perfect clone.

## Output

`replica/recon.md` and `replica/features.csv`, then a five-line summary: the
core loop, screen and flow counts, the three hardest parts, what is out of
scope, and the next step: `@replica-architect`.


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
