# Replica-Skill-Chatgpt

Eleven separate skills adapted for ChatGPT and Codex from [Jake Schincariol’s Replica](https://github.com/Jakeschincariol/replica-skill). Rebuild app functionality with fresh code, assets and branding.

## Skills

| Skill | Purpose |
| --- | --- |
| `@replica-recon` | rebuilding an app and mapping its screens, flows, components, inferred data model and features from public sources or authorized account views |
| `@replica-architect` | planning a clone from its recon map, choosing a stack, database schema, API routes and build milestones |
| `@replica-design` | rebuilding a clone design system, defining color roles, type, spacing, accessible components and design tokens |
| `@replica-build` | implementing a clone from recon and design specs, building its shell, core flow, screens and all interaction states |
| `@replica-backend` | adding auth, database access rules, payments, email, jobs and official integrations to an app clone |
| `@replica-test` | testing an app clone, checking its user flows, reproducing bugs and writing end-to-end regression tests |
| `@replica-diff` | comparing a clone with its original, checking feature parity, identifying gaps and measuring screenshot layout differences |
| `@replica-entrepreneur` | researching public user reviews to identify complaints, missing features, improvements and positioning for an independent alternative |
| `@replica-brand` | naming and rebranding an app clone with its own identity, palette, logo brief, voice and original-brand remnant checks |
| `@replica-launch` | preparing a clone landing page, pricing, app store listing and evidence-based launch plan |
| `@replica-deploy` | deploying a rebranded clone, checking production readiness, DNS, hosting, environment variables and mobile releases |

## Use

In ChatGPT with Skills support, provide this repository URL and ask to install the eleven `replica-*` skill folders. Availability depends on your ChatGPT environment; this repository is not an OpenAI MCP connector or a Claude plugin.

Then request a skill by name, for example:

> @replica-recon Map this scheduling app’s core booking flow from public documentation.

> @replica-diff Compare my implementation against the feature matrix.

For Codex, copy the eleven `replica-*` folders into your user skill directory, typically `~/.codex/skills/`, without replacing existing folders. In Codex interfaces supporting dollar invocation, use `$replica-recon`. Skills can also be supplied as instructions in a chat, but Python tools require an execution environment.

Run in order for a complete project: recon, architect, design, build, backend, test, diff, entrepreneur, brand, launch, deploy. Each can also run independently when its prerequisites are available. Project evidence lives in `replica/` in your app project.

## Tools

Python 3.8 or newer; standard library only, no API keys and no network calls from these tools. Run from this repository, using your project’s absolute input paths if it lives elsewhere:

```bash
python3 replica-diff/parity.py /path/to/project/replica/features.csv
python3 replica-diff/imgdiff.py original.png clone.png --out diff.png
python3 replica-design/contrast.py /path/to/project/replica/design/tokens.json
python3 replica-entrepreneur/reviews.py /path/to/project/replica/reviews.csv
python3 replica-brand/sweep.py /path/to/project --config /path/to/project/replica/brand.json
python3 replica-launch/listing.py /path/to/project/replica/launch/listing.json
python3 -m unittest discover -s tests -v
```

A partial must-have blocks shipping. Missing screenshots leave visual parity unassessed. A shipping verdict also requires verified core flows and no open S1/S2 bugs. Static tools do not prove runtime readiness.

## ChatGPT adaptations

Each folder has its own SKILL.md and agents/openai.yaml. Templates and tools remain beside their relevant skill, matching the original repository’s split. Each skill includes the ChatGPT execution contract so individual installation retains the guidance. Cross-skill dependencies resolve by skill name rather than assuming neighboring installed folder names.

Use available research, browser and repository tools under their actual access rules. Use Sites skills for complete website work where applicable; preserve existing native or web stacks. Verify current provider and store requirements. Continue within user authorization, keep credentials private, and never invent reviews, checks or scores.

## Scope and license

Study public evidence and authorized views. Rebuild behavior with fresh implementation. Do not copy proprietary source, private APIs, trademarks, logos, licensed content or competitor copy. Reviews are research, not testimonials.

Original work: Copyright (c) 2026 Jake Schincariol, MIT License. Original source revision: `77c9436fb3d18c3d58169efb8caf4fe906b0dc51`. This is an independent ChatGPT adaptation, not an official OpenAI product or a claim of affiliation with the original author. See [LICENSE](LICENSE).
