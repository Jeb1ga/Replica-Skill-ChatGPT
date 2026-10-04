---
name: replica-entrepreneur
description: Use when researching public user reviews to identify complaints, missing features, improvements and positioning for an independent alternative.
---

# replica-entrepreneur

A straight copy of an app has no reason to exist. This skill finds the reason:
what the original's users hate, in their own words, and fixes it in yours.

Bundled tool in this skill folder:

```bash
python3 <skill-root>/reviews.py replica/reviews.csv --out replica/feedback.md
```

## The rules, which are not negotiable

- **Never fabricate.** No invented reviews, quotes, ratings, counts, users or
  sources. If a source cannot be reached, say so and move on. If there are 14
  reviews, say 14.
- **Every quote is verbatim and linked.** Copied exactly from the page, with
  the URL of the review or thread. `reviews.py` drops any row without a link.
- **Reading, not scraping.** Read review pages the way a person does, in the
  browser, and copy rows into the sheet. No scraping libraries against stores
  or review sites whose terms forbid it. Official public feeds and APIs are
  fine within their terms: Apple's customer reviews RSS feed
  (`https://itunes.apple.com/us/rss/customerreviews/id=<APP_ID>/sortBy=mostRecent/json`),
  the Hacker News Algolia API (`hn.algolia.com/api/v1/search?query=...`),
  Reddit's official API under its terms.
- **No fake reviews, ever.** Not for your app, not against theirs. It is
  illegal in the US (the FTC's 2024 rule) and in many other places.
- **Reviewers are not your testimonials.** Their words are research. Do not
  put them on your landing page.

## Step 1: collect

Aim for 100+ reviews across at least three sources, recent first:

| source | where |
| --- | --- |
| App Store | the app page, Ratings and Reviews, See All; or the RSS feed above |
| Google Play | the listing, See all reviews, sort by newest |
| G2, Capterra, Trustpilot | the product's review pages, filter to 1 to 3 stars too |
| Reddit | search "X alternative", "switched from X", "X sucks", "X vs" |
| Hacker News | the Algolia API or site search, same queries |
| the original's own board | its public roadmap or feature-request board (Canny and similar) and the vote counts |
| its changelog | what it shipped, so you do not "fix" what is already fixed |

Each row in `replica/reviews.csv`: `source,url,date,rating,text`, text copied
exactly. Read the 3 and 4 star reviews too. "Love it, but..." is where the
best fixes hide.

## Step 2: rank

```bash
python3 <skill-root>/reviews.py replica/reviews.csv --out replica/feedback.md
```

It sorts reviews into themes (`themes.json`, edit it for the app's category),
weights low ratings and recent reviews higher, marks themes with fewer than 3
reviews or only one source as thin, lists every request in the users' own
words, and surfaces low ratings that matched no theme. Read that last list by
hand. It is often the best part.

## Step 3: three lists

From `feedback.md`, write three ranked lists. Each item: the problem in one
line, how many reviews, how many sources, one or two linked quotes.

1. **What they hate.** Complaints about things the app does.
2. **What is missing.** Features people ask for by name.
3. **What is unsolved.** Whole jobs or groups the app ignores ("not built for
   teams", "useless for therapists"). These become positioning.

Thin themes are listed as thin. Do not present three angry Reddit comments as
a trend.

## Step 4: the fix plan

Pick the top 5 to 8 by evidence times how cheaply you can fix them. For each:
what to build or change, size (S, M, L), which skill does it, and the
evidence. Add each one to `replica/features.csv` as a row with `original` set
to `no`. Pricing and billing complaints go to `@replica-launch`.

## Step 5: the angle

Three positioning options, each grounded in a top theme:

```
For {{who}} who {{hate this about the original, in plain words}},
{{your app}} {{does this instead}}.
Evidence: {{theme}}, {{n}} reviews across {{n}} sources.
```

Recommend one. It drives replica-brand's name and voice and replica-launch's
hero. Do not put the original's name in your app name, ads or store listing.
A factual comparison page is a legal question for a lawyer in your country.

## Output

`replica/reviews.csv`, `replica/feedback.md`, `replica/fixes.md` (three
lists, fix plan, angle), new rows in `features.csv`, and a summary that
states the sample size. Next: `@replica-brand`.


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
