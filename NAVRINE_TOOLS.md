# NAVRINE Content OS — Tool Map

This file defines how the AI layer should think about and use the existing Postiz-derived capabilities inside NAVRINE Content OS.

## Tooling Principles

1. **Research before claims.** Current facts, trends, platforms, products, or market movements should be researched before publication.
2. **Plan before publishing.** A campaign should have an audience, objective, angle, platform, and success criterion.
3. **Adapt per platform.** Do not blindly duplicate the same content everywhere.
4. **Require confirmation before scheduling/publishing** unless an explicitly configured automation policy says otherwise.
5. **Never invent evidence.** Analytics, client outcomes, citations, quotes, and performance numbers must come from real data.
6. **Use tools to execute, not to decorate.** Every tool call should advance research, creation, validation, distribution, or measurement.

## Existing Runtime Tools

The Postiz base currently exposes these tool classes through `libraries/nestjs-libraries/src/chat/tools/tool.list.ts`.

### `integrationListTool`
NAVRINE meaning: **List Channels**

Use for:
- discovering connected social accounts
- selecting eligible distribution channels
- verifying account/platform identity before scheduling

Do not call them “integrations” in user-facing language. Say “channels” or “accounts”.

### `groupListTool`
NAVRINE meaning: **List Brands / Workspaces / Clients**

Use for:
- selecting which brand, business, workspace, or client a campaign belongs to
- scoping channels and content to the correct entity

### `integrationSchemaTool`
NAVRINE meaning: **Get Platform Rules**

Use before scheduling to:
- retrieve required provider settings
- validate supported post formats
- understand platform-specific restrictions

This tool is mandatory before a publish/schedule action when provider rules are not already known from the latest context.

### `integrationTriggerTool`
NAVRINE meaning: **Publish / Trigger Channel Action**

Use only after content and destination are validated.

### `integrationSchedulePostTool`
NAVRINE meaning: **Schedule Content**

Use for:
- immediate publishing
- future scheduling
- multi-channel campaign distribution

Before execution, confirm:
- final copy
- media
- date/time/timezone
- platform/channel
- brand/workspace
- any provider-specific settings

### `postsListTool`
NAVRINE meaning: **Inspect Content Calendar**

Use for:
- upcoming posts
- campaign review
- detecting schedule gaps
- avoiding duplicate themes
- finding an existing scheduled/draft post before updating settings

### `postSettingsTool`
NAVRINE meaning: **Update Platform Delivery Settings**

Use for:
- modifying provider-specific settings of existing draft/scheduled content

It is not a general content editor. Do not imply that it rewrites the post body unless the underlying capability actually supports that.

### `generateImageTool`
NAVRINE meaning: **Generate Visual Asset**

Use for:
- editorial illustrations
- carousel visuals
- campaign concepts
- social images

Visual direction should follow NAVRINE’s premium, modern, design-forward taste and avoid generic AI-looking output.

### `generateVideoOptionsTool`
NAVRINE meaning: **Inspect Video Generation Options**

Use before choosing a video generation path.

### `videoFunctionTool`
NAVRINE meaning: **Video Utility / Transformation**

Use when the selected video workflow requires a specific function or transformation.

### `generateVideoTool`
NAVRINE meaning: **Generate Video Asset**

Use for short-form concepts, explainers, visual storytelling, and campaign content when generation quality is appropriate.

### `uploadFromUrlTool`
NAVRINE meaning: **Import External Asset**

Use for:
- bringing an approved external asset into the media system
- repurposing existing NAVRINE-owned media

Validate ownership/usage rights before publishing external assets.

## NAVRINE Logical Tools

These are product-level tools that should be represented in the agent behavior even when implemented as orchestration around existing lower-level tools.

### 1. `brandContext`
Purpose: load the brand’s positioning, audience, offers, voice, proof, constraints, and active priorities.

Default source for NAVRINE itself: `NAVRINE_CONTEXT.md`.

Output should include:
- brand summary
- target audience
- content pillars
- tone
- commercial objectives
- forbidden claims / risk constraints

### 2. `contentResearch`
Purpose: collect fresh evidence and ideas before writing.

Research targets:
- market shifts
- recent news
- product/platform changes
- audience pain points
- competitor narratives
- recurring questions
- emerging keywords/topics

Expected output:
- facts with source references
- observations
- inferred opportunities clearly marked as inference
- stale/uncertain claims flagged

### 3. `opportunityScore`
Purpose: rank ideas before spending production effort.

Suggested scoring dimensions (0–5 each):
- audience relevance
- novelty/timeliness
- NAVRINE authority / right-to-win
- proof availability
- shareability
- commercial alignment
- evergreen value
- production effort (reverse scored)

Return a total score and concise rationale.

### 4. `contentPlan`
Purpose: turn opportunities into a weekly/monthly content system.

Each planned item should have:
- working title
- core thesis
- audience
- funnel objective
- pillar
- platform
- format
- source/evidence requirement
- CTA
- publish date/time
- repurposing path
- success metric

### 5. `generateContent`
Purpose: draft content from an approved brief.

Generate:
- hook
- body/script
- CTA
- optional visual brief
- optional title/thumbnail ideas

Do not create unsupported facts.

### 6. `adaptContent`
Purpose: convert a source asset into platform-native derivatives.

Examples:
- article → LinkedIn post
- article → X thread
- case study → Instagram carousel
- long-form video → Shorts/Reels/TikTok scripts
- technical build notes → founder/operator post

The derivative should preserve the idea, not the exact wording.

### 7. `qualityReview`
Purpose: act as the editorial gate before approval.

Score 0–100 using:
- usefulness
- specificity
- credibility
- clarity
- platform fit
- distinctiveness
- brand fit
- commercial fit

Auto-revise weak content before presenting it when problems are obvious.

### 8. `scheduleContent`
Purpose: map approved content to actual Postiz scheduling tools.

Pipeline:
`qualityReview → platform rules → user confirmation → schedule/publish`

### 9. `performanceReview`
Purpose: interpret real content performance and extract lessons.

Analyze, where data exists:
- impressions/reach
- watch time/retention
- saves
- shares
- comments
- clicks
- qualified leads
- conversion proxies

Do not optimize for vanity metrics alone.

### 10. `learningLoop`
Purpose: convert performance into updated strategy.

Output:
- what worked
- what failed
- likely reason
- evidence confidence
- topics/formats to increase
- topics/formats to reduce
- tests for the next cycle

## Default Agent Workflow

For “make content about X”:

`brandContext → contentResearch → opportunityScore → generateContent → adaptContent → qualityReview`

For “plan next week/month”:

`brandContext → inspect calendar → contentResearch → opportunityScore → contentPlan → qualityReview`

For “publish/schedule this”:

`qualityReview → list channels → get platform rules → confirm → scheduleContent`

For “what should we do next?”:

`inspect calendar + performanceReview + contentResearch → learningLoop → contentPlan`

## Autonomous Mode Policy

Default mode is **approval-first**.

The agent may autonomously:
- research
- generate ideas
- create briefs
- draft content
- adapt variants
- score/revise drafts
- propose schedules

The agent should not autonomously publish unless a workspace has an explicit auto-publish policy covering:
- allowed channels
- allowed formats
- allowed time windows
- review threshold
- prohibited topics
- commercial/legal constraints

This keeps NAVRINE fast without sacrificing brand quality or trust.
