# NAVRINE Content OS

AI-native content planning, generation, review, scheduling, distribution, and learning system for NAVRINE and managed brands.

NAVRINE Content OS is built on top of the open-source Postiz codebase and keeps Postiz's mature social-channel infrastructure while replacing the generic scheduler mindset with a NAVRINE-native content operating system.

> Helping brands scale with tech.

## What This Product Is

NAVRINE Content OS is not just a social scheduler.

It is designed around a closed content loop:

`Research → Opportunity → Angle → Plan → Generate → Adapt → Review → Schedule → Publish → Measure → Learn → Iterate`

The system should help NAVRINE and client brands turn expertise, market intelligence, projects, experiments, and business insight into consistent high-quality distribution.

## NAVRINE Context

Read [`NAVRINE_CONTEXT.md`](./NAVRINE_CONTEXT.md) for the canonical brand and editorial context, including:

- NAVRINE positioning
- target audiences
- content pillars
- brand voice
- content quality rules
- platform behavior
- commercial intent
- truthfulness constraints
- operating loop

## NAVRINE Tool Map

Read [`NAVRINE_TOOLS.md`](./NAVRINE_TOOLS.md) for the tool contract and agent behavior.

The existing Postiz-derived runtime provides lower-level capabilities for:

- connected channel discovery
- workspaces/groups
- platform/provider schema validation
- content calendar inspection
- scheduled post settings
- scheduling and publishing
- image generation
- video generation
- media import

NAVRINE adds a higher-level mental model around those capabilities:

- `brandContext`
- `contentResearch`
- `opportunityScore`
- `contentPlan`
- `generateContent`
- `adaptContent`
- `qualityReview`
- `scheduleContent`
- `performanceReview`
- `learningLoop`

## Runtime Agent

The Mastra agent is registered as:

```text
NAVRINE Content OS
id: navrine-content
```

Its runtime instructions live in:

```text
libraries/nestjs-libraries/src/chat/load.tools.service.ts
```

The registered agent key lives in:

```text
libraries/nestjs-libraries/src/chat/mastra.service.ts
```

NAVRINE-specific topic/category taxonomies live in:

```text
libraries/nestjs-libraries/src/agent/agent.categories.ts
libraries/nestjs-libraries/src/agent/agent.topics.ts
```

## Default Autonomy

NAVRINE Content OS uses **approval-first publishing** by default.

The agent may autonomously:

- research
- generate opportunities
- prepare briefs
- draft content
- adapt platform variants
- score and revise drafts
- propose a calendar

Publishing should require confirmation unless a workspace has an explicit automation policy that defines allowed channels, formats, time windows, quality thresholds, and prohibited topics.

## Content Pillars

1. AI Infrastructure
2. Engineering
3. Data Operations
4. Brand & Design
5. Founder Systems
6. Build in Public / Case Studies
7. Market Intelligence

## Core Stack

Inherited from Postiz:

- pnpm workspaces / monorepo
- Next.js / React frontend
- NestJS backend
- Prisma + PostgreSQL
- Redis
- Temporal orchestration
- Mastra agent runtime
- LangChain / LangGraph content-generation flows
- multi-platform social publishing infrastructure

The repository requires Node.js `>=22.12.0 <23.0.0` and pnpm `10.6.1` according to the current package configuration.

## Environment

Start from:

```bash
cp .env.example .env
```

At minimum, configure the required database, Redis, JWT, frontend/backend URLs, storage, AI provider keys, and the OAuth credentials for social platforms you intend to connect.

The existing `.env.example` documents the supported variables.

## Development

Install dependencies:

```bash
pnpm install
```

Run development services:

```bash
pnpm dev
```

Useful commands include:

```bash
pnpm dev-backend
pnpm build
pnpm build:frontend
pnpm build:backend
pnpm build:orchestrator
pnpm prisma-db-push
```

For local infrastructure, see the included Docker Compose configuration.

## Product Direction

The next NAVRINE-specific product layers should be built around:

- Content Command Center
- Brand Brain / workspace context
- Content Pillars and campaigns
- Research Radar
- Opportunity / Idea Bank
- weekly and monthly Content Planner
- AI Content Studio
- platform-native repurposing
- approval queue
- publishing calendar
- analytics and content-learning loop

The distribution infrastructure is already present. NAVRINE's differentiated value should come from strategy, intelligence, brand memory, editorial quality, and continuous learning.

## Upstream & Attribution

This repository is derived from **Postiz** (`gitroomhq/postiz-app`). Postiz provides the underlying open-source social-media scheduling and publishing infrastructure.

Upstream project:

```text
https://github.com/gitroomhq/postiz-app
```

Do not remove upstream copyright/license notices where required.

## License

The inherited codebase is licensed under **AGPL-3.0**. See [`LICENSE`](./LICENSE).

Before using this repository as a proprietary or hosted commercial product, review the AGPL obligations applicable to your deployment and modifications.
