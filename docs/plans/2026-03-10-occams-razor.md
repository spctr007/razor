# Occam's Razor Page Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Create `occams-razor.html` — a self-contained educational page on Occam's Razor applied to software design, matching the conventions of `first-principles.html`.

**Architecture:** Single HTML file with all CSS and JS embedded. No external files, no build step. Reuses identical CSS variable names, font stack, and UX patterns from `first-principles.html`. Seven sections: Foundation → Core Framework → Practical Method → Anti-Patterns → Case Study → Quiz → Cheatsheet.

**Tech Stack:** Vanilla HTML/CSS/JS. Google Fonts (Playfair Display, DM Mono, Syne). No frameworks, no dependencies.

---

### Task 1: Scaffold the file — head, CSS variables, reset, base typography

**Files:**
- Create: `occams-razor.html`

**Step 1: Write the file skeleton**

Create `occams-razor.html` with `<head>`, Google Fonts link, and `<style>` block containing:
- CSS reset (`*, *::before, *::after`)
- `:root` dark-mode variables (copy exact values from `first-principles.html`)
- `[data-theme="light"]` variables (copy exact values)
- `@media (prefers-color-scheme: light)` block
- `body`, `html` base styles

Use these exact variable values (from `first-principles.html`):
```css
:root {
  --bg: #0a0a0f;
  --surface: #111118;
  --surface2: #1a1a25;
  --border: #2a2a3a;
  --accent: #e8c547;
  --accent2: #7c6af0;
  --accent3: #47c5e8;
  --text: #e8e8f0;
  --muted: #6b6b80;
  --danger: #e84747;
  --toggle-bg: #1a1a25;
  --toggle-border: #2a2a3a;
  --toggle-icon: '☀️';
}
[data-theme="light"] {
  --bg: #f5f4ef;
  --surface: #fffffe;
  --surface2: #eeecea;
  --border: #d8d5ce;
  --accent: #c4961a;
  --accent2: #5b4fd4;
  --accent3: #1a9dbf;
  --text: #1a1a28;
  --muted: #7a7870;
  --danger: #c43030;
  --toggle-bg: #eeecea;
  --toggle-border: #d8d5ce;
  --toggle-icon: '🌙';
}
```

**Step 2: Verify**

Open in browser. Page should be blank but dark (`#0a0a0f` background). No console errors.

**Step 3: Commit**
```bash
git add occams-razor.html
git commit -m "feat: scaffold occams-razor.html with CSS variables and reset"
```

---

### Task 2: Add all remaining CSS — layout, components, animations

**Files:**
- Modify: `occams-razor.html`

**Step 1: Add CSS blocks** in this order inside the `<style>` tag:

- **Theme toggle** (`#theme-toggle`, `#theme-toggle:hover`)
- **Hero** (`.hero`, `.hero-eyebrow`, `.hero-title`, `.hero-title em`, `.hero-subtitle`, `.hero-nav`, `.nav-pill`, `.nav-pill:hover`, `.scroll-hint`, `.scroll-line`)
- **Sections** (`section`, `.section-label`, `.section-title`, `.section-body`, `.definition-block`, `.definition-block cite`)
- **Principle cards** (`.principles-grid`, `.principle-card`, `.principle-card:hover`, `.principle-card.active`, `.principle-number`, `.principle-name`, `.principle-tagline`, `.principle-expand`, `.principle-card.active .principle-expand`, `.example-box`, `.example-box .ex-label`, `.example-box p`)
- **Workflow** (`.workflow`, `.workflow-step`, `.workflow-step:not(:last-child)::after`, `.step-marker`, `.workflow-step:hover .step-marker`, `.step-marker .step-num`, `.step-marker .step-icon`, `.step-content`, `.step-title`, `.step-desc`, `.prompt-block`, `.prompt-block::before`, `.prompt-block .var`)
- **Comparison table** (`.comparison`, `.comp-header`, `.comp-header div`, `.comp-row`, `.comp-row:hover`, `.comp-row div`, `.comp-row div:first-child`, `.comp-row div:nth-child(2)`, `.comp-row div:nth-child(3)`)
- **Case study** (`.case-study`, `.case-tag`, `.case-question`, `.decomposition`, `.decomp-item`, `.decomp-item:hover`, `.decomp-arrow`, `.decomp-text`, `.decomp-text strong`)
- **Quiz** (`.quiz-container`, `.quiz-card`, `.quiz-q`, `.quiz-options`, `.quiz-option`, `.quiz-option::before`, `.quiz-option:hover:not(.answered)`, `.quiz-option.correct`, `.quiz-option.wrong`, `.quiz-feedback`, `.quiz-feedback.show`, `.quiz-feedback.good`, `.quiz-feedback.bad`)
- **Cheatsheet** (`.cheatsheet`, `.cs-item`, `.cs-icon`, `.cs-title`, `.cs-list`, `.cs-list li`, `.cs-list li::before`)
- **Animations** (`@keyframes fadeUp`, `@keyframes slide`)
- **Divider** (`.divider`)
- **Footer** (`footer`)
- **Responsive** (`@media (max-width: 768px)`)
- **Observe animation** (`.observe` + `.visible` pattern using `opacity: 0; transform: translateY(20px)` → animated in)

Copy values directly from `first-principles.html` for all of these.

**Step 2: Verify**

Page still blank (no HTML body yet) but stylesheet loads with no errors.

**Step 3: Commit**
```bash
git add occams-razor.html
git commit -m "feat: add full CSS component styles to occams-razor"
```

---

### Task 3: Add HTML body — theme toggle + hero section

**Files:**
- Modify: `occams-razor.html`

**Step 1: Add to `<body>`:**

```html
<!-- THEME TOGGLE -->
<button id="theme-toggle" aria-label="Toggle light/dark mode" title="Toggle theme">
  <span id="theme-icon">☀️</span>
</button>

<!-- HERO -->
<div class="hero">
  <div class="hero-eyebrow">A mental model for the AI age</div>
  <h1 class="hero-title">Occam's<br><em>Razor</em><br>in Software</h1>
  <p class="hero-subtitle">The simplest solution that works is usually correct. Learn to cut unnecessary complexity — and use AI without adding more layers than you need.</p>
  <nav class="hero-nav">
    <a class="nav-pill" href="#what">What it is</a>
    <a class="nav-pill" href="#principles">The 5 principles</a>
    <a class="nav-pill" href="#workflow">AI workflow</a>
    <a class="nav-pill" href="#antipatterns">Anti-patterns</a>
    <a class="nav-pill" href="#casestudy">Case study</a>
    <a class="nav-pill" href="#quiz">Test yourself</a>
  </nav>
  <div class="scroll-hint">
    <div class="scroll-line"></div>
    SCROLL TO LEARN
  </div>
</div>
```

**Step 2: Verify**

Hero appears. Title reads "Occam's / Razor / in Software" in Playfair Display. Nav pills render. Dark background.

**Step 3: Commit**
```bash
git add occams-razor.html
git commit -m "feat: add hero section to occams-razor"
```

---

### Task 4: Add Section 01 — Foundation (What is Occam's Razor?)

**Files:**
- Modify: `occams-razor.html`

**Step 1: Add after hero:**

```html
<!-- WHAT IS IT -->
<section id="what">
  <div class="section-label">01 / Foundation</div>
  <h2 class="section-title">What is<br>Occam's Razor?</h2>
  <p class="section-body">Occam's Razor is a problem-solving principle stating that among competing hypotheses, the one with the fewest assumptions should be selected. In software, it means: don't build more than the problem requires.</p>

  <div class="definition-block">
    <p>Entities must not be multiplied beyond necessity. When two explanations fit the facts equally well, prefer the simpler one.</p>
    <cite>— William of Ockham, 14th century philosopher — applied daily by engineers who ship</cite>
  </div>

  <br><br>
  <p class="section-body">In software, this translates directly: don't introduce abstractions, patterns, or infrastructure that the current problem doesn't require. Every layer you add must earn its place — it carries a cost in complexity, maintenance, and cognitive load for every engineer who comes after you.</p>
  <br>
  <p class="section-body">With AI tools, this matters <strong style="color:var(--text)">more than ever</strong> — because AI will happily generate sophisticated, pattern-heavy, over-engineered solutions to simple problems if you don't ask for simpler ones explicitly.</p>
</section>

<hr class="divider">
```

**Step 2: Verify**

Section renders with definition block, quotes, body text. Divider appears below.

**Step 3: Commit**
```bash
git add occams-razor.html
git commit -m "feat: add foundation section to occams-razor"
```

---

### Task 5: Add Section 02 — Core Framework (5 expandable principle cards)

**Files:**
- Modify: `occams-razor.html`

**Step 1: Add after the divider:**

```html
<!-- 5 PRINCIPLES -->
<section id="principles">
  <div class="section-label">02 / Core Framework</div>
  <h2 class="section-title">The 5 Principles<br>Applied to Software</h2>
  <p class="section-body">Click each principle to expand it with software engineering examples and how AI fits in.</p>

  <div class="principles-grid" id="principlesGrid">

    <div class="principle-card" onclick="togglePrinciple(this)">
      <div class="principle-number">PRINCIPLE 01</div>
      <div class="principle-name">Prefer the Simpler Explanation</div>
      <div class="principle-tagline">Don't multiply abstractions beyond what the problem demands.</div>
      <div class="principle-expand">
        <p>Every architectural element — a message queue, an event bus, a caching layer, a service mesh — exists to solve a real problem. If you can't articulate which specific problem it solves for you right now, you probably don't need it. The cost of unnecessary complexity is paid by every engineer who reads your code afterward.</p>
        <div class="example-box">
          <div class="ex-label">Software Example</div>
          <p>"We need Kafka for our notification system." Why? "For scalability." Current load: 50 events/day. A simple database table with a background job does the same job with 90% less operational complexity and zero new infrastructure to learn.</p>
        </div>
        <div class="example-box" style="border-left-color: var(--accent3); margin-top: 0.75rem;">
          <div class="ex-label" style="color: var(--accent3);">AI Application</div>
          <p>When AI suggests an architecture, ask: "What is the simplest solution that meets only the stated requirements? Give me that first, then tell me what would need to change if scale increased 100x."</p>
        </div>
      </div>
    </div>

    <div class="principle-card" onclick="togglePrinciple(this)">
      <div class="principle-number">PRINCIPLE 02</div>
      <div class="principle-name">Measure Cognitive Load, Not Line Count</div>
      <div class="principle-tagline">Complexity lives in the reader's head, not the editor's line counter.</div>
      <div class="principle-expand">
        <p>Simple code isn't necessarily short code. A 10-line function that introduces 4 new concepts is more complex than a 40-line function that reads like plain English. Occam's Razor applied to code means minimizing the number of concepts, not characters. Fewer moving parts, fewer mental models to hold.</p>
        <div class="example-box">
          <div class="ex-label">Software Example</div>
          <p>A clever one-liner using reduce, flatMap, and a custom comparator replaces 20 lines of a readable loop. The one-liner "wins" on line count and loses on every other metric: it's harder to debug, harder to modify, harder to read in a 2am incident.</p>
        </div>
        <div class="example-box" style="border-left-color: var(--accent3); margin-top: 0.75rem;">
          <div class="ex-label" style="color: var(--accent3);">AI Application</div>
          <p>Tell AI: "Write this for a junior engineer joining the team tomorrow, not for impressing senior engineers. Optimize for clarity, not cleverness. If you use an advanced language feature, explain whether a simpler form would work just as well."</p>
        </div>
      </div>
    </div>

    <div class="principle-card" onclick="togglePrinciple(this)">
      <div class="principle-number">PRINCIPLE 03</div>
      <div class="principle-name">Eliminate Unnecessary Layers</div>
      <div class="principle-tagline">Every abstraction has a cost. Make each layer earn its place.</div>
      <div class="principle-expand">
        <p>Abstraction is a tool, not a virtue. A wrapper class that wraps a wrapper that wraps an interface that wraps a library call doesn't make the code cleaner — it makes it harder to trace, harder to debug, and harder to delete. Good software has the minimum number of layers needed to separate genuinely different concerns.</p>
        <div class="example-box">
          <div class="ex-label">Software Example</div>
          <p>A "Repository pattern" over an ORM over a database driver is three layers to query one table. Ask: does each layer represent a genuinely separate concern, or is it abstraction for abstraction's sake? If you collapsed two of them, would anything get harder to change independently?</p>
        </div>
        <div class="example-box" style="border-left-color: var(--accent3); margin-top: 0.75rem;">
          <div class="ex-label" style="color: var(--accent3);">AI Application</div>
          <p>Ask AI: "Here's my proposed layering. For each layer, tell me: what specifically would be harder to change if this layer didn't exist? If the answer is 'nothing', let's remove it."</p>
        </div>
      </div>
    </div>

    <div class="principle-card" onclick="togglePrinciple(this)">
      <div class="principle-number">PRINCIPLE 04</div>
      <div class="principle-name">Don't Architect for Hypotheticals</div>
      <div class="principle-tagline">Solve the problem you have. The future will bring its own requirements.</div>
      <div class="principle-expand">
        <p>Over-engineering is almost always driven by imagined futures: "we might need multi-tenancy," "we might need to swap databases," "we might need to scale to millions of users." These futures rarely arrive as imagined — and when they do, the pre-built abstractions are usually wrong anyway. Build for today's requirements with today's constraints. Refactor when the future becomes the present.</p>
        <div class="example-box">
          <div class="ex-label">Software Example</div>
          <p>An API designed to support "any payment provider" through an abstraction layer, when you have exactly one payment provider and no plans to change. The abstraction makes Stripe harder to use while providing no current value. YAGNI: You Aren't Gonna Need It.</p>
        </div>
        <div class="example-box" style="border-left-color: var(--accent3); margin-top: 0.75rem;">
          <div class="ex-label" style="color: var(--accent3);">AI Application</div>
          <p>Before asking AI to make something "extensible" or "pluggable" — stop. Ask instead: "What are the actual requirements I need to meet this week? Build exactly that, and tell me what would need to change if requirement X appeared in 6 months."</p>
        </div>
      </div>
    </div>

    <div class="principle-card" onclick="togglePrinciple(this)">
      <div class="principle-number">PRINCIPLE 05</div>
      <div class="principle-name">Simple ≠ Simplistic</div>
      <div class="principle-tagline">Simplicity requires more thought, not less. Earned simplicity is the hardest kind.</div>
      <div class="principle-expand">
        <p>Occam's Razor is not an excuse for lazy design. A "simple" solution that ignores error handling, security, or edge cases isn't simple — it's incomplete. True simplicity means a solution that is complete, correct, and easy to understand. It often takes more effort to produce than a complex one, because you have to ruthlessly cut without losing correctness.</p>
        <div class="example-box">
          <div class="ex-label">Software Example</div>
          <p>A simple REST endpoint that is also safe (validates input, returns correct error codes, handles concurrency, has a timeout) is harder to write than one that just works for the happy path. Simplicity in design — few moving parts — is different from simplicity in effort.</p>
        </div>
        <div class="example-box" style="border-left-color: var(--accent3); margin-top: 0.75rem;">
          <div class="ex-label" style="color: var(--accent3);">AI Application</div>
          <p>Ask AI: "Is this solution actually simple, or is it just incomplete? What necessary complexity am I dropping by going with this approach? What's the minimum I need to add to make this production-safe without adding unnecessary layers?"</p>
        </div>
      </div>
    </div>

  </div>
</section>

<hr class="divider">
```

**Step 2: Verify**

5 cards render. Clicking each expands/collapses the `.principle-expand` div (requires JS from Task 8 — cards will be static until then, that's fine).

**Step 3: Commit**
```bash
git add occams-razor.html
git commit -m "feat: add core framework principles section"
```

---

### Task 6: Add Section 03 — Practical Method (AI workflow)

**Files:**
- Modify: `occams-razor.html`

**Step 1: Add after the divider:**

```html
<!-- AI WORKFLOW -->
<section id="workflow">
  <div class="section-label">03 / Practical Method</div>
  <h2 class="section-title">The Occam's Razor<br>AI Workflow</h2>
  <p class="section-body">A five-step method for applying the razor before, during, and after generating code with AI.</p>

  <div class="workflow">

    <div class="workflow-step">
      <div class="step-marker">
        <span class="step-num">STEP 01</span>
        <span class="step-icon">✂️</span>
      </div>
      <div class="step-content">
        <div class="step-title">State Only What You Need Now</div>
        <p class="step-desc">Before prompting, write down your actual requirements — not imagined future ones. Strip qualifiers like "someday," "maybe," and "in case we." Only what you need to ship this week counts.</p>
        <div class="prompt-block">
"My current requirements are:<br>
<span class="var">[list only concrete, present-tense requirements]</span><br><br>
Explicitly NOT in scope: <span class="var">[list things that sound tempting but aren't needed yet]</span><br><br>
Design the simplest solution that meets only the in-scope requirements.<br>
Do not add flexibility, extensibility, or abstraction beyond what is needed."</div>
      </div>
    </div>

    <div class="workflow-step">
      <div class="step-marker">
        <span class="step-num">STEP 02</span>
        <span class="step-icon">🔬</span>
      </div>
      <div class="step-content">
        <div class="step-title">Challenge Every Component</div>
        <p class="step-desc">For every piece of the proposed solution, ask: what specific requirement does this serve? If you can't answer, it's a candidate for removal.</p>
        <div class="prompt-block">
"Here's the solution you proposed:<br>
<span class="var">[paste solution]</span><br><br>
For each component or layer, answer: what specific requirement<br>
from my list does this serve?<br><br>
Flag anything that doesn't map directly to a stated requirement.<br>
Then suggest what to remove."</div>
      </div>
    </div>

    <div class="workflow-step">
      <div class="step-marker">
        <span class="step-num">STEP 03</span>
        <span class="step-icon">📉</span>
      </div>
      <div class="step-content">
        <div class="step-title">Ask for the Simpler Version</div>
        <p class="step-desc">After seeing the first solution, always ask for a simpler one. AI defaults to comprehensive. You want minimal.</p>
        <div class="prompt-block">
"Now give me a version that is meaningfully simpler.<br>
Drop any pattern or layer that isn't strictly required.<br><br>
What are the concrete trade-offs of the simpler version<br>
versus the previous one?<br>
Under what conditions would the simpler version break?"</div>
      </div>
    </div>

    <div class="workflow-step">
      <div class="step-marker">
        <span class="step-num">STEP 04</span>
        <span class="step-icon">⚖️</span>
      </div>
      <div class="step-content">
        <div class="step-title">Evaluate What You'd Lose</div>
        <p class="step-desc">For each thing removed in simplification, understand the cost. Some complexity is essential — removing it is not simplicity, it's incompleteness. Know the difference before deciding.</p>
        <div class="prompt-block">
"Between the simpler and more complex versions,<br>
what does the simpler one handle incorrectly or not at all?<br><br>
Separate this into two lists:<br>
1. Things I'd genuinely need to add back (edge cases, errors, security)<br>
2. Things I only thought I'd need (premature flexibility, speculative scale)"</div>
      </div>
    </div>

    <div class="workflow-step">
      <div class="step-marker">
        <span class="step-num">STEP 05</span>
        <span class="step-icon">🚀</span>
      </div>
      <div class="step-content">
        <div class="step-title">Ship and Set a Complexity Budget</div>
        <p class="step-desc">Once you've applied the razor, ship the result. Set a written rule: no new abstraction layers without a concrete requirement that currently can't be met without them.</p>
        <div class="prompt-block">
"We've shipped the simple version. Help me write a one-paragraph<br>
decision record that captures:<br>
1. What we chose and why<br>
2. What we explicitly decided NOT to build<br>
3. What specific signal would tell us to add complexity later<br><br>
This will live in our docs so future engineers don't re-add<br>what we deliberately removed."</div>
      </div>
    </div>

  </div>
</section>

<hr class="divider">
```

**Step 2: Verify**

5 workflow steps render in a vertical timeline with icons and prompt blocks.

**Step 3: Commit**
```bash
git add occams-razor.html
git commit -m "feat: add AI workflow section to occams-razor"
```

---

### Task 7: Add Section 04 — Anti-Patterns comparison table

**Files:**
- Modify: `occams-razor.html`

**Step 1: Add after the divider:**

```html
<!-- ANTI-PATTERNS -->
<section id="antipatterns">
  <div class="section-label">04 / Anti-Patterns</div>
  <h2 class="section-title">When Engineers<br>Violate the Razor</h2>
  <p class="section-body">These are the most common ways complexity gets added without necessity — and what applying the razor looks like instead.</p>

  <div class="comparison">
    <div class="comp-header">
      <div>Scenario</div>
      <div>Over-engineered</div>
      <div>Occam's Approach</div>
    </div>

    <div class="comp-row">
      <div>User authentication for a 3-person internal tool</div>
      <div>OAuth2 with identity provider, refresh token rotation, role-based permission matrix, audit logging service</div>
      <div>HTTP Basic Auth or a shared secret header. Add OAuth when the team grows or compliance requires it.</div>
    </div>

    <div class="comp-row">
      <div>Config values that differ between environments</div>
      <div>Feature flag system with a remote dashboard, SDK integration, percentage rollouts, A/B experiment tracking</div>
      <div>Environment variables. A `.env` file. Change the value to change the behavior.</div>
    </div>

    <div class="comp-row">
      <div>Storing 500 records that rarely change</div>
      <div>Redis cache in front of PostgreSQL with cache invalidation events, TTL tuning, warm-up scripts</div>
      <div>Query the database. Add a cache when profiling shows the query is actually slow.</div>
    </div>

    <div class="comp-row">
      <div>Background job that runs once a day</div>
      <div>Distributed task queue (Celery/BullMQ), worker autoscaling, retry policies, dead-letter queue, monitoring dashboard</div>
      <div>A cron job. Or a simple database row with a `run_at` column checked every minute.</div>
    </div>

    <div class="comp-row">
      <div>API consumed by a single frontend you own</div>
      <div>Versioned REST API with hypermedia links, OpenAPI spec, SDK generation, backwards-compatibility policy</div>
      <div>Unversioned endpoints. Change both sides together. Add versioning when a second consumer appears.</div>
    </div>

    <div class="comp-row">
      <div>Sharing code between two services</div>
      <div>Private npm/PyPI package with its own repo, CI/CD, semver, changelog, and dependency update bot</div>
      <div>Copy the code. Refactor to a shared package when the duplication becomes an actual maintenance problem.</div>
    </div>
  </div>
</section>

<hr class="divider">
```

**Step 2: Verify**

6-row comparison table renders with correct column colors (danger for over-engineered, accent3 for Occam's approach).

**Step 3: Commit**
```bash
git add occams-razor.html
git commit -m "feat: add anti-patterns comparison table"
```

---

### Task 8: Add Section 05 — Case Study

**Files:**
- Modify: `occams-razor.html`

**Step 1: Add after the divider:**

```html
<!-- CASE STUDY -->
<section id="casestudy">
  <div class="section-label">05 / Worked Example</div>
  <h2 class="section-title">The Notification<br>System</h2>
  <p class="section-body">A team is asked to build a notification system for their SaaS product. Watch how Occam's Razor changes the outcome.</p>

  <div class="case-study">
    <div class="case-tag">⚡ Case Study</div>
    <div class="case-question">"We need to notify users when things happen in the system."</div>

    <p style="color: var(--muted); font-size: 0.9rem; margin-bottom: 1.5rem;">Actual requirements gathered: send an email when a report is ready. ~200 users. Reports run nightly.</p>

    <p style="font-family: 'DM Mono', monospace; font-size: 0.7rem; letter-spacing: 0.15em; color: var(--danger); margin-bottom: 1rem;">THE OVER-ENGINEERED RESPONSE</p>

    <div class="decomposition">
      <div class="decomp-item">
        <div class="decomp-arrow">→</div>
        <div class="decomp-text">
          <strong>Event Bus</strong>
          Kafka cluster to emit domain events from every service. "Notifications are just one consumer — this will scale to anything."
        </div>
      </div>
      <div class="decomp-item">
        <div class="decomp-arrow">→</div>
        <div class="decomp-text">
          <strong>Notification Service</strong>
          Dedicated microservice with its own database, deployment pipeline, and API. Subscribes to the event bus.
        </div>
      </div>
      <div class="decomp-item">
        <div class="decomp-arrow">→</div>
        <div class="decomp-text">
          <strong>Template Engine</strong>
          Handlebars-based template system with a database-backed template store, so non-engineers can edit emails.
        </div>
      </div>
      <div class="decomp-item">
        <div class="decomp-arrow">→</div>
        <div class="decomp-text">
          <strong>Preference Center</strong>
          User-facing notification settings UI. Per-event type toggles. Stored in the notification service DB.
        </div>
      </div>
    </div>

    <p style="color: var(--muted); font-size: 0.85rem; margin: 1.5rem 0;">Timeline: 6 weeks. Three engineers. Still not shipped.</p>

    <p style="font-family: 'DM Mono', monospace; font-size: 0.7rem; letter-spacing: 0.15em; color: #47e87a; margin-bottom: 1rem;">THE OCCAM'S RAZOR RESPONSE</p>

    <div class="decomposition">
      <div class="decomp-item" style="border-left-color: #47e87a;">
        <div class="decomp-arrow" style="color: #47e87a;">→</div>
        <div class="decomp-text">
          <strong style="color: #47e87a;">A cron job</strong>
          Runs at 6am. Queries: "which reports finished since yesterday?" One SQL query.
        </div>
      </div>
      <div class="decomp-item" style="border-left-color: #47e87a;">
        <div class="decomp-arrow" style="color: #47e87a;">→</div>
        <div class="decomp-text">
          <strong style="color: #47e87a;">Sendgrid API call</strong>
          For each result row, send one email using a hardcoded template. Plain text with one link.
        </div>
      </div>
      <div class="decomp-item" style="border-left-color: #47e87a;">
        <div class="decomp-arrow" style="color: #47e87a;">→</div>
        <div class="decomp-text">
          <strong style="color: #47e87a;">A log line</strong>
          Print "Sent N emails" to stdout. Your existing log aggregator captures it.
        </div>
      </div>
    </div>

    <p style="color: var(--muted); font-size: 0.85rem; margin: 1.5rem 0;">Timeline: 1 day. One engineer. Ships before standup.</p>

    <div class="example-box" style="margin-top: 1.5rem;">
      <div class="ex-label">What Changes When Requirements Change?</div>
      <p>If users need real-time notifications → add WebSockets at that point. If templates need to be editable → add a template table then. If volume hits 50,000 users → profile first, optimize second. Each requirement, when it actually arrives, drives the right addition. No premature complexity needed.</p>
    </div>
  </div>
</section>

<hr class="divider">
```

**Step 2: Verify**

Case study renders with two contrasting decomposition lists (red for over-engineered, green for Occam's). Timeline callouts visible.

**Step 3: Commit**
```bash
git add occams-razor.html
git commit -m "feat: add worked case study section"
```

---

### Task 9: Add Section 06 — Quiz

**Files:**
- Modify: `occams-razor.html`

**Step 1: Add after the divider:**

```html
<!-- QUIZ -->
<section id="quiz">
  <div class="section-label">06 / Test Yourself</div>
  <h2 class="section-title">Apply the Razor</h2>
  <p class="section-body">Three scenarios. Apply Occam's Razor and see if your instinct aligns with the principle.</p>

  <div class="quiz-container">

    <div class="quiz-card">
      <div class="quiz-q">A startup with 50 users wants to "future-proof" their data layer by building a custom ORM abstraction over PostgreSQL so they can "swap databases later." What does Occam's Razor say?</div>
      <div class="quiz-options">
        <button class="quiz-option" data-letter="A" onclick="answer(this, false)">Build the abstraction now — it'll be harder to add later and database swaps are common</button>
        <button class="quiz-option" data-letter="B" onclick="answer(this, true)">Use the ORM directly. If you ever need to swap databases, the abstraction you'd build then will be better informed by actual requirements</button>
        <button class="quiz-option" data-letter="C" onclick="answer(this, false)">Build a minimal abstraction — just one thin layer so you're halfway there</button>
        <button class="quiz-option" data-letter="D" onclick="answer(this, false)">Evaluate 5 database options first to make the right long-term choice</button>
      </div>
      <div class="quiz-feedback">
        <strong>Correct.</strong> Database swaps are rare, and when they happen, the migration is never clean regardless of your abstraction layer. The simpler explanation: use your ORM directly, solve the problem you have, and revisit if the hypothetical ever materializes. YAGNI and Occam's Razor agree.
      </div>
    </div>

    <div class="quiz-card">
      <div class="quiz-q">Which of these is an example of violating Occam's Razor, rather than applying it?</div>
      <div class="quiz-options">
        <button class="quiz-option" data-letter="A" onclick="answer(this, false)">Skipping error handling in an API endpoint that accepts external input</button>
        <button class="quiz-option" data-letter="B" onclick="answer(this, false)">Storing user sessions in a cookie instead of a distributed session store for a single-server app</button>
        <button class="quiz-option" data-letter="C" onclick="answer(this, true)">Adding a plugin architecture to a CLI tool that has exactly one use case and one team</button>
        <button class="quiz-option" data-letter="D" onclick="answer(this, false)">Using a flat file for config instead of a database when the config rarely changes</button>
      </div>
      <div class="quiz-feedback">
        <strong>Correct.</strong> A plugin architecture multiplies entities (abstractions, interfaces, conventions) beyond necessity when there's only one use case and one team. Options A skips necessary complexity (error handling is required, not optional). Options B and D are good Razor applications — simpler solutions for simpler problems.
      </div>
    </div>

    <div class="quiz-card">
      <div class="quiz-q">A team ships a "simple" authentication system with no input validation, no rate limiting, and no token expiry. They justify it as "Occam's Razor — fewest moving parts." Are they applying the principle correctly?</div>
      <div class="quiz-options">
        <button class="quiz-option" data-letter="A" onclick="answer(this, false)">Yes — they've eliminated unnecessary complexity and can add security features later</button>
        <button class="quiz-option" data-letter="B" onclick="answer(this, true)">No — they've confused simple with simplistic. Those aren't optional features, they're necessary correctness</button>
        <button class="quiz-option" data-letter="C" onclick="answer(this, false)">Depends on the threat model — for an internal tool, this might be fine</button>
        <button class="quiz-option" data-letter="D" onclick="answer(this, false)">Yes, as long as they document the missing features as future work</button>
      </div>
      <div class="quiz-feedback">
        <strong>Correct.</strong> Occam's Razor eliminates unnecessary complexity, not necessary complexity. Input validation, rate limiting, and token expiry are requirements of a correct auth system — not optional extras. Removing them makes the solution incomplete, not simple. Simple ≠ simplistic.
      </div>
    </div>

  </div>
</section>

<hr class="divider">
```

**Step 2: Verify**

3 quiz cards render. Clicking options should work after JS is added in Task 10.

**Step 3: Commit**
```bash
git add occams-razor.html
git commit -m "feat: add quiz section"
```

---

### Task 10: Add Cheatsheet + Footer

**Files:**
- Modify: `occams-razor.html`

**Step 1: Add after the divider:**

```html
<!-- CHEATSHEET -->
<section id="cheatsheet">
  <div class="section-label">07 / Quick Reference</div>
  <h2 class="section-title">The Razor<br>Cheatsheet</h2>
  <p class="section-body">Keep these questions close when you're designing or reviewing code.</p>

  <div class="cheatsheet">
    <div class="cs-item">
      <div class="cs-icon">✂️</div>
      <div class="cs-title">The Razor Question</div>
      <ul class="cs-list">
        <li>Does this layer exist to solve a real, current requirement?</li>
        <li>Can I name the specific problem this abstraction solves?</li>
        <li>What happens if I delete this? Does anything break?</li>
        <li>Is this complexity earned, or speculative?</li>
      </ul>
    </div>
    <div class="cs-item">
      <div class="cs-icon">🚩</div>
      <div class="cs-title">Red Flags</div>
      <ul class="cs-list">
        <li>"We might need this later"</li>
        <li>"Let's make this pluggable/extensible"</li>
        <li>"This is the industry standard pattern"</li>
        <li>"Let's abstract this so we can swap it out"</li>
        <li>"This will scale to millions"</li>
      </ul>
    </div>
    <div class="cs-item">
      <div class="cs-icon">✅</div>
      <div class="cs-title">Simple ≠ Simplistic</div>
      <ul class="cs-list">
        <li>Error handling is required, not optional</li>
        <li>Security is never premature complexity</li>
        <li>Observability belongs in day one</li>
        <li>Simplicity means fewer moving parts, not fewer safety nets</li>
      </ul>
    </div>
    <div class="cs-item">
      <div class="cs-icon">🤖</div>
      <div class="cs-title">AI Prompts</div>
      <ul class="cs-list">
        <li>"Give me the simplest version that meets only these requirements"</li>
        <li>"What would you remove if I told you we have 100 users?"</li>
        <li>"What's missing from the simpler version that's actually required?"</li>
        <li>"Write a decision record for what we chose not to build"</li>
      </ul>
    </div>
    <div class="cs-item">
      <div class="cs-icon">📐</div>
      <div class="cs-title">The Complexity Budget</div>
      <ul class="cs-list">
        <li>Every new layer needs a written justification</li>
        <li>No abstraction without a second use case</li>
        <li>No caching before profiling</li>
        <li>No queue before the synchronous version fails</li>
      </ul>
    </div>
    <div class="cs-item">
      <div class="cs-icon">🔄</div>
      <div class="cs-title">When to Add Complexity</div>
      <ul class="cs-list">
        <li>When a specific requirement can't be met without it</li>
        <li>When profiling shows a concrete bottleneck</li>
        <li>When a second consumer actually appears</li>
        <li>When the simpler version demonstrably fails in production</li>
      </ul>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <span>Occam's Razor · Software Engineering with AI</span>
  <span>A mental model series</span>
</footer>
```

**Step 2: Verify**

6-cell cheatsheet grid renders. Footer appears at bottom.

**Step 3: Commit**
```bash
git add occams-razor.html
git commit -m "feat: add cheatsheet and footer"
```

---

### Task 11: Add JavaScript — theme toggle, card expand, quiz, scroll animations

**Files:**
- Modify: `occams-razor.html`

**Step 1: Add `<script>` block before `</body>`:**

```html
<script>
  // ── THEME ──
  const root = document.documentElement;
  const toggle = document.getElementById('theme-toggle');
  const icon = document.getElementById('theme-icon');

  const saved = localStorage.getItem('theme');
  if (saved) {
    root.setAttribute('data-theme', saved);
    icon.textContent = saved === 'light' ? '🌙' : '☀️';
  }

  toggle.addEventListener('click', () => {
    const current = root.getAttribute('data-theme');
    const next = current === 'light' ? 'dark' : 'light';
    root.setAttribute('data-theme', next);
    localStorage.setItem('theme', next);
    icon.textContent = next === 'light' ? '🌙' : '☀️';
  });

  // ── EXPANDABLE CARDS ──
  function togglePrinciple(el) {
    const isActive = el.classList.contains('active');
    document.querySelectorAll('.principle-card').forEach(c => c.classList.remove('active'));
    if (!isActive) el.classList.add('active');
  }

  // ── QUIZ ──
  function answer(btn, correct) {
    const card = btn.closest('.quiz-card');
    if (card.querySelector('.answered')) return;
    const feedback = card.querySelector('.quiz-feedback');
    card.querySelectorAll('.quiz-option').forEach(b => {
      b.classList.add('answered');
      b.style.pointerEvents = 'none';
    });
    btn.classList.add(correct ? 'correct' : 'wrong');
    feedback.classList.add('show', correct ? 'good' : 'bad');
  }

  // ── SCROLL ANIMATIONS ──
  const observer = new IntersectionObserver(entries => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.classList.add('visible');
        observer.unobserve(e.target);
      }
    });
  }, { threshold: 0.1 });

  document.querySelectorAll('section, .principle-card, .workflow-step, .comp-row, .cs-item, .quiz-card').forEach(el => {
    el.classList.add('observe');
    observer.observe(el);
  });
</script>
```

Also add these CSS rules for the observe/visible animation pattern (add to the `<style>` block):
```css
.observe {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.5s ease, transform 0.5s ease;
}
.observe.visible {
  opacity: 1;
  transform: translateY(0);
}
```

**Step 2: Verify**

- Theme toggle switches between light/dark and persists on refresh
- Clicking a principle card expands it; clicking again collapses; clicking another collapses the previous
- Quiz answers show correct/wrong feedback; second click is ignored
- Scroll animations trigger as sections enter viewport

**Step 3: Commit**
```bash
git add occams-razor.html
git commit -m "feat: add theme toggle, card expand, quiz, and scroll animations"
```

---

### Task 12: Update CLAUDE.md pages table + final verification

**Files:**
- Modify: `CLAUDE.md`

**Step 1: Update the Pages table** in CLAUDE.md from:
```
| `occams-razor.html` | Occam's Razor applied to software design (planned) |
```
to:
```
| `occams-razor.html` | Occam's Razor applied to software design |
```

**Step 2: Open in browser and verify end-to-end:**
- Dark mode default, light mode toggle works and persists
- All 7 sections visible and properly styled
- Hero nav pills scroll to correct sections
- Principle cards expand/collapse
- Workflow steps render with prompt blocks
- Comparison table colors correct
- Case study renders both decomposition lists
- All 3 quiz questions work (correct + incorrect paths)
- Cheatsheet grid renders 6 cells
- Scroll animations trigger

**Step 3: Commit**
```bash
git add CLAUDE.md
git commit -m "docs: mark occams-razor.html as complete in CLAUDE.md"
```

---

**Plan complete.**
