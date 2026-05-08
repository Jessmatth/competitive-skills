---
name: battle-card
description: Create a competitive battle card — a markdown document that helps internal sales reps win deals against a specific named competitor. The card covers TL;DR positioning, discovery questions, objection handling, pricing tactics, switch stories, recent intel, and where the competitor wins (the honest section reps need). Use this skill whenever the user asks for a battle card, "[competitor] battle card," sales enablement document for a specific competitor, competitive playbook, objection-handling doc, "how do we sell against [competitor]," or any internal text document that helps sales reps navigate competitive deals. Trigger this skill when the user wants Claude to research a named competitor and produce a working battle card filled with usable intelligence, even if they do not say the words "battle card" explicitly. Do NOT use for prospect-facing visual comparisons (use competitive-comparison-graphic for those instead); this skill produces sales-team-facing text documents.
---

# Battle card

A skill for producing competitive battle cards: text documents that help sales reps win deals against a specific named competitor. The output is a markdown file structured for skim-reading mid-call.

## When to use

Trigger this skill when the user wants any of these:

- A battle card for a specific named competitor
- A competitive playbook or sales enablement doc against a vendor
- Objection handling against a competitor
- A "how do we sell against X" document
- A refresh of an existing battle card
- An internal compete page for a competitor

Do not trigger for visual comparison graphics (those go to `competitive-comparison-graphic`). This skill produces a text document for the internal sales team, not a visual for prospects.

## What good battle cards do that bad ones don't

A battle card works when reps can find the right answer in under 10 seconds. That means:

- **Skimmable.** Each section bite-sized. Reps glance at it during a discovery call.
- **Honest.** Reps trust the card more when it admits where the competitor wins. Without that, they discount everything.
- **Discovery before objection handling.** Traps set early in the deal pay off later. The "where we win" and "discovery questions" sections come before "objection handling" because the goal is to anchor the deal on our strengths before objections arrive, not to react after.
- **Dated.** Recent intel needs a refresh date. Stale intel kills credibility faster than missing intel.
- **Has a feedback loop.** Without a way for reps to flag what's working, the card goes stale by Q2.

These are not stylistic preferences — they are the difference between a card reps actually use and one that lives in a wiki nobody opens.

## Inputs you need

Required:
- **Competitor name** — the company being beaten

Recommended (ask if not provided):
- **User's company name** — for context on positioning. If not supplied, write the card with `[Your Company]` placeholders.
- **Win rate vs the competitor** — a number from CRM data. If unknown, leave the field blank rather than inventing one.
- **PMM owner / point of contact** — the person reps escalate to.
- **Refresh cadence** — quarterly is the default unless the user says otherwise.

If the user has only given you the competitor name, write the card with researched content for the competitor and `[placeholder]` markers for the user's own context. Don't invent the user's company info.

## Workflow

### 1. Confirm scope

If the user has only said the competitor's name, confirm: "Filled-in card with research, or just the template?" Default to filled-in unless they want a blank template.

### 2. Research the competitor

Search the web for usable intelligence. Run roughly these searches in parallel where you can:

- `[competitor] product features pricing`
- `[competitor] G2 reviews complaints` — surfaces real objections from buyers
- `[competitor] vs [user's company]` — finds existing comparison content
- `[competitor] case study customer outcomes`
- `[competitor] funding leadership news` — for the recent-intel section
- `[competitor] pricing tier discount` — for pricing tactics

Fetch the competitor's homepage and pricing page if they're public. Pull their hero message, top 3 claims, and ICP from the marketing copy.

For G2 reviews, look for the "what users dislike" sections. These give you real objections the rep will hear and real seams to attack.

### 3. Draft the card

Read `template.md` and fill in each section. Apply these constraints:

**TL;DR**: 2 sentences max. Sentence 1 = when reps will see this competitor. Sentence 2 = the 1 thing to remember when handling them.

**Where we win**: 3 differentiators, no more. Each with a "what we do," a "why it matters to the buyer," and a proof point. If you don't have a proof point, write `[need proof point]` rather than fabricating a customer name.

**Where they win**: be substantive. At least 2 to 3 honest cases where the competitor genuinely fits better. If you cannot identify any, the section is wrong — every competitor wins somewhere. Reps notice when this section is empty or dismissive ("they don't really win") and stop trusting the card.

**Discovery questions**: 5 questions max. They should expose the competitor's weak spots without being leading. "How are you handling [thing the competitor is bad at] today?" works. "Doesn't [competitor] have a problem with X?" doesn't.

**Objection handling**: 3 to 4 common objections. Each with a response and a follow-up question. The follow-up question is what turns the objection back into a discovery moment.

**Pricing and deal tactics**: only fill in what you actually know. If you don't have their list price, write `[unknown — ask deal desk]` rather than guessing. Wrong pricing intel is worse than missing pricing intel.

**Recent intel**: dated. If the section is more than 30 days old at write time, mark it as stale.

**Switch stories**: name customers who moved from the competitor to the user's company. If you don't have these, write `[need switch stories from CS team]`.

### 4. Review against the quality bar

Before saving, check:

- Is "Where they win" substantive (≥2 cases, not dismissive)?
- Are discovery questions positioned BEFORE objection handling?
- Is there a refresh date and an owner field?
- Are unknowns marked as placeholders, not invented?
- Does the card fit on roughly 2 pages once printed (skim test)?

If any of these fail, fix before delivering.

### 5. Save and present

Save as `[competitor]-battle-card.md` in the outputs directory and present the file. Mention 1 or 2 obvious follow-ups: a Word doc version for distribution, a 1-pager condensed version for SDRs, or a slide-deck variant for QBRs.

## Output format

Default: markdown file at `/mnt/user-data/outputs/[competitor-name]-battle-card.md`.

Offer Word doc on request — markdown converts cleanly via the docx skill. Some sales teams prefer Google Docs; mention that markdown copy-pastes into Google Docs and Notion well.

## Style rules for the card itself

These are properties of the document, not personal preferences. They apply regardless of the user's writing voice:

- **Sentence-case headers.** No Title Case, no ALL CAPS.
- **Active voice.** "Reps win this section by doing X" not "X is what is done by reps."
- **Digits for numbers.** "3 differentiators" not "three differentiators."
- **Short paragraphs.** 1 to 3 sentences.
- **Minimal bolding.** Use `**bold**` for the differentiator labels and the objection quotes only. Bolding random words mid-sentence makes the card harder to skim.
- **No em dashes** in the document body. The only em-dash that's allowed is in attribution lines (`— Person Name`).

## Examples

**Good filled-in differentiator:**

```
**1. Revenue impact attribution**
- What we do: Native Salesforce integration ties competitive intel directly to closed-won revenue per battlecard
- Why it matters to the buyer: CFOs need to see CI's revenue contribution, not vanity engagement metrics
- Proof: Affinity case study, win rate moved from 16% to 45% after deploying our Impact module
```

**Bad filled-in differentiator (don't do this):**

```
**1. Best-in-class platform**
- What we do: We're the leader in the space
- Why it matters: Customers love us
- Proof: We have many customers
```

The bad version is generic, unverifiable, and gives the rep nothing to say. The good version names a specific capability, names the buyer's pain, and names a specific customer outcome.

**Good "Where they win" entry:**

```
- [Competitor] genuinely fits better when the prospect is mid-market with no dedicated CI owner and a single competitor to track. Their starter tier is 30% cheaper than ours, and their lower-touch onboarding lands faster for teams without a PMM.
```

**Bad "Where they win" entry (don't do this):**

```
- They don't really win, but their marketing is louder than ours.
```

The bad version tells reps nothing. The good version gives them an honest segment to qualify out of, which protects win rate.

## Template reference

The full template is in `template.md` in this skill directory. It contains placeholders in `{{DOUBLE_CURLY}}` format and section structure that should not be reorganized — the section ordering is part of the design.
