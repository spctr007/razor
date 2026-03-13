# Design: chesterton-fence.html

**Date:** 2026-03-13
**Series position:** Model 03
**File:** `chesterton-fence.html`
**Page identity:** Code Archaeology — investigation before intervention

---

## Hero

Opens with a 2-sentence teaser of the case study incident:

> "An AI cleaned up the codebase on a Tuesday. By Thursday, 3% of payment transactions were silently failing."

Then pulls back to define the principle. Title: *Chesterton's* / *Fence* (italic accent on "Fence"). Nav pills link to all 7 sections.

---

## Page Structure

| # | Label | Title |
|---|-------|-------|
| 01 | Foundation | What is Chesterton's Fence? |
| 02 | Core Framework | 5 Principles of the Fence |
| 03 | Archaeology Protocol | Investigate, Then Prompt |
| 04 | Anti-Patterns | How Engineers Violate the Fence |
| 05 | Case Study | The 500ms That Brought Down Payments |
| 06 | Quiz | Test Your Instincts |
| 07 | Cheatsheet | Quick Reference |

---

## 01 / Foundation — What is Chesterton's Fence?

Definition block quotes G.K. Chesterton:
> *"Do not remove a fence until you know why it was put up."*

Software translation: every constraint, guard, workaround, and "unnecessary" check in a codebase is a fence. Some are genuinely obsolete. Most are not. The fence exists because something happened — a bug, an outage, a security incident, a quirk in a dependency. You weren't there. The code was.

AI-specific angle: AI sees code, not history. It has no access to the incident postmortem, the Slack thread, the three-year-old PR. When AI refactors confidently, it is working from syntax alone. The fence looks like clutter. The cattle are invisible.

---

## 02 / Core Framework — 5 Principles

Expandable cards, each with a software example and AI application prompt.

| # | Name | Tagline |
|---|------|---------|
| 01 | Never remove what you can't explain | If you can't state why it's safe to delete, you're not done investigating |
| 02 | "Weird" code is usually defensive code | Counterintuitive guards are the ones most likely to be load-bearing |
| 03 | The history is part of the code | git blame, commit messages, and PR descriptions are primary sources |
| 04 | AI sees the fence, not the cattle | AI has no institutional memory — it cannot know what the code was defending against |
| 05 | The burden of proof is on removal | Keeping costs nothing. Removing requires a complete explanation |

---

## 03 / Archaeology Protocol — Investigate, Then Prompt

Two-phase workflow with copy-paste prompt templates for each step.

### Phase 1: Investigate (before AI touches anything)

| Step | Title | Action |
|------|-------|--------|
| 01 | Read the stratigraphy | `git log -p -- <file>` — read every commit that touched this code |
| 02 | Find the incident layer | Search commits, PRs, and tickets for the code's fingerprint |
| 03 | Ask AI to explain, not change | Prompt AI to describe what the code does and *why it might exist* before proposing edits |

### Phase 2: Prompt with context loaded

| Step | Title | Action |
|------|-------|--------|
| 04 | Load the archaeology | Share commit message, PR description, linked ticket — give AI the history it can't see |
| 05 | Constrain the removal | Prompt AI to propose changes with explicit reasoning for what was preserved and why |

---

## 04 / Anti-Patterns

Comparison table (Wrong → Right):

| Wrong | Right |
|-------|-------|
| "This looks unused" | Trace all call sites, including dynamic ones, before concluding anything is dead |
| "AI said it's safe to remove" | AI doesn't know your incident history — that's your job to supply |
| "The code is old, therefore bad" | Age is not evidence of obsolescence. Old fences often guard old wounds |
| "It has no tests, so it must be dead" | Critical defensive code is often untested because it's hard to reproduce |
| "I don't understand it, so I'll delete it" | Not understanding it is the reason to investigate, not the reason to remove |

---

## 05 / Case Study — The 500ms That Brought Down Payments

**Setup:** A backend service has `await sleep(500)` before calling a payment processor SDK. AI flags it during a "dead code cleanup" sprint — no comment, no test, looks like a forgotten debug delay. AI removes it. The PR is reviewed and merged.

**Simulated git archaeology** (rendered as a styled terminal block):
```
$ git log -p --follow -- payment/processor.js | grep -A5 "sleep"

commit a3f9c2d  (3 years ago)  marcus.chen@company.com
"fix: add delay before processor.init() call"

+  await sleep(500); // SDK fires PAYMENT_READY before internal
+                    // state is actually ready. Race condition.
+                    // Filed: GH-2847. No fix from vendor yet.
```

**What happened without it:** 3% of transactions attempt to charge before the SDK's internal token cache is warm — silent failures, no exception thrown. Only surfaces under load. Took 6 hours to diagnose.

**Resolution:** The fence is restored. A comment is added. A test is written that detects the race. The archaeology is baked into the code itself.

---

## 06 / Quiz — 3 Questions

1. AI proposes removing a `try/catch` that "never triggers in tests." What do you do first?
   - *Correct: check git history for why it was added*

2. A `|| []` default in a 4-year-old utility function has no comment. Safe to remove?
   - *Correct: not until you know what was returning null/undefined before*

3. Which is the strongest reason to keep unfamiliar code?
   - *Correct: you can't explain what would break if it were gone*

---

## 07 / Cheatsheet — 6-cell Quick Reference Grid

1. **The Rule** — Never remove what you can't explain
2. **Investigation Commands** — git log, git blame, git log -p
3. **Pre-Prompt Checklist** — steps before handing anything to AI
4. **Red Flags** — AI danger zones (no comment, no test, looks unused)
5. **The Removal Test** — "Can I explain exactly what this defends against?"
6. **The Archaeology Prompt** — copy-paste template for loading context into AI

---

## Visual & Technical Conventions

- Follows `occams-razor.html` exactly for CSS variables, layout, and JS patterns
- Same accent color system (no per-page overrides)
- Hero opens with incident teaser before title
- Case study uses a styled `<pre>` terminal block to simulate git output
- Workflow section branded as "The Archaeology Protocol"
- All CSS and JS embedded inline — no external files
