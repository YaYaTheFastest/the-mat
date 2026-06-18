# The Mat & The Forge

**A personal, AI-augmented operating system for high-agency living.**

- **The Mat**: A high-quality Brazilian Jiu-Jitsu technique library.
- **The Forge**: The broader system for equipment, fitness, ranch operations, deliberate practice, and cross-domain intelligence.

Everything is powered by a single Obsidian vault as the source of truth, with Grok/Hermes doing the heavy intellectual and synthesis work, surfaced through a clean, fast web/PWA experience.

## Philosophy & Design Principles

- **The vault is the single source of truth.** All authoritative data lives in Obsidian ("Jorgenson Brain").
- **The user manages almost nothing.** No servers, no file wrangling, no copy-paste loops. Grok and automation handle the complexity.
- **Highest quality by default.** When something enters the system, it should already meet a high standard (structured, actionable, well-referenced, continuously improvable).
- **AI as a true co-pilot.** Hermes (powered by xAI Grok) is used for research, card upgrades, standardization, health synthesis, and explicit cross-domain transfer (e.g. fitness signals → BJJ performance).
- **Frictionless loops.** iOS Shortcuts, one-tap Hermes tasks, deep links, and direct vault edits are preferred over manual processes.
- **Cross-device presence.** Beautiful, usable experience on phone, iPad, and desktop. The app should "just work."

## Core Components

### The Mat (BJJ Techniques)

A curated library of real BJJ techniques (~120 cards after strict filtering).

- Heavy emphasis on Gracie Barra GB1 curriculum (W01–W09+ populated).
- Personal captures from video, instructors, and live training.
- Strict server-side filtering: only genuine technique content from the BJJ section of the vault (meta files, equipment notes, non-BJJ domains, etc. are excluded).

**Card Standard (2026 GB1 format):**

- Frontmatter: `name`, `position` (closed-guard, open-guard, half-guard, etc.), `category`, `gb_curriculum`, `principle_tags` (5 sharp principles), `videos` (with `why` explanations), `confidence`, `related_techniques`, `card_layout_version: "2026-05"`.
- Body structure:
  - ## Observe
  - ## Learn / Key Principles (5 Sharp Principles + Common Mistakes)
  - ## Where It Leads (Positional Flows + Long-term BJJ Development)
  - ## Execute (numbered steps + Key Cue + Drills)
  - Media references + placeholders
  - ## Personal Cues & Notes (preserved verbatim)

UI features include clear guard-type visibility (position badges), quality/completeness filters (GB1, High Quality, Has Notes, Has Video), and direct Hermes polishing.

### The Forge (Operational System)

Structured support for real-world deliberate practice and operations:

- **Equipment & Maintenance**: Detailed ranch/shop cards with hours tracking, maintenance schedules, service history, and Daily Wins integration.
- **Fitness Domain**: Physiology metrics (HRV, resting HR, readiness), protocols (StrongFirst, AGT, mobility flows), principles (breathwork, tension), and health export syntheses with explicit BJJ performance transfer notes.
- **Cross-Domain Intelligence**: Health and training data is synthesized into actionable BJJ insights (e.g., "High readiness + good REM → prioritize heavy pressure guard retention").

### Hermes (Grok-Powered Intelligence Layer)

- Creates structured review tasks directly in the vault (`00 Meta/Hermes Tasks`).
- One-tap handoff via iOS Shortcuts deep links (content is pre-populated).
- Used for:
  - Upgrading technique cards to the 2026 standard.
  - Standardizing equipment cards.
  - Generating health/fitness syntheses with BJJ transfer.
  - General research and synthesis tasks.

## Architecture & Data Flow

```
Mac (Master Vault)
  └─ Obsidian (Jorgenson Brain)
       └─ 20 Knowledge Base/BJJ/Captures
       └─ 00 Meta/Systems/Domains/Fitness
       └─ Equipment cards, etc.
       └─ 00 Meta/Hermes Tasks

↓ rsync (via script)

DigitalOcean Droplet
  └─ /opt/vault (rsynced copy)
  └─ Next.js app (PM2)
       └─ Reads vault at runtime
       └─ Serves The Mat + Forge UI

GitHub (Code)
  └─ Source + this README

iOS Shortcuts
  └─ Zero-friction bridge to Hermes
```

- **Master data** lives only on the Mac.
- **App** is a thin, fast presentation + interaction layer.
- **No user-managed servers** in daily use.
- Sync is one-command (see `scripts/sync-vault-to-droplet.sh`).

## Tech Stack

- **App**: Next.js 16 (App Router, Turbopack), TypeScript, Tailwind.
- **Data**: gray-matter + custom vault loaders (`lib/vault.ts`).
- **AI**: xAI Grok via custom Hermes system + API routes.
- **Automation**: iOS Shortcuts + deep links.
- **Deployment**: DigitalOcean droplet + PM2.
- **Sync**: rsync (vault) + git (code).
- **Vault**: Obsidian (primary authoring + review environment).

## Current State (Mid-2026)

- Real BJJ technique library: ~120 cards after rigorous filtering.
- Significant GB1 curriculum coverage (W01 through W09 populated).
- Many cards upgraded to consistent high-quality 2026 format.
- Guard type (position) information is now clearly surfaced in the UI.
- Quality filters allow slicing "all real BJJ cards" by completeness and curriculum status.
- Health export pipeline delivering recent data (June 2026 exports present in vault).
- Hermes polish workflow available per-card.
- Direct vault editing used for bulk content upgrades (Grok writes improved cards straight to the master vault).
- Frictionless sync script in place.

## Forge Domains & Bubbles Homepage (New)

The Forge homepage at `/forge` now features beautiful, large clickable orb-style bubbles (circular cards with hover scale and glow effects using Framer Motion).

Domains:
- **The Mat** (BJJ techniques)
- **Fitness & Recovery**
- **Equipment & Ranch**
- **Cross-Domain Insights**

The config is extensible. A prominent "+ New Domain" bubble opens the floating Hermes chat pre-filled with a creation prompt. Hermes will search the vault, standardize to high-quality template, and write structured content back.

Clicking a bubble goes to `/domains/[slug]`, which loads relevant vault content (techniques for Mat, fitness data, equipment, etc.), with search, and one-tap Hermes polish buttons that trigger automatic standardization and vault writes.

The floating Hermes chat is now fully context-aware for domains: it detects the current slug from URL and can create or polish entire domains by searching the vault, categorizing, applying the 2026-style format, and writing files directly.

This fulfills the goal of extensible domain hubs with zero-friction AI assistance.

## Strategic Questions for Grok Review

This README is written as a briefing document. When thinking about future directions, please consider the following:

### Content & Quality
- How do we finish bringing the entire technique library (and future captures) to the highest standard with minimal ongoing user effort?
- What is the right balance between "direct Grok edits to vault files" vs. Hermes task + user paste workflows?
- Should there be a formal "promotion" or quality gate process, or should everything that reaches the user already be polished?

### AI & Automation Leverage
- How can we get even more leverage from Grok/Hermes across the vault (synthesis, pattern detection, proactive suggestions)?
- Opportunities for deeper cross-domain intelligence (fitness → BJJ, equipment maintenance discipline → training consistency, etc.)?
- Long-term role of the per-card Hermes button vs. bulk/automated processing.

### Architecture & Operations
- Is the current Mac → rsync → DigitalOcean model the right long-term shape, or are there better low-maintenance alternatives?
- How should we think about versioning, backups, and multi-device consistency for the vault?
- What would it take to support isolated instances for family members in the future?

### Product & Experience
- What features would deliver the highest leverage for deliberate practice (curriculum progress, routines generator, mind maps integration, streak/retention analytics, etc.)?
- How should the UI evolve to make guard types, principles, and personal notes even more immediately useful?
- Opportunities to reduce any remaining friction in the daily workflow?

### Growth & Scope
- How far should "The Forge" extend beyond BJJ + ranch ops?
- What metrics or feedback loops would be most valuable to surface?
- How do we keep the system feeling lightweight and high-agency rather than becoming another thing to manage?

## How to Work With This Project (for Grok)

1. The Obsidian vault is authoritative for content.
2. This GitHub repo is for code and high-level documentation (like this README).
3. When making recommendations, distinguish between:
   - Changes to the Next.js app code
   - Direct improvements to vault files (cards, syntheses)
   - New automation / Hermes task templates
   - Deployment or sync process changes
4. Prefer solutions that reduce user management overhead.

## Quick Links (Development)

- Local source: `Projects/the-mat`
- Vault master: Obsidian (Jorgenson Brain)
- Production: DigitalOcean droplet
- Sync helper: `scripts/sync-vault-to-droplet.sh`

---

*This README exists primarily so Grok can review the system holistically and help chart the next phase of development.*