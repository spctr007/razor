# Conway's Law — Page Design Spec

**Date:** 2026-03-23
**Page:** `conways-law.html`
**Model number:** 04
**Angle:** The Inverse Conway Maneuver (Lever First)

---

## Overview

A standalone educational HTML page on Conway's Law, consistent with the existing razor collection. The primary frame is the **Inverse Conway Maneuver**: Conway's Law is not just a warning but a design lever — deliberately shape your team structure to produce the architecture you want. The AI application angle focuses on how AI coding assistants amplify existing org patterns, making team alignment a prerequisite before deploying AI at scale.

---

## Hero

**Incident hook:**
> "The microservices migration succeeded. 18 months later, they counted: 23 services, 23 teams. Every cross-team API call required a ticket. The architecture was technically correct. It just perfectly replicated every dysfunction in the org."

**Eyebrow:** Mental Model 04 · Software Engineering with AI
**Title:** Conway's / *Law*
**Subtitle:** Your system architecture will mirror your team structure whether you plan it or not. The Inverse Conway Maneuver turns that from a warning into a weapon.

**Nav pills:** What it is · 5 Principles · The Maneuver · Anti-Patterns · Case Study · Quiz · Cheatsheet

---

## Section 01 — Foundation (`#what`)

**Title:** What is Conway's Law?

**Body:** Conway's Law is Melvin Conway's 1967 observation: *"Organizations which design systems are constrained to produce designs which are copies of the communication structures of those organizations."* In practice: your module boundaries follow your team boundaries. Your API contracts follow your reporting lines. Your monolith's internal coupling follows who sits next to whom.

The Inverse Conway Maneuver flips this from a liability into a strategy: **design your team structure first to produce the architecture you want**, then let Conway's Law do its work.

**Definition block quote:**
> "Organizations which design systems are constrained to produce designs which are copies of the communication structures of those organizations."
> — Melvin Conway, 1967

---

## Section 02 — Core Framework (`#principles`)

**Title:** 5 Principles of the Law

5 expandable cards, each with a Software Example block and an AI Application block.

### Principle 01 — Your Architecture Is a Portrait of Your Org
*The system you have is the system your communication structure produced.*

Conway's Law is not a metaphor — it's a force. Teams that communicate freely produce tightly coupled modules. Teams that communicate through tickets produce hard API boundaries. Teams that don't communicate produce parallel reimplementations. You cannot fight this by drawing a better architecture diagram. You fight it by changing how people work together.

- **Software Example:** A checkout service with tangled payments and fulfillment logic — not because the domains are related, but because those two teams share a sprint.
- **AI Application:** Before assuming the AI-suggested architecture is correct, ask: does the proposed service boundary match who will own it? If not, the architecture won't survive contact with the org.

### Principle 02 — Seams Follow Ownership, Not Logic
*Module boundaries emerge from who owns what, not from what makes logical sense.*

When a domain spans two teams, the split happens at the handoff — not at the cleanest abstraction. The result is interfaces that are wide, fragile, and over-specified because each side is defending its territory. Ownership ambiguity is the root cause of most architectural debt.

- **Software Example:** A notifications service that half-lives in the payments team's repo and half in the platform team's repo — because it was built collaboratively and nobody claimed it. The interface is a mess of legacy fields because both teams are scared to break the other.
- **AI Application:** "Before proposing a service split, identify which team will own each resulting service end-to-end. If ownership is ambiguous, flag that before proposing architecture."

### Principle 03 — The Inverse Conway Maneuver
*Design your teams to produce the architecture you want.*

If you want a clean service boundary between payments and notifications, create a team that owns payments end-to-end and a team that owns notifications end-to-end — before writing the services. The architecture will follow. This is the premise behind Team Topologies, Amazon's two-pizza teams, and most successful platform splits.

- **Software Example:** Spotify's squad model was not a cultural experiment — it was an architectural decision. The architecture they wanted (independent, deployable services per domain) required independent, autonomous teams per domain. Team structure first; architecture followed.
- **AI Application:** "We are restructuring around these domain teams: [list]. For each proposed service or module, assign it to exactly one team. Flag anything that would require two teams to co-own."

### Principle 04 — AI Accelerates the Existing Pattern
*AI tools crystallize your current org structure into code faster than ever.*

When an engineer uses an AI coding assistant, the code it generates naturally follows the context it's given: the files the engineer owns, the APIs they call, the conventions their team uses. AI doesn't see org charts — but it amplifies whoever holds the keyboard. If your teams are siloed, AI-assisted development will build those silos into the architecture at 10x speed, before anyone notices.

- **Software Example:** Three platform teams each adopt an AI assistant. Six months later, each team has built its own internal observability library — all slightly different, none compatible. The AI wasn't wrong; it was working from the context each team provided. The duplication was already there, latent in the org. AI made it structural.
- **AI Application:** Before rolling out AI assistants org-wide, audit your team ownership model. Misaligned teams + AI acceleration = architectural debt at machine speed.

### Principle 05 — Team Interfaces Are API Contracts
*How your teams communicate IS your interface design.*

Every sync meeting that shouldn't exist is a tight coupling. Every Slack DM for a "quick question" is an undocumented API call. Every team that can deploy independently is a service with a clean interface. Designing your system architecture and designing your team interactions are the same problem — the Inverse Conway Maneuver is where they converge.

- **Software Example:** A team that can deploy on Friday afternoon without notifying anyone has a clean interface. A team that sends a "heads up" Slack message before every deploy is tightly coupled to whoever reads that message.
- **AI Application:** "List every external dependency this service has. For each dependency, identify the owning team. If the owning team is the same as this team, that's not an external dependency — it's internal complexity. Restructure accordingly."

---

## Section 03 — Practical Method (`#maneuver`)

**Title:** The Inverse Conway Protocol

**Subtitle:** A two-phase method: map your current mirror, then reshape deliberately. Never skip Phase 1.

### Phase 1 — Map the Mirror

**Step 01 — Draw the Communication Structure**
Before touching architecture, draw how your teams actually communicate — not the org chart, but the real flow. Who files tickets to whom? Which teams share on-call rotations? Where do deploys require coordination? This is your current architecture, expressed in human terms.

*Prompt block (questions to run with the team):*
```
Who does your team file tickets to?
Which teams file tickets to you?
Which deploys require you to notify another team?
Which teams share your on-call rotation?
Which services does your team call that another team owns?
```

**Step 02 — Overlay the System Architecture**
Place your actual service/module map next to the communication map. Find the matches: team boundaries that became service boundaries, coordination overhead that became synchronous API calls, ownership gaps that became shared databases. This is the mirror.

**Step 03 — Identify the Misalignments**
The gaps between the architecture you want and the architecture you have are almost always org problems in disguise. A service owned by two teams will never have a clean interface. A domain that spans three teams will have three implementations.

### Phase 2 — Reshape Deliberately

**Step 04 — Design the Target Team Structure**
Working backwards from the architecture you want: what team structure would naturally produce it? Map desired service boundaries to team ownership boundaries. Stream-aligned teams own a domain end-to-end. Platform teams provide capabilities as an internal product with an explicit API.

**Step 05 — Move Teams, Then Code**
Restructure team ownership *before* restructuring the code. Once the team boundary matches the desired service boundary, the code will follow through natural feature work — not a big-bang refactor. Trying to restructure the code before the org is like painting a house while the walls are still being moved.

**Step 06 — Apply the AI Maneuver**
Once teams own clean domains, deploy AI coding assistants within those boundaries. The AI generates code in the context of one team's codebase, following one team's conventions, calling one team's APIs. Conway's Law amplified by AI now works *for* you.

*Prompt block:*
```
You are working within the [team name] domain.
The services you own are: [list].
The external services you are allowed to call are: [list].
Do not suggest calling any service not on this list.
Generate code that respects these ownership boundaries.
```

---

## Section 04 — Anti-Patterns (`#anti`)

Comparison table: 4 rows, wrong vs. Conway-aware.

| Anti-Pattern | Conway-Aware Approach |
|---|---|
| **Design architecture first, hope org adapts** — Draw the ideal microservices diagram, then ask existing teams to own slices. Teams own whatever maps to headcount, not domain expertise. Architecture drifts back to org within a quarter. | **Design team structure first, let architecture follow** — Define team ownership boundaries based on business domains. Service boundaries emerge from team boundaries without a big-bang migration. |
| **Shared ownership of a service** — Two teams maintain the payments service because "it's too big for one team." Every interface decision is a negotiation. Every deploy requires coordination. The service grows without direction. | **Single team owns a domain end-to-end** — One team owns payments: schema, API, deploy pipeline, on-call. Other teams treat it as an external dependency with a stable contract. Decisions are fast; the interface stays clean. |
| **AI tools deployed org-wide before restructuring** — Every engineer uses an AI assistant in existing context. AI accelerates feature development within existing silos. Six months later, coupling is deeper than before and harder to untangle. | **Restructure teams first, then amplify with AI** — Establish clean domain ownership. Deploy AI assistants within those boundaries. AI-generated code naturally follows the domain model because engineers work within a single, well-bounded context. |
| **Platform team as a gatekeeper** — A central platform team that all other teams file tickets to. Every infrastructure need goes through a queue. The platform team is the tightest coupling point and the architecture's biggest bottleneck. | **Platform as an internal product** — Platform team provides self-service capabilities with documented APIs and SLAs. Other teams adopt them without coordination. The platform team thinks like a product team; its customers are internal engineers. |

---

## Section 05 — Case Study (`#case`)

**Title:** The Checkout Rewrite That Wasn't

**Setup:** A mid-size e-commerce company has a monolithic checkout service owned by three teams: Payments, Fulfillment, and Frontend Platform. Every release requires a joint deploy window. The architecture team proposes splitting into three services. Six months into the rewrite, the services are more coupled than the monolith — because the teams still coordinate on everything.

**Diagnosis:** The teams drew service boundaries on a whiteboard without changing who owned what. The communication structure didn't change, so the architecture didn't either — it just added network hops to the existing coupling.

**The Inverse Conway Move:** Engineering director pauses the rewrite. Splits ownership first:
- **Payments team** owns payment intent, charge, refund — full stack, schema to API
- **Fulfillment team** owns order lifecycle, inventory reservation, shipment — their own database, their own deploy
- **Checkout team** (new): owns the checkout UI and orchestration layer that calls Payments and Fulfillment as external APIs

No code moves on week one. Ownership boundaries are drawn, documented, and ratified.

**Result:** Over the following quarter, the natural feature work of three independent teams produces the service split the rewrite couldn't. The architecture emerged from the org design.

**AI Postscript:** The company rolls out AI coding assistants per team. Each AI context is scoped to one team's codebase. AI-generated code naturally respects domain boundaries because no engineer on the Payments team has context for Fulfillment code.

---

## Section 06 — Quiz (`#quiz`)

3 questions using the `answer(btn, correct)` pattern.

**Q1:** A team wants to split their monolith into microservices. What should they do first?
- A) Write service contracts and OpenAPI specs
- B) Migrate the database to separate schemas per domain
- C) **Restructure team ownership to match desired service boundaries** ✓
- D) Identify the most-changed files and split along those lines

*Correct:* Conway's Law means architecture follows the org. Change the org first; the code follows.
*Wrong:* Specs and schemas are premature — they'll be renegotiated along team lines anyway.

**Q2:** Your company deploys AI coding assistants to all engineers before any restructuring. What is the most likely outcome?
- A) AI helps engineers naturally refactor toward cleaner architecture
- B) **Existing team silos are accelerated and harder to untangle** ✓
- C) AI reduces the need for Conway-aware design
- D) Coupling decreases because AI writes more consistent code

*Correct:* AI amplifies the existing pattern. Misaligned team structures become architectural debt at machine speed.
*Wrong:* AI has no awareness of org structure. It generates code in whatever context the engineer provides.

**Q3:** A platform team receives 40 tickets per week from other teams. What is the Conway-aware fix?
- A) Hire more platform engineers to handle ticket volume
- B) Embed platform engineers in each product team
- C) **Redesign the platform as a self-service internal product with a stable API** ✓
- D) Consolidate all infrastructure into a single larger platform team

*Correct:* A ticket-driven platform is a coupling point. Self-service capabilities with stable contracts eliminate the synchronous dependency.
*Wrong:* Scaling a bottleneck doesn't remove it. The fix is to change the interface: from "file a ticket" to "call an API."

---

## Section 07 — Cheatsheet (`#cheatsheet`)

6-tile grid.

| Tile | Items |
|---|---|
| The Law | Systems mirror communication structures · Team boundaries become service boundaries · Coupling follows coordination overhead · You cannot architect your way out of an org problem |
| The Maneuver | Design team structure before system structure · One team owns one domain end-to-end · Move teams first, then let code follow · Target architecture → target team topology |
| Map the Mirror | Draw real communication flows, not org charts · Overlay team map onto service map · Shared ownership = future coupling · Every coordination meeting is a tight coupling |
| Warning Signs | Two teams own the same service · Deploys require cross-team coordination · A platform team runs on tickets · AI tools deployed before restructuring |
| AI Application | Restructure teams before deploying AI · Scope AI context to team's owned domain · AI amplifies existing patterns — align them first · "You work within [team] domain. Owned services: [list]." |
| The Standard | Can this team deploy without coordination? · Does one team own this domain end-to-end? · Is the platform self-service with a stable API? · Would AI context naturally respect this boundary? |

---

## Technical Conventions

Follows all conventions from `CLAUDE.md` and `first-principles.html`:

- Self-contained HTML, all CSS and JS embedded
- CSS custom properties on `:root` (dark default) and `[data-theme="light"]`
- `@media (prefers-color-scheme: light)` on `:root:not([data-theme="dark"])`
- Standard variable names: `--bg`, `--surface`, `--surface2`, `--border`, `--accent`, `--accent2`, `--accent3`, `--text`, `--muted`, `--danger`
- Fixed `#home-btn` top-left, `#theme-toggle` top-right, `#back-to-top` bottom-right
- Theme persisted to `localStorage` under key `theme`
- `togglePrinciple(el)` for expandable cards
- `answer(btn, correct)` for quiz
- Intersection Observer for scroll animations
- Google Fonts: Playfair Display, DM Mono, Syne
- No external CSS or JS files
