---
name: replica-launch
description: Use when preparing a clone landing page, pricing, app store listing and evidence-based launch plan.
---

# replica-launch

Reads `replica/fixes.md` (the angle and the evidence), `replica/brand.md`,
and `replica/brand.json`. Writes `replica/launch/`: `landing.md`,
`pricing.md`, `listing.json`, `launch-plan.md`.

```bash
python3 <skill-root>/listing.py replica/launch/listing.json      # limits, claims, the original's name
```

Start from `listing.example.json` in this folder.

## The rules

- **No fake proof.** No invented testimonials, user counts, star ratings,
  press logos or "trusted by" rows. An empty proof section is better than a
  fake one. Real beta users, with permission, are fine.
- **No reviewer quotes as testimonials.** The original's reviews are research.
- **The original's name stays out** of your app name, store listing, keywords
  and ads. Apple and Google reject it, and it invites a takedown.

## Step 1: landing page

`landing.md`, section by section, then build it in the project:

1. **Hero**: the angle as a headline (what you do, for whom), one line under
   it, one button. Screenshot of the real product.
2. **The problem**: the top two "hate" themes, in plain words. Paraphrase,
   do not quote reviewers.
3. **How it works**: three steps, from the core flow.
4. **Features**: each tied to a fix from `fixes.md`. Lead with the fixes,
   not the parity features. Parity is the price of entry.
5. **Pricing**: the table from step 2.
6. **FAQ**: the real objections, including "can I import from {{category}}
   tools?" if you built an importer.
7. **Final call to action.**

Copy in the brand voice. Run replica-design's contrast check on the page.

## Step 2: pricing

`pricing.md`:

- The original's public pricing page and 2 or 3 alternatives, in one table,
  with the URL and the date read. Prices change, so the date matters.
- What reviewers said about price and billing, from `feedback.md`, with counts.
- The model: free plan or trial, per seat or flat, monthly and annual
  (annual usually 2 months free).
- Three tiers at most. Name them by who they are for.
- Fix the billing complaints in the product: one-click cancel, clear renewal
  emails, no surprise per-seat jumps.
- The Stripe products and prices to create (the user creates them).

## Step 3: store listing

Fill `listing.json`, then:

```bash
python3 <skill-root>/listing.py replica/launch/listing.json
```

It checks App Store limits (name 30, subtitle 30, promotional text 170,
keywords 100, description 4000) and Google Play's (title 30, short
description 80, full 4000), counts characters the way a person does, flags
ranking and price claims in short fields, emoji, wasted keyword characters,
and **any name from `avoid`** anywhere in the listing. Exit 1 on an error.

Apple's App Review Guideline 4.1 (Copycats) rejects apps that simply copy a
popular app or make minor changes to another app's name or UI. Your fixes
and your own brand are what get you through review, so make them visible in
the screenshots and the first lines of the description.

Also prepare: screenshots at the current required sizes (check App Store
Connect and Play Console when you upload, they change), privacy labels and
the data safety form, privacy policy and support URLs, age rating, and review
notes with a demo account the reviewer can use.

## Step 4: launch plan

`launch-plan.md`: a waitlist or beta list before launch, analytics and error
tracking live, where the original's unhappy users talk (the Reddit threads
and communities from the research), a Product Hunt or Hacker News post that
leads with the fix, and the first 10 users to talk to by hand.

## Output

`replica/launch/` complete, the landing page built, `listing.py` passing.
Next: `@replica-deploy`.


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
