---
name: replica-backend
description: Use when adding auth, database access rules, payments, email, jobs and official integrations to an app clone.
---

# replica-backend

Reads `replica/architecture.md`. Writes migrations and server code, and keeps
`replica/backend.md` (checklist below) up to date.

## The rules

- **Official, public APIs only, with the user's own keys.** Never call the
  original app's private endpoints, never reuse its OAuth client, never proxy
  through it.
- **The user creates accounts and keys.** ChatGPT never signs up for services,
  never types a password, card or live key. The user creates the Stripe,
  Supabase, Resend or Google Cloud project and puts keys in `.env.local`.
  ChatGPT writes `.env.example` with every variable name and no values.
- **Test mode first.** Stripe test keys and test cards until replica-deploy.

## Auth

- Email sign up with verification, password reset, magic link if the original
  has it. OAuth (Google, Apple) with the user's own developer apps.
- Sessions: http-only secure cookies. Sign out everywhere.
- Roles and teams if the recon map has them: owner, admin, member, with one
  function that answers "can this user do this to this record".
- Account deletion that actually deletes. Apple requires it for apps with
  sign up.

## Database

- Migrations from `architecture.md`, checked in, run by a script.
- Access rules on every table: row level security policies on Supabase, or
  the authorisation function called in every query. Test it: a second user
  must get nothing back.
- Seed script with realistic fake data (no real people).
- Backups on (the host's daily backups count, check they are enabled).

## Payments

- Stripe Checkout for sign up to a plan, the Customer Portal for changes and
  cancelling. Do not build card forms.
- Webhooks: verify the signature, store the event id, make every handler
  idempotent (Stripe retries). Handle `checkout.session.completed`,
  `customer.subscription.updated`, `customer.subscription.deleted`,
  `invoice.payment_failed`.
- Subscription status lives in your database, updated by webhooks, read by
  your app. Never trust the client.
- Cancelling is one click. Hard-to-cancel billing is a top complaint about
  most apps, and in many places it is illegal.

## Email and jobs

- Transactional email through Resend or Postmark from your own domain.
  Templates written fresh.
- Jobs for anything time-based (reminders, digests, sync, cleanup) with
  retries and a dead-letter log. Times in UTC, shown in the user's zone.

## Integrations

For each integration in the feature matrix: the official API, the OAuth
scopes needed (fewest possible), the provider's review process, rate limits.
Google scopes like Calendar need Google's OAuth verification before public
launch, which takes weeks. Start it early and write that in `backend.md`.

## Security checklist

- [ ] secrets only in env vars, `.env*` in `.gitignore`, nothing in client bundles
- [ ] input validated on the server (zod or similar) on every route
- [ ] authorisation checked on every read and write, tested with a second user
- [ ] rate limits on auth, sign up, and anything that sends email or SMS
- [ ] webhooks verify signatures
- [ ] uploads: size and type limits, served from a separate domain or bucket
- [ ] no user data in URLs or logs
- [ ] dependencies audited (`npm audit`)
- [ ] privacy policy lists every processor (Stripe, Resend, host, analytics)

## Output

Working auth, database, payments in test mode, email and the integrations,
`.env.example`, `replica/backend.md` with the checklist ticked, feature
matrix rows updated. Next: `@replica-test`.


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
