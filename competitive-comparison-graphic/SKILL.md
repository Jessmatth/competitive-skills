---
name: competitive-comparison-graphic
description: Create a polished, prospect-facing competitive comparison graphic comparing the user's company against a named competitor. The output is a 680px-wide SVG with 3 hero metric cards, a 4-row capability comparison with bars, and a customer quote. Use this skill whenever the user asks to build a battle card visual, vs-graphic, comparison chart for prospects, "why us over them" image, competitive one-pager, side-by-side product comparison, or any sales-facing image showing how their company stacks up against a specific named competitor. Trigger this skill any time a side-by-side visual comparison between two named companies is needed for sales or marketing collateral, even if the user does not use the exact phrase "battle card" or "comparison graphic." Do NOT use for internal text-heavy battle cards (those are markdown documents); this skill is for the visual collateral that goes in front of prospects.
---

# Competitive comparison graphic

A skill for generating a prospect-facing competitive comparison graphic. The graphic is a 680px-wide SVG with header, 3 hero metric cards, 4 capability rows with side-by-side bars, and a customer quote.

## When to use

Trigger this skill when the user wants any of these:

- A "vs" graphic for sales (e.g., "Acme vs Competitor")
- A prospect-facing comparison chart
- A battle card visual (the *image*, not the internal sales doc)
- A "why us over them" one-pager
- A competitive one-pager for a deck or LinkedIn post
- A side-by-side capability comparison they can put in front of a buyer

Do not trigger for internal sales enablement docs (those are text-heavy markdown). This skill produces a polished image, not a document.

## Inputs you need

Required:
- **User's company name** — the company creating the graphic
- **Competitor name** — the company being compared against

Strongly recommended (ask if not provided):
- **3 hero metrics**, each with a value, a label, and a source. These appear at the top.
- **4 capabilities to compare**, each with a short title, a 4–5 word description, and 2 scores (user's company and competitor) on a 0–100 scale.
- **A customer quote with attribution.**

Optional:
- **User's brand color** (hex) — if not provided, search for it (see "Brand research" below).
- **Competitor brand color** — default to neutral gray `#6F7375`. Using the competitor's actual brand color is honest but most B2B comparison collateral uses neutral gray for the competitor to avoid looking petty.

## Workflow

### 1. Gather inputs

If the user has only given you the two company names, ask for the rest. Suggest defaults if helpful, but do not invent metrics or quotes — those need to come from the user or from verifiable public claims.

If the user wants you to research metrics (e.g., "use Crayon's published claims"), do a web search for the user's company's published customer outcomes and pull verifiable numbers. Cite sources in your response so the user's legal team can verify before publication.

### 2. Brand research

If the user hasn't supplied their brand color:

1. Search: `[company] brand color palette primary hex`
2. Look for a brand guide PDF, brandfetch entry, or style guide on their site
3. Fetch the brand guide if you find one
4. Extract the primary brand color hex

If you can't find an authoritative brand color, ask the user. Don't guess — using the wrong color on their own collateral is a brand violation.

### 3. Score the capabilities honestly

Resist the urge to make every row 95/15. A graphic where the user wins every category by a huge margin loses credibility immediately. Aim for spreads like:

- Row 1: 95 / 60 (clear lead)
- Row 2: 90 / 70 (solid lead, but credible)
- Row 3: 95 / 55 (strongest area)
- Row 4: 90 / 75 (closer comparison — this is what makes the rest believable)

Include at least one row where the gap is closer (within 15–20 points). This makes the rest of the graphic feel honest. Without it, prospects discount the whole thing.

### 4. Tighten the descriptions

The left text column is 225px wide. Capability subtitles that exceed about 30 characters at 12px will run into the bar columns. Keep capability titles to 23 characters or less, and capability subtitles to 4–5 words.

Bad: "Sparks AI generates SWOTs, win themes, and summaries" (overflows)
Good: "Sparks AI summarizes intel" (fits cleanly)

### 5. Render the SVG

Read `template.svg` and replace the `{{PLACEHOLDER}}` tokens with the user's content. Then render via the visualization tool if available (`show_widget` or equivalent), or save to disk as an SVG file.

Bar widths are calculated from scores: `bar_width_px = round((score / 100) * 145)`. The maximum bar width is 145.

### 6. Tell the user how to export and adapt

After rendering:

- Mention that the graphic exports as SVG (right-click → save, or screenshot for slides).
- Note that the column-header wordmarks are stylized text, not licensed logos — they should swap in actual logo SVGs from each company's brand assets before publishing externally.
- Flag any metric that came from a single-customer case study so legal can review.
- Offer a follow-up: a 16:9 slide-deck variant, a metrics-only LinkedIn version, or a version with a different customer quote.

## Layout reference

The SVG is 680 wide, 712 tall. Coordinates are pixels. Do not change the layout structure — change only the placeholder content.

```
y=30–119    Header (eyebrow, headline, subhead, accent line)
y=146–244   3 hero metric cards (194 wide each, 98 tall, 9px gap)
y=290       "Capability comparison" section header
y=298       Top divider
y=322–328   Column header row (Capability label | user's wordmark | competitor's wordmark)
y=350       Bottom divider
y=384–602   4 capability rows (64px row spacing)
y=616       Final divider
y=648, 672  Quote and attribution
```

Bar columns:
- User's bar: x=275 to x=420 (max width 145)
- Competitor's bar: x=455 to x=600 (max width 145)

Left text column ends at x=265.

## Design rules

These come from the original design pattern. Don't relax them — they're what makes the graphic look credible rather than amateurish:

- **Sentence case everywhere.** No Title Case, no ALL CAPS — even for eyebrow text (use letter-spacing to get the "eyebrow" look).
- **Two font weights only:** 400 (regular) and 500 (medium). Never 700.
- **No emoji, no gradients, no shadows, no gradients.**
- **Don't use red for the competitor.** Looks insecure. Use neutral gray (`#6F7375`).
- **Customer quote uses serif:** `font-family="var(--font-serif)"` and `font-style="italic"`. This is the only place serif appears.
- **Round all displayed numbers.** No "2.0×" — use "2×". No "98.5%" — use "98%".

## Template

The SVG template is in `template.svg` in this skill directory. It contains placeholders in `{{DOUBLE_CURLY}}` format. Replace them all before rendering.

### Placeholder reference

| Placeholder | Example | Notes |
|---|---|---|
| `{{HEADLINE}}` | `Crayon vs Klue` | Big top headline |
| `{{SUBHEAD}}` | `Why enterprise CI teams choose Crayon...` | One-line positioning |
| `{{ACCENT_COLOR}}` | `#2DC3D0` | Color of the small underline rect |
| `{{COMPANY_COLOR}}` | `#0538BF` | User's brand primary, for bars and metric text |
| `{{COMPANY_COLOR_SOFT}}` | `rgba(5,56,191,0.15)` | Same color at 15% alpha for bar background |
| `{{COMPANY_COLOR_BG}}` | `rgba(5,56,191,0.08)` | Same color at 8% alpha for metric card background |
| `{{COMPANY_COLOR_SUB}}` | `#0363D1` | Lighter shade for metric card subtitle |
| `{{COMPETITOR_COLOR}}` | `#6F7375` | Competitor bar color (default neutral gray) |
| `{{COMPETITOR_COLOR_SOFT}}` | `rgba(111,115,117,0.15)` | Competitor bar background |
| `{{COMPANY_WORDMARK}}` | `crayon` | Lowercase company name |
| `{{COMPETITOR_WORDMARK}}` | `klue` | Lowercase competitor name |
| `{{COMPETITOR_WORDMARK_COLOR}}` | `#1A2540` | Competitor wordmark color (try to match their brand) |
| `{{METRIC_N_VALUE}}` | `2×` | N=1,2,3. Big number. |
| `{{METRIC_N_LABEL}}` | `competitive win rate` | Short label under value |
| `{{METRIC_N_SOURCE}}` | `Crayon customer outcomes` | Attribution under label |
| `{{CAP_N_TITLE}}` | `Competitor monitoring` | N=1,2,3,4. ≤23 chars. |
| `{{CAP_N_SUB}}` | `100+ data types tracked daily` | ≤30 chars / 4–5 words |
| `{{CAP_N_COMPANY_BAR}}` | `138` | Pixel width = round(score/100 * 145) |
| `{{CAP_N_COMPETITOR_BAR}}` | `87` | Same calculation for competitor |
| `{{QUOTE}}` | `"Our win rate increased from 16% to 45%."` | Wrap in actual quotes |
| `{{ATTRIBUTION}}` | `— Director of CI, Affinity` | Use em-dash here (the only allowed em-dash) |

## Examples

**Good filled-in example:**

```
Headline: Crayon vs Klue
Subhead: Why enterprise CI teams choose Crayon to track signals, enable sales, and prove revenue impact
Company color: #0538BF (Crayon Battle Blue)
Competitor color: #6F7375 (neutral)

Metrics:
  2× / competitive win rate / Crayon customer outcomes
  100+ / data sources tracked / automated daily
  85% / less manual research / vs traditional methods

Capabilities (title / sub / company score / competitor score):
  Competitor monitoring / 100+ data types tracked daily / 95 / 60
  AI insight synthesis / Sparks AI summarizes intel / 90 / 70
  Revenue impact tracking / Salesforce-linked attribution / 95 / 55
  Enterprise integrations / Salesforce, Slack, Gong, MCP / 90 / 75

Quote: "Our win rate increased from 16% to 45%."
Attribution: — Director of Market and Competitive Intelligence, Affinity
```

**Bad inputs to push back on:**

- All four capabilities scored 95/15 — too lopsided, ask the user to think of one closer comparison
- Hero metrics with no source attribution — ask where the number came from
- "We win every category" subhead — too aggressive, suggest a more confident-but-honest framing
- Capability subtitle longer than 5 words — will overflow into the bars; tighten it
- A red competitor color — looks insecure; suggest neutral gray
