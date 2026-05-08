# Competitive Skills for Claude Code

Three Claude Code skills that turn 30 minutes of research into the assets a PMM-of-one actually needs: a prospect-facing comparison graphic, an internal battle card, and a recurring competitor intel report.

Two of the three skills (`competitive-comparison-graphic` and `battle-card`) were written by [Jess Matthews](https://github.com/Jessmatth) while running customer development for [Echo](https://echo.ai), a competitive intelligence agent for sales-led B2B SaaS. The third (`competitor-intel`) is adapted from the open-source Goose Skills project. Free to use, fork, and remix.

---

## What's in here

### 1. Comparison Graphic (`competitive-comparison-graphic/`)

**Output:** A 680px-wide SVG, prospect-facing. Three hero metric cards, four capability comparison rows with bars, one customer quote.

**Use it for:**
- LinkedIn posts comparing your company against your top competitor
- Slide-deck visuals
- The image you attach to a cold DM (this is the lead-magnet use case)

**Trigger:** "Build a comparison graphic for [your company] vs [competitor]."

**Time to produce:** ~5-10 minutes once you have the inputs.

### 2. Battle Card (`battle-card/`)

**Output:** A markdown document, sales-team-facing. Covers TL;DR positioning, discovery questions, objection handling, pricing tactics, switch stories, recent intel, and where the competitor wins (the honest section reps need).

**Use it for:**
- Internal sales enablement
- The post-call gift you send a PMM after a customer-dev interview
- The seed for your own sales team's competitive playbook

**Trigger:** "Create a battle card for [competitor]."

**Time to produce:** ~15-20 minutes once the underlying intel exists.

### 3. Weekly Competitor Update (`competitor-intel/`)

**Output:** Structured competitor profiles plus a landscape summary. Markdown, designed to slot into a knowledge base or a recurring email update.

**Use it for:**
- The first deep dive on 3-5 competitors you'll be facing in deals
- A monthly or weekly refresh ("what changed at [competitor] this month?")
- Feeding the other two skills with raw research so you don't double-research

**Trigger:** "Research [competitor] for me" or "Weekly competitor update for [competitors]."

**Time to produce:** ~30-45 minutes for an initial deep profile, ~10-15 minutes for a refresh.

---

## How they work together

The three skills compose into a value ladder for cold outreach to PMMs:

| Stage | Skill | Effort | What it does |
|-------|-------|--------|--------------|
| Cold hook | Comparison Graphic | 10 min | Visual you attach to a LinkedIn DM. Gets opened. |
| Warm gift | Battle Card | 15 min | The thing they'd actually hand their reps. Sent post-call. |
| Background | Competitor Intel | 30 min | The research that powers both. Don't double-research. |

---

## Install

These are Claude Code skills. They live in `~/.claude/skills/`. To install:

```bash
git clone https://github.com/Jessmatth/competitive-skills.git
cp -R competitive-skills/competitive-comparison-graphic ~/.claude/skills/
cp -R competitive-skills/battle-card ~/.claude/skills/
cp -R competitive-skills/competitor-intel ~/.claude/skills/
```

Restart Claude Code (or run `/skills` to confirm they loaded). All three should now show up in the skill list.

To use one, just ask Claude Code in plain language. Each skill's description tells Claude when to fire automatically. Or invoke directly: `/competitive-comparison-graphic`, `/battle-card`, `/competitor-intel`.

---

## What you need before running them

The graphic and the battle card both expect inputs you provide or that Claude researches. Before you ask:

- **Both companies' names** (yours and the competitor's)
- **Your top 3 product-design or customer-outcome metrics** (honest ones, with sources)
- **Your top 4 capabilities** to compare side-by-side
- **A brand color** for your company (hex code)
- Optionally: a customer quote, or a published industry stat that frames the problem

The competitor-intel skill is more autonomous. Give it 2-5 competitor names and it will research the rest.

---

## Honest limitations

- **Don't fabricate metrics.** If your company has no customer outcomes yet (pre-launch, early-stage), use product-spec claims and label them as such. The graphic burns the moment you put fake numbers on it.
- **The graphic uses stylized text wordmarks**, not licensed logos. Swap in real logo SVGs before publishing externally.
- **G2 and Capterra often return 403** to direct fetches. The competitor-intel skill falls back to web search for review snippets; star counts may have small ranges.
- **Pricing is usually quote-only** in the CI category. Numbers cited in profiles are typically third-party estimates (Vendr, Prospeo), not vendor-published. The skills note this.

---

## Credits

- **`competitive-comparison-graphic`** — written by Jess Matthews (2026).
- **`battle-card`** — written by Jess Matthews (2026).
- **`competitor-intel`** — adapted from [gooseworks-ai/goose-skills](https://github.com/gooseworks-ai/goose-skills) (`skills/composites/competitor-intel`), MIT-licensed.

---

## License

MIT. Use them, fork them, ship them inside your own product if you want. A link back is appreciated but not required.

---

## Feedback

If you use these to source customer-dev interviews, ship a cold-outreach campaign, or build something better on top, I want to hear about it. Open an issue or DM [@Jessmatth](https://github.com/Jessmatth).
