# Chesterton's Fence Page — Implementation Plan

> **For agentic workers:** REQUIRED: Use superpowers:subagent-driven-development (if subagents available) or superpowers:executing-plans to implement this plan. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build `chesterton-fence.html` — a self-contained educational page on Chesterton's Fence applied to AI-assisted software engineering, following the exact conventions of `occams-razor.html`.

**Architecture:** Single HTML file with all CSS and JS embedded inline. No build step, no external dependencies beyond Google Fonts. Seven sections: Foundation → 5 Principles → Archaeology Protocol → Anti-Patterns → Case Study → Quiz → Cheatsheet.

**Tech Stack:** HTML5, CSS3 (custom properties, grid, flexbox), vanilla JS (IntersectionObserver, localStorage), Google Fonts (Playfair Display, DM Mono, Syne).

**Spec:** `docs/superpowers/specs/2026-03-13-chestertons-fence-design.md`

**Verification:** This project has no test suite. Each task ends with a browser verification step — open the file via `\\wsl$\Ubuntu\home\eslavag\Development\github\razor\chesterton-fence.html` in Windows File Explorer.

---

## Chunk 1: Scaffold, CSS, and Hero

### Task 1: Create the HTML shell with full CSS

**Files:**
- Create: `chesterton-fence.html`

Read `occams-razor.html` in full before writing anything — the CSS is the source of truth for all variables, components, and patterns.

- [ ] **Step 1: Create `chesterton-fence.html` with the full CSS block**

Copy the entire CSS from `occams-razor.html` verbatim (lines 1–910 approximately). Update only:
- `<title>`: `Chesterton's Fence · Software Engineering with AI`
- Hero gradient colors: keep `rgba(124,106,240,0.15)` and `rgba(232,197,71,0.08)` — same palette

The CSS includes: CSS variables (dark/light), home button, back-to-top, theme toggle, hero, nav pills, scroll hint, section labels, section titles/body, definition block, principles grid + cards, workflow steps + prompt blocks, comparison table, case study block, decomp items, example boxes, quiz cards + options + feedback, cheatsheet grid, footer, animations, and all IntersectionObserver fade-in rules.

Do not modify any CSS. Copy it exactly.

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Chesterton's Fence · Software Engineering with AI</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;0,900;1,400;1,700&family=DM+Mono:wght@300;400;500&family=Syne:wght@400;600;700;800&display=swap" rel="stylesheet">
<style>
  /* paste full CSS from occams-razor.html here */
</style>
</head>
<body>
<!-- content goes here in later tasks -->
</body>
</html>
```

- [ ] **Step 2: Add the terminal block CSS**

The case study uses a styled `<pre>` block to simulate a git terminal. Add this after the existing CSS, before `</style>`:

```css
  /* ── TERMINAL BLOCK ── */
  .terminal {
    background: #0d0d14;
    border: 1px solid #2a2a3a;
    border-left: 3px solid var(--accent3);
    padding: 1.5rem 1.75rem;
    font-family: 'DM Mono', monospace;
    font-size: 0.8rem;
    line-height: 1.7;
    color: #c8c8d8;
    overflow-x: auto;
    margin: 2rem 0;
    white-space: pre;
  }

  .terminal .t-cmd  { color: var(--accent3); }
  .terminal .t-sha  { color: var(--accent2); }
  .terminal .t-date { color: var(--muted); }
  .terminal .t-auth { color: var(--accent); }
  .terminal .t-msg  { color: var(--text); font-weight: 600; }
  .terminal .t-add  { color: #47e8a0; }
  .terminal .t-cmt  { color: var(--muted); font-style: italic; }

  [data-theme="light"] .terminal {
    background: #f0efe9;
    border-color: #d8d5ce;
    border-left-color: var(--accent3);
    color: #2a2a38;
  }
```

- [ ] **Step 3: Open file in browser — verify blank page loads with no console errors**

Open: `\\wsl$\Ubuntu\home\eslavag\Development\github\razor\chesterton-fence.html`
Expected: blank page, no errors in DevTools console.

- [ ] **Step 4: Commit**

```bash
git add chesterton-fence.html
git commit -m "feat: scaffold chesterton-fence.html with full CSS"
```

---

### Task 2: Fixed UI chrome and hero section

**Files:**
- Modify: `chesterton-fence.html`

- [ ] **Step 1: Add home button, theme toggle, back-to-top button**

Place these immediately after `<body>`:

```html
<a id="home-btn" href="index.html" aria-label="Home">⌂</a>

<button id="theme-toggle" aria-label="Toggle theme">
  <span id="theme-icon">☀️</span>
</button>

<button id="back-to-top" aria-label="Back to top" onclick="window.scrollTo({top:0,behavior:'smooth'})">↑</button>
```

- [ ] **Step 2: Add the hero section**

```html
<header class="hero">
  <div class="hero-incident">An AI cleaned up the codebase on a Tuesday.<br>By Thursday, 3% of payment transactions were silently failing.</div>
  <p class="hero-eyebrow">Mental Model 03 · Software Engineering with AI</p>
  <h1 class="hero-title">Chesterton's<br><em>Fence</em></h1>
  <p class="hero-subtitle">Never remove what you don't understand. The code you can't explain is the code most likely to hurt you.</p>
  <nav class="hero-nav">
    <a class="nav-pill" href="#what">What it is</a>
    <a class="nav-pill" href="#principles">5 Principles</a>
    <a class="nav-pill" href="#archaeology">The Protocol</a>
    <a class="nav-pill" href="#anti">Anti-Patterns</a>
    <a class="nav-pill" href="#case">Case Study</a>
    <a class="nav-pill" href="#quiz">Quiz</a>
    <a class="nav-pill" href="#cheatsheet">Cheatsheet</a>
  </nav>
  <div class="scroll-hint">
    <span class="scroll-line"></span>
    <span class="scroll-text">scroll</span>
  </div>
</header>
```

- [ ] **Step 3: Add the hero-incident CSS**

Add after the existing `.hero-subtitle` styles in the CSS:

```css
  .hero-incident {
    font-family: 'DM Mono', monospace;
    font-size: 0.85rem;
    color: var(--danger);
    line-height: 1.6;
    margin-bottom: 2.5rem;
    padding: 1rem 1.25rem;
    border-left: 2px solid var(--danger);
    opacity: 0;
    animation: fadeUp 0.8s 0.1s forwards;
  }
```

- [ ] **Step 4: Verify in browser**

Expected:
- Dark background with noise texture
- Red incident teaser at top of hero
- Title "Chesterton's Fence" with italic gold "Fence"
- Nav pills row visible
- Home button (top-left), theme toggle (top-right)
- Light mode toggle works and persists on reload

- [ ] **Step 5: Commit**

```bash
git add chesterton-fence.html
git commit -m "feat: add hero section with incident teaser to chesterton-fence"
```

---

## Chunk 2: Foundation and Principles

### Task 3: Section 01 — Foundation

**Files:**
- Modify: `chesterton-fence.html`

Add after `</header>`:

- [ ] **Step 1: Add the foundation section**

```html
<main>

<section id="what">
  <div class="section-label">01 / Foundation</div>
  <h2 class="section-title">What is<br>Chesterton's Fence?</h2>
  <p class="section-body">G.K. Chesterton's principle is simple: do not remove a fence until you understand why it was put up. In software, every constraint, guard, workaround, and "unnecessary" check is a fence. Some are genuinely obsolete. Most are not.</p>

  <div class="definition-block">
    <p>If you don't see the use of it, I certainly won't let you clear it away. Go away and think. Then, when you can come back and tell me that you do see the use of it, I may allow you to destroy it.</p>
    <cite>— G.K. Chesterton, <em>The Thing</em>, 1929</cite>
  </div>

  <br><br>
  <p class="section-body">The fence exists because something happened. A bug, an outage, a security incident, a race condition in a third-party SDK. You weren't there. The code was. Every <code style="font-family:'DM Mono',monospace;color:var(--accent3);font-size:0.9em">sleep(500)</code>, every <code style="font-family:'DM Mono',monospace;color:var(--accent3);font-size:0.9em">|| []</code>, every <code style="font-family:'DM Mono',monospace;color:var(--accent3);font-size:0.9em">try/catch</code> that "never fires" was written by someone who had a reason.</p>
  <br>
  <p class="section-body">With AI tools, this matters <strong style="color:var(--text)">more than ever</strong> — because AI sees code, not history. It has no access to the incident postmortem, the Slack thread, the three-year-old PR that explains the guard nobody questions anymore. When AI refactors confidently, it is working from syntax alone. The fence looks like clutter. The cattle are invisible.</p>
</section>

<hr class="divider">
```

- [ ] **Step 2: Verify in browser**

Expected: Foundation section renders below hero with definition block styled correctly.

- [ ] **Step 3: Commit**

```bash
git add chesterton-fence.html
git commit -m "feat: add foundation section to chesterton-fence"
```

---

### Task 4: Section 02 — 5 Principles

**Files:**
- Modify: `chesterton-fence.html`

- [ ] **Step 1: Add principles section**

```html
<section id="principles">
  <div class="section-label">02 / Core Framework</div>
  <h2 class="section-title">5 Principles<br>of the Fence</h2>
  <p class="section-body">Click each principle to expand it with software engineering examples and how AI fits in.</p>

  <div class="principles-grid" id="principlesGrid">

    <div class="principle-card" onclick="togglePrinciple(this)">
      <div class="principle-number">PRINCIPLE 01</div>
      <div class="principle-name">Never Remove What You Can't Explain</div>
      <div class="principle-tagline">If you can't state why it's safe to delete, you're not done investigating.</div>
      <div class="principle-expand">
        <p>The inability to explain a piece of code is not evidence that it's useless — it's evidence that your investigation is incomplete. Before removing anything, you need a complete answer to: what does this do, when does it run, and what would break without it? "It looks unused" is not an explanation. "It only runs on the error path that our happy-path tests never exercise" is.</p>
        <div class="example-box">
          <div class="ex-label">Software Example</div>
          <p>A <code style="font-family:'DM Mono',monospace">finally</code> block that releases a database connection looks redundant when the <code style="font-family:'DM Mono',monospace">try</code> block already has cleanup logic. Remove it, and you've created a connection leak that only surfaces under load — exactly when you can least afford it.</p>
        </div>
        <div class="example-box" style="border-left-color: var(--accent3); margin-top: 0.75rem;">
          <div class="ex-label" style="color: var(--accent3);">AI Application</div>
          <p>Before asking AI to clean up code: "Before proposing any removals, explain what each piece you want to remove does, when it executes, and what you believe happens if it's absent. I will verify your explanation against the codebase history before approving any deletion."</p>
        </div>
      </div>
    </div>

    <div class="principle-card" onclick="togglePrinciple(this)">
      <div class="principle-number">PRINCIPLE 02</div>
      <div class="principle-name">"Weird" Code Is Usually Defensive Code</div>
      <div class="principle-tagline">Counterintuitive guards are the ones most likely to be load-bearing.</div>
      <div class="principle-expand">
        <p>Code that looks wrong is rarely the result of incompetence. Experienced engineers write "weird" code when the straightforward approach has already failed in production. The magic number, the unexpected type coercion, the seemingly redundant null check — these are scars. They encode the memory of failures that the codebase has survived so that you don't have to survive them again.</p>
        <div class="example-box">
          <div class="ex-label">Software Example</div>
          <p>An API handler that checks <code style="font-family:'DM Mono',monospace">if (userId !== undefined && userId !== null && userId !== '')</code> instead of just <code style="font-family:'DM Mono',monospace">if (userId)</code> is defensive — likely because some client was sending empty string userIds and causing downstream corruption. The verbose check is the fence.</p>
        </div>
        <div class="example-box" style="border-left-color: var(--accent3); margin-top: 0.75rem;">
          <div class="ex-label" style="color: var(--accent3);">AI Application</div>
          <p>When AI calls something "redundant" or "overly verbose": "This pattern may be intentionally defensive. Before simplifying it, check git history for commits touching this line. Is there an incident or bug report that explains why the naive version was rejected?"</p>
        </div>
      </div>
    </div>

    <div class="principle-card" onclick="togglePrinciple(this)">
      <div class="principle-number">PRINCIPLE 03</div>
      <div class="principle-name">The History Is Part of the Code</div>
      <div class="principle-tagline">git blame, commit messages, and PR descriptions are primary sources — not optional reading.</div>
      <div class="principle-expand">
        <p>Source control is not just version storage — it is the institutional memory of every decision the codebase has ever made. A file without its history is a fence without its sign. Reading code in isolation, without reading why it was written, is archaeological fieldwork without stratigraphy. You're picking up artifacts with no idea which layer they came from or what they were doing there.</p>
        <div class="example-box">
          <div class="ex-label">Software Example</div>
          <p><code style="font-family:'DM Mono',monospace">git log -p -- src/payments/processor.js</code> takes 30 seconds. The commit three years ago that added the <code style="font-family:'DM Mono',monospace">sleep(500)</code> call says: "fix: compensate for SDK race condition — JIRA-4821." That's your answer. The code's history is the documentation you needed.</p>
        </div>
        <div class="example-box" style="border-left-color: var(--accent3); margin-top: 0.75rem;">
          <div class="ex-label" style="color: var(--accent3);">AI Application</div>
          <p>Paste relevant git history into your prompt: "Here is the commit history for this file: [paste]. Given this history, what is the purpose of [specific code]? What risk does removing it introduce?" AI reasons much better when you provide the institutional memory it can't access.</p>
        </div>
      </div>
    </div>

    <div class="principle-card" onclick="togglePrinciple(this)">
      <div class="principle-number">PRINCIPLE 04</div>
      <div class="principle-name">AI Sees the Fence, Not the Cattle</div>
      <div class="principle-tagline">AI has no institutional memory — it cannot know what the code was defending against.</div>
      <div class="principle-expand">
        <p>Large language models are trained on syntax, not history. They see the current state of your code — not the three production incidents that shaped it. When AI confidently labels something "dead code" or "unnecessary complexity," it is making a structural observation without context. This is not a flaw; it is a fundamental limitation. AI is an extraordinarily capable reader of what the fence looks like. It cannot know why the fence was built.</p>
        <div class="example-box">
          <div class="ex-label">Software Example</div>
          <p>A feature flag that appears never set to <code style="font-family:'DM Mono',monospace">true</code> in the codebase might be a killswitch that ops toggles at the infrastructure level during incidents. AI sees dead code. Ops sees a circuit breaker. Removing it silently eliminates an incident response tool nobody wrote down.</p>
        </div>
        <div class="example-box" style="border-left-color: var(--accent3); margin-top: 0.75rem;">
          <div class="ex-label" style="color: var(--accent3);">AI Application</div>
          <p>Treat AI's "safe to remove" conclusions as hypotheses, not verdicts. AI is identifying candidates for investigation — not authorizing deletion. Your job is to provide the context AI can't see, then ask again: "Given this incident history and these operational constraints, is it still safe to remove?"</p>
        </div>
      </div>
    </div>

    <div class="principle-card" onclick="togglePrinciple(this)">
      <div class="principle-number">PRINCIPLE 05</div>
      <div class="principle-name">The Burden of Proof Is on Removal</div>
      <div class="principle-tagline">Keeping costs nothing. Removing requires a complete explanation.</div>
      <div class="principle-expand">
        <p>In most contexts, we assume that doing something requires justification and doing nothing does not. For code removal, invert this. Keeping code that might be needed costs almost nothing — a few lines in a file, no runtime overhead if it's on a dead path. Removing code that was needed costs an outage, a debugging session, and a post-mortem. Given asymmetric costs, the burden of proof belongs on the side of removal. "I think it's probably fine" is not sufficient justification.</p>
        <div class="example-box">
          <div class="ex-label">Software Example</div>
          <p>A data migration script from 2019 has run once and will never run again. It's safe to remove — you can answer exactly why: it ran on this date, the migration is complete, and re-running it would be a no-op due to the idempotency check on line 12. That's the standard. That's what "safe to remove" looks like.</p>
        </div>
        <div class="example-box" style="border-left-color: var(--accent3); margin-top: 0.75rem;">
          <div class="ex-label" style="color: var(--accent3);">AI Application</div>
          <p>Before accepting any AI-proposed deletion: "Write a one-paragraph removal justification for each thing you want to delete. It must include: what the code did, when it ran, why it was originally added, and why it is now verifiably safe to remove. If you can't write this paragraph, we keep it."</p>
        </div>
      </div>
    </div>

  </div>
</section>

<hr class="divider">
```

- [ ] **Step 2: Verify in browser**

Expected:
- 5 principle cards render in grid
- Clicking each card expands it (only one open at a time)
- Example boxes and AI application boxes styled correctly

- [ ] **Step 3: Commit**

```bash
git add chesterton-fence.html
git commit -m "feat: add 5 principles section to chesterton-fence"
```

---

## Chunk 3: Archaeology Protocol and Anti-Patterns

### Task 5: Section 03 — The Archaeology Protocol

**Files:**
- Modify: `chesterton-fence.html`

- [ ] **Step 1: Add archaeology workflow section**

```html
<section id="archaeology">
  <div class="section-label">03 / Practical Method</div>
  <h2 class="section-title">The Archaeology<br>Protocol</h2>
  <p class="section-body">A two-phase method: investigate before you touch, then prompt with the context AI can't see. Never skip Phase 1.</p>

  <div style="font-family:'DM Mono',monospace;font-size:0.7rem;letter-spacing:0.2em;text-transform:uppercase;color:var(--accent);margin-bottom:1.5rem;">Phase 1 — Investigate</div>

  <div class="workflow">

    <div class="workflow-step">
      <div class="step-marker">
        <span class="step-num">STEP 01</span>
        <span class="step-icon">🪨</span>
      </div>
      <div class="step-content">
        <div class="step-title">Read the Stratigraphy</div>
        <p class="step-desc">Run <code style="font-family:'DM Mono',monospace;color:var(--accent3)">git log -p -- &lt;file&gt;</code> and read every commit that has ever touched this code. Pay attention to commit messages, dates, and author names. A three-year-old commit with a message like "fix: compensate for SDK bug" is the most important line in the file.</p>
        <div class="prompt-block">
git log -p --follow -- <span class="var">&lt;path/to/file&gt;</span>
git blame <span class="var">&lt;path/to/file&gt;</span>
git log --all --grep="<span class="var">&lt;function or variable name&gt;</span>"</div>
      </div>
    </div>

    <div class="workflow-step">
      <div class="step-marker">
        <span class="step-num">STEP 02</span>
        <span class="step-icon">🔍</span>
      </div>
      <div class="step-content">
        <div class="step-title">Find the Incident Layer</div>
        <p class="step-desc">Search commit history, PR descriptions, and linked tickets for the code's fingerprint. Look for incident IDs, bug numbers, and phrases like "fix:", "hotfix:", "compensate for", "workaround". The PR that introduced the fence often explains exactly what it's protecting against.</p>
        <div class="prompt-block">
git log --all --grep="<span class="var">&lt;JIRA-ID or keyword&gt;</span>" --oneline
git log --all -S "<span class="var">&lt;function name or string&gt;</span>" --oneline</div>
      </div>
    </div>

    <div class="workflow-step">
      <div class="step-marker">
        <span class="step-num">STEP 03</span>
        <span class="step-icon">🤖</span>
      </div>
      <div class="step-content">
        <div class="step-title">Ask AI to Explain, Not Change</div>
        <p class="step-desc">Before proposing any edits, ask AI to describe what the code does and why it might exist — as a hypothesis. This forces a reasoning step before action, and often surfaces the explanation you were looking for.</p>
        <div class="prompt-block">
"Here is a piece of code I'm unfamiliar with:<br>
<span class="var">[paste code]</span><br><br>
Do not suggest changes yet.<br>
First: explain what this code does, when it runs, and<br>
what you hypothesize it was written to protect against.<br>
List any patterns that suggest it is defensive code."</div>
      </div>
    </div>

  </div>

  <div style="font-family:'DM Mono',monospace;font-size:0.7rem;letter-spacing:0.2em;text-transform:uppercase;color:var(--accent2);margin:2.5rem 0 1.5rem;">Phase 2 — Prompt with Context Loaded</div>

  <div class="workflow">

    <div class="workflow-step">
      <div class="step-marker">
        <span class="step-num">STEP 04</span>
        <span class="step-icon">📜</span>
      </div>
      <div class="step-content">
        <div class="step-title">Load the Archaeology</div>
        <p class="step-desc">Share what you found: the commit message, the PR description, the linked incident. Give AI the institutional memory it can't access on its own. An AI with context is categorically different from an AI without it.</p>
        <div class="prompt-block">
"Here is the git history for this file:<br>
<span class="var">[paste relevant commits and messages]</span><br><br>
Here is the PR description that introduced this code:<br>
<span class="var">[paste PR description]</span><br><br>
Given this context, re-evaluate whether the code<br>
I originally flagged is safe to remove."</div>
      </div>
    </div>

    <div class="workflow-step">
      <div class="step-marker">
        <span class="step-num">STEP 05</span>
        <span class="step-icon">⚖️</span>
      </div>
      <div class="step-content">
        <div class="step-title">Constrain the Removal</div>
        <p class="step-desc">If removal is still warranted, require AI to produce a removal justification for every fence it wants to take down. The justification must state what the code did, why it's now safe to remove, and what would need to change to make removal dangerous again.</p>
        <div class="prompt-block">
"For each piece of code you propose removing,<br>
write a removal justification that includes:<br>
1. What this code does<br>
2. When it runs<br>
3. Why it was originally added<br>
4. Why it is now verifiably safe to remove<br>
5. What would need to change to make removal risky again<br><br>
If you cannot write this justification, keep the code."</div>
      </div>
    </div>

  </div>
</section>

<hr class="divider">
```

- [ ] **Step 2: Verify in browser**

Expected:
- Phase 1 and Phase 2 labels render correctly
- 5 workflow steps with prompt blocks
- Prompt blocks use monospace styling and `var` highlighted spans

- [ ] **Step 3: Commit**

```bash
git add chesterton-fence.html
git commit -m "feat: add archaeology protocol section to chesterton-fence"
```

---

### Task 6: Section 04 — Anti-Patterns

**Files:**
- Modify: `chesterton-fence.html`

- [ ] **Step 1: Add anti-patterns comparison table**

```html
<section id="anti">
  <div class="section-label">04 / What Not to Do</div>
  <h2 class="section-title">How Engineers<br>Violate the Fence</h2>
  <p class="section-body">These are the reasoning shortcuts that turn "cleanup" into outages.</p>

  <div class="comparison">
    <div class="comp-header">
      <span class="comp-wrong">❌ The Violation</span>
      <span class="comp-right">✓ The Protocol</span>
    </div>
    <div class="comp-row">
      <div class="comp-wrong">"This looks unused"</div>
      <div class="comp-right">Trace all call sites — including dynamic invocations, config-driven paths, and runtime-generated references — before concluding anything is dead.</div>
    </div>
    <div class="comp-row">
      <div class="comp-wrong">"AI said it's safe to remove"</div>
      <div class="comp-right">AI doesn't know your incident history. That's your job to supply. AI's verdict without your context is a hypothesis, not a fact.</div>
    </div>
    <div class="comp-row">
      <div class="comp-wrong">"The code is old, therefore bad"</div>
      <div class="comp-right">Age is not evidence of obsolescence. Old fences often guard old wounds. A three-year-old workaround might be protecting against a three-year-old vendor bug with no fix.</div>
    </div>
    <div class="comp-row">
      <div class="comp-wrong">"It has no tests, so it must be dead"</div>
      <div class="comp-right">Critical defensive code is often untested precisely because the failure mode it prevents is hard to reproduce in a test environment. No test coverage ≠ not running.</div>
    </div>
    <div class="comp-row">
      <div class="comp-wrong">"I don't understand it, so I'll delete it"</div>
      <div class="comp-right">Not understanding it is the reason to investigate, not the reason to remove. Ignorance is the starting point of the protocol, not the justification for skipping it.</div>
    </div>
    <div class="comp-row">
      <div class="comp-wrong">"It's a cleanup sprint — no risk"</div>
      <div class="comp-right">Cleanup sprints are where Chesterton's Fence violations cluster. The intent is low risk; the execution is often the opposite. Apply the full protocol regardless of sprint framing.</div>
    </div>
  </div>
</section>

<hr class="divider">
```

- [ ] **Step 2: Verify in browser**

Expected: Comparison table renders with red "violation" column and green "protocol" column. Rows have consistent spacing.

- [ ] **Step 3: Commit**

```bash
git add chesterton-fence.html
git commit -m "feat: add anti-patterns section to chesterton-fence"
```

---

## Chunk 4: Case Study, Quiz, Cheatsheet

### Task 7: Section 05 — Case Study

**Files:**
- Modify: `chesterton-fence.html`

- [ ] **Step 1: Add case study section**

```html
<section id="case">
  <div class="section-label">05 / Worked Example</div>
  <h2 class="section-title">The 500ms That<br>Brought Down Payments</h2>
  <p class="section-body">A real class of failure. The names and numbers are illustrative.</p>

  <div class="case-study">

    <div class="decomp-item">
      <div class="decomp-label">The Scene</div>
      <div class="decomp-content">A backend payments service has been stable for three years. A senior engineer kicks off a "tech debt cleanup" sprint. They use an AI coding assistant to scan the codebase for dead code, unnecessary delays, and unused variables.</div>
    </div>

    <div class="decomp-item">
      <div class="decomp-label">The Fence</div>
      <div class="decomp-content">The AI flags this line in <code style="font-family:'DM Mono',monospace;color:var(--accent3)">payment/processor.js</code>:
      <br><br>
      <code style="font-family:'DM Mono',monospace;font-size:0.9em;color:var(--accent3);background:rgba(71,197,232,0.08);padding:0.4rem 0.75rem;display:inline-block;border-radius:4px;">await sleep(500); // ???</code>
      <br><br>
      No comment. No test. No obvious caller. The AI reports: <em>"This appears to be an unnecessary artificial delay. Safe to remove."</em> The engineer reviews the PR, agrees, and merges.</div>
    </div>

    <div class="decomp-item">
      <div class="decomp-label">What the History Said</div>
      <div class="decomp-content">
        Running the Archaeology Protocol would have taken 30 seconds:
      </div>
    </div>

  </div>

  <pre class="terminal"><span class="t-cmd">$ git log -p --follow -- payment/processor.js | grep -B2 -A8 "sleep"</span>

<span class="t-sha">commit a3f9c2d</span>  <span class="t-date">(3 years, 4 months ago)</span>  <span class="t-auth">marcus.chen@company.com</span>
<span class="t-msg">"fix: add delay before processor.init() call"</span>

<span class="t-add">+  await sleep(500);</span>  <span class="t-cmt">// SDK fires PAYMENT_READY before internal</span>
                      <span class="t-cmt">// state is actually ready. Race condition.</span>
                      <span class="t-cmt">// Filed with vendor: GH-2847. No fix yet.</span>
                      <span class="t-cmt">// Revisit when SDK >= 4.0 ships.</span></pre>

  <div class="case-study">

    <div class="decomp-item">
      <div class="decomp-label">What Happened</div>
      <div class="decomp-content">Without the delay, approximately 3% of payment transactions attempted to charge before the SDK's internal token cache finished warming. The SDK returned no error — it silently accepted the call and failed downstream. The failure only surfaced under load. Detection took six hours. Three days of transactions required manual reconciliation.</div>
    </div>

    <div class="decomp-item">
      <div class="decomp-label">The Resolution</div>
      <div class="decomp-content">The sleep was restored. The comment was rewritten to include the vendor ticket number, the SDK version when the fix would land, and a note explaining the race condition in detail. A test was written that mocked the SDK's async initialization to detect the race. The archaeology was baked into the code so the next engineer would not need to excavate it.</div>
    </div>

    <div class="decomp-item">
      <div class="decomp-label">The Lesson</div>
      <div class="decomp-content">The AI made a structurally correct observation — the sleep had no comment, no test, and looked like a debug artifact. It had no way to know it was a production-critical compensation for a vendor race condition. That context existed exclusively in git history. The 30-second archaeology would have found it. The cleanup sprint didn't run the protocol.</div>
    </div>

  </div>
</section>

<hr class="divider">
```

- [ ] **Step 2: Verify in browser**

Expected:
- Case study blocks render with label/content layout
- Terminal block shows syntax-highlighted git output in monospace
- Light mode: terminal has light background with correct colors

- [ ] **Step 3: Commit**

```bash
git add chesterton-fence.html
git commit -m "feat: add case study section to chesterton-fence"
```

---

### Task 8: Section 06 — Quiz

**Files:**
- Modify: `chesterton-fence.html`

- [ ] **Step 1: Add quiz section**

```html
<section id="quiz">
  <div class="section-label">06 / Test Yourself</div>
  <h2 class="section-title">Apply the<br>Fence</h2>
  <p class="section-body">Three scenarios. Apply Chesterton's Fence and see if your instinct aligns with the principle.</p>

  <div class="quiz-container">

    <div class="quiz-card">
      <div class="quiz-q">AI proposes removing a <code style="font-family:'DM Mono',monospace">try/catch</code> block that "never triggers in tests and appears to be boilerplate." What should you do first?</div>
      <div class="quiz-options">
        <button class="quiz-option" data-letter="A" onclick="answer(this, false)">Accept the change — if it never triggers, it's clearly unnecessary overhead</button>
        <button class="quiz-option" data-letter="B" onclick="answer(this, false)">Ask AI to rewrite it more cleanly before removing it</button>
        <button class="quiz-option" data-letter="C" onclick="answer(this, true)">Run git log on the file and find the commit that added this catch block — read why it was added before touching it</button>
        <button class="quiz-option" data-letter="D" onclick="answer(this, false)">Add a test that intentionally triggers it to verify it's reachable, then decide</button>
      </div>
      <div class="quiz-feedback">
        <strong class="feedback-label"></strong> "Never triggers in tests" means nothing — your tests may not exercise the error path. The archaeological reflex is correct: read the history first. The commit that added the catch block will tell you what exception it was handling and whether that condition still exists. C is the protocol. D is reasonable but secondary.
      </div>
    </div>

    <div class="quiz-card">
      <div class="quiz-q">A <code style="font-family:'DM Mono',monospace">|| []</code> default value appears in a four-year-old utility function with no comment. Your colleague says it's redundant because the function is always called with a valid array. Safe to remove?</div>
      <div class="quiz-options">
        <button class="quiz-option" data-letter="A" onclick="answer(this, false)">Yes — if all current callers pass valid arrays, the default is dead code</button>
        <button class="quiz-option" data-letter="B" onclick="answer(this, false)">Yes — the function should rely on its callers to pass valid input</button>
        <button class="quiz-option" data-letter="C" onclick="answer(this, true)">Not yet — find out what was returning null or undefined before the default was added, and confirm that condition is no longer possible</button>
        <button class="quiz-option" data-letter="D" onclick="answer(this, false)">Replace it with a runtime assertion that throws if the value is missing</button>
      </div>
      <div class="quiz-feedback">
        <strong class="feedback-label"></strong> "All current callers pass valid arrays" is a claim about today. The <code style="font-family:'DM Mono',monospace">|| []</code> was added because something was passing a non-array value four years ago. Until you know what was causing that and can confirm it's gone, you don't know if you've closed the gap or just hidden it. C is the protocol.
      </div>
    </div>

    <div class="quiz-card">
      <div class="quiz-q">Which of these is the strongest justification for removing an unfamiliar piece of code?</div>
      <div class="quiz-options">
        <button class="quiz-option" data-letter="A" onclick="answer(this, false)">AI confirmed it's unreachable based on static analysis</button>
        <button class="quiz-option" data-letter="B" onclick="answer(this, false)">The code has existed for 5 years with no associated tests</button>
        <button class="quiz-option" data-letter="C" onclick="answer(this, false)">No team member can remember why it was written</button>
        <button class="quiz-option" data-letter="D" onclick="answer(this, true)">You can explain exactly what it defends against, have confirmed that condition is no longer possible, and have a test that would catch a regression if you're wrong</button>
      </div>
      <div class="quiz-feedback">
        <strong class="feedback-label"></strong> The other options are reasons to investigate more, not reasons to delete. A: static analysis misses dynamic call paths. B: age and test coverage are independent. C: nobody remembering is the reason to dig, not to remove. D is the complete justification: you understand the fence, you've verified the cattle are gone, and you've set a tripwire for if they come back.
      </div>
    </div>

  </div>
</section>

<hr class="divider">
```

- [ ] **Step 2: Verify in browser**

Expected:
- 3 quiz cards render correctly
- Clicking correct answer highlights green, shows feedback
- Clicking wrong answer highlights red, reveals correct answer in green

- [ ] **Step 3: Commit**

```bash
git add chesterton-fence.html
git commit -m "feat: add quiz section to chesterton-fence"
```

---

### Task 9: Section 07 — Cheatsheet and Footer

**Files:**
- Modify: `chesterton-fence.html`

- [ ] **Step 1: Add cheatsheet and footer**

```html
<section id="cheatsheet">
  <div class="section-label">07 / Quick Reference</div>
  <h2 class="section-title">The Fence<br>Cheatsheet</h2>
  <p class="section-body">Keep these close when reviewing, refactoring, or working with AI on unfamiliar code.</p>

  <div class="cheatsheet">
    <div class="cs-item">
      <div class="cs-icon">🪨</div>
      <div class="cs-title">The Rule</div>
      <ul class="cs-list">
        <li>Never remove what you can't explain</li>
        <li>Keeping costs nothing; removing requires justification</li>
        <li>"I don't understand it" means investigate, not delete</li>
        <li>Weird code is usually defensive code</li>
      </ul>
    </div>
    <div class="cs-item">
      <div class="cs-icon">🔎</div>
      <div class="cs-title">Investigation Commands</div>
      <ul class="cs-list">
        <li><code style="font-family:'DM Mono',monospace;font-size:0.85em">git log -p -- &lt;file&gt;</code></li>
        <li><code style="font-family:'DM Mono',monospace;font-size:0.85em">git blame &lt;file&gt;</code></li>
        <li><code style="font-family:'DM Mono',monospace;font-size:0.85em">git log --all -S "&lt;term&gt;"</code></li>
        <li><code style="font-family:'DM Mono',monospace;font-size:0.85em">git log --grep="&lt;keyword&gt;"</code></li>
      </ul>
    </div>
    <div class="cs-item">
      <div class="cs-icon">✅</div>
      <div class="cs-title">Pre-Removal Checklist</div>
      <ul class="cs-list">
        <li>Read the full git history for this file</li>
        <li>Found the commit that introduced this code</li>
        <li>Understand what condition it was written to handle</li>
        <li>Confirmed that condition is no longer possible</li>
        <li>Have a test that would catch a regression</li>
      </ul>
    </div>
    <div class="cs-item">
      <div class="cs-icon">🚩</div>
      <div class="cs-title">AI Danger Zones</div>
      <ul class="cs-list">
        <li>"This appears to be dead code"</li>
        <li>"This delay seems unnecessary"</li>
        <li>"This check is redundant"</li>
        <li>"Safe to remove"</li>
        <li>"This is legacy code with no purpose"</li>
      </ul>
    </div>
    <div class="cs-item">
      <div class="cs-icon">⚖️</div>
      <div class="cs-title">The Removal Test</div>
      <ul class="cs-list">
        <li>What does this code defend against?</li>
        <li>Is that condition still possible?</li>
        <li>What breaks if I'm wrong?</li>
        <li>How quickly would I detect the regression?</li>
        <li>If I can't answer all four — keep it</li>
      </ul>
    </div>
    <div class="cs-item">
      <div class="cs-icon">🤖</div>
      <div class="cs-title">The Archaeology Prompt</div>
      <ul class="cs-list">
        <li>"Do not change anything yet"</li>
        <li>"Explain what this code does and why it might exist"</li>
        <li>"Here is the commit history: [paste]"</li>
        <li>"Write a removal justification or conclude we keep it"</li>
      </ul>
    </div>
  </div>
</section>

</main>

<footer>
  <span>Chesterton's Fence · Software Engineering with AI</span>
  <span>A mental model series</span>
</footer>
```

- [ ] **Step 2: Verify in browser**

Expected: 6-cell cheatsheet grid, footer at bottom. All 7 sections now visible end-to-end.

- [ ] **Step 3: Commit**

```bash
git add chesterton-fence.html
git commit -m "feat: add cheatsheet and footer to chesterton-fence"
```

---

## Chunk 5: JavaScript and Index Update

### Task 10: Embedded JavaScript

**Files:**
- Modify: `chesterton-fence.html`

- [ ] **Step 1: Add the full script block before `</body>`**

```html
<script>
  // ── BACK TO TOP ──
  const backToTop = document.getElementById('back-to-top');
  window.addEventListener('scroll', () => {
    backToTop.classList.toggle('visible', window.scrollY > 300);
  }, { passive: true });

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
    if (!correct) {
      card.querySelectorAll('.quiz-option').forEach(b => {
        if (b.getAttribute('onclick').includes('true')) b.classList.add('correct');
      });
    }
    feedback.querySelector('.feedback-label').textContent = correct ? 'Correct.' : 'The right answer:';
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

- [ ] **Step 2: Verify all JS features in browser**

Check each item:
- [ ] Theme toggle switches dark/light and persists across page reload
- [ ] Principle cards expand/collapse (only one open at a time)
- [ ] Quiz answers register correct/wrong, reveal feedback, lock after first click
- [ ] Back-to-top button appears after scrolling 300px
- [ ] Scroll animations fire as sections enter viewport

- [ ] **Step 3: Commit**

```bash
git add chesterton-fence.html
git commit -m "feat: add JS interactions to chesterton-fence"
```

---

### Task 11: Update index.html

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Convert the Chesterton's Fence card from coming-soon to live**

In `index.html`, find:

```html
    <div class="topic-card coming-soon fade-in">
      <span class="card-number">Model 03</span>
      <h2 class="card-title">Chesterton's<br><em>Fence</em></h2>
      <p class="card-desc">Never remove something without understanding why it was put there. The code you don't understand is the code most likely to hurt you.</p>
      <span class="card-tag">Coming soon</span>
    </div>
```

Replace with:

```html
    <a class="topic-card fade-in" href="chesterton-fence.html">
      <span class="card-number">Model 03</span>
      <h2 class="card-title">Chesterton's<br><em>Fence</em></h2>
      <p class="card-desc">Never remove something without understanding why it was put there. The code you don't understand is the code most likely to hurt you.</p>
      <span class="card-tag">Archaeology</span>
    </a>
```

- [ ] **Step 2: Verify in browser**

Open `index.html`. Expected:
- Model 03 card is now clickable (no longer dimmed/dashed)
- Card tag reads "Archaeology" instead of "Coming soon"
- Counter shows "3 of 6 published"
- Clicking the card navigates to `chesterton-fence.html`

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: link chesterton-fence.html from index — Model 03 live"
```

---

## Final Checklist

Before declaring done, verify the full page in both themes:

- [ ] Hero incident teaser renders in red with border-left
- [ ] All 7 nav pills scroll to correct sections
- [ ] All 5 principle cards expand and collapse correctly
- [ ] All 5 workflow steps render with prompt blocks
- [ ] Comparison table alternates row styling correctly
- [ ] Terminal block renders with syntax highlighting in both dark and light mode
- [ ] All 3 quiz questions work correctly
- [ ] Cheatsheet 6-cell grid renders without overflow
- [ ] Home button returns to index.html
- [ ] Back-to-top appears on scroll, scrolls to top on click
- [ ] Theme toggle works and persists
- [ ] No console errors in DevTools
