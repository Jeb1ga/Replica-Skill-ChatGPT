---
name: replica-backend
description: >-
  Builds the backend of an app clone: auth, database migrations and access
  rules, payments with Stripe, email, background jobs and third-party
  integrations through official APIs only, plus a security checklist. Use when
  the user says "add login", "set up auth", "wire up the database", "add
  payments", "connect Stripe", "add Google Calendar", "send emails",
  "backend for my clone", or when @replica-build is running on fake data.
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

## ChatGPT compatibility

Use available tools under their actual access and credential rules. Research public information with web search; interact with accounts only when authorized. Never invent reviews, screenshots, test results or parity scores. Follow quotation limits. Verify current provider, store and hosting requirements. Preserve the user's existing stack; use Sites skills for complete websites when applicable.

Resolve `<skill-root>` to this skill's installed folder. Resolve another named skill independently through the skill catalog; do not assume installed folders stay adjacent. Run tools with Python from the app project directory. Templates remain beside SKILL.md; copy them into the project before customizing. Keep repository work in its repository; use Library for standalone deliverables when available.

A partial must-have blocks shipping. Without screenshots, mark layout unassessed. Tool scores alone do not establish readiness. Complete authorized work without repeated confirmations; prepare preflight before requesting any new production authorization. Real purchases and outreach require explicit permission.

Adapted from Jake Schincariol's [Replica](https://github.com/Jakeschincariol/replica-skill), MIT licensed. Retain the included LICENSE.
