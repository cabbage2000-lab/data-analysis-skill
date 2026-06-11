# data-analysis-skill: Turn data files into analysis reports that tell a story

**English** | [中文](README.zh-CN.md)

This is an **Agent Skill** for data analysis — it runs across multiple AI coding tools instead of being tied to any single one. Hand it a data file (CSV / Excel / JSON / TSV), say "analyze this", and it works like a data analyst who knows your industry: it first confirms the business context with you, then cleans and analyzes the data, and finally delivers a **single-file interactive HTML report** — not isolated charts and numbers, but a data story with insights and conclusions you can take straight into a meeting.

**Works in:** [Claude Code](https://claude.com/claude-code) (primary, fully tested) · [Codex CLI](https://developers.openai.com/codex/cli) (adapted) · and any AI coding tool that loads the same Agent Skill structure (`SKILL.md` + frontmatter + subdirectory resources). The five-phase workflow and statistical discipline are identical across tools — only the task-list and questioning mechanics adapt per tool.

**See it first**: open [`skills/data-analysis-workspace/sample_report.html`](skills/data-analysis-workspace/sample_report.html) in your browser (internet access required — chart libraries load from CDN).

---

## What it can do for you

- "Here's our Q2 order data — give me an analysis report" → a complete narrative report organized from a retail perspective: GMV, average order value, repeat purchases, returns — every chart comes with an interpretation, conclusions first
- "Check whether variant B in my A/B test is actually better" → a rigorous statistical answer (p-value, confidence interval, assumption checks) without forcing you through the full report pipeline
- "Analyze my account's posts from the past three months" → interpreted through a content-creator lens: engagement rate, completion rate, follower growth efficiency
- "Do a business review of this budget execution sheet" → analyzed from an FP&A perspective: revenue, gross margin, expense ratios, budget attainment

## Installation

Prerequisite: at least one supported AI coding tool installed — [Claude Code](https://claude.com/claude-code) and/or the [Codex CLI](https://developers.openai.com/codex/cli). A single command installs into whichever ones it detects (Codex only when `~/.codex/` exists).

```bash
# Run from the repo root; the skill is installed to ~/.claude/skills/data-analysis-skill,
# and to ~/.codex/skills/data-analysis-skill when ~/.codex/ is detected
bash sync-to-user.sh

# If your skills directories live elsewhere:
DATA_ANALYSIS_CLAUDE_SKILL=/your/path bash sync-to-user.sh
DATA_ANALYSIS_CODEX_SKILL=/your/codex/path bash sync-to-user.sh
```

Under Codex, task tracking uses update_plan and the stage-1 industry confirmation appears as a numbered text question (Codex has no structured questioning tool); the workflow and statistical discipline are otherwise identical.

To upgrade later, pull the latest code and run the same command again.

## How to use it

1. **Provide data, state your need.** In your AI coding tool (Claude Code, Codex, …), point to your data file and say what you want:

   ```
   Analyze this sales data for me: retail_orders.csv — I need a report
   ```

2. **Answer a few multiple-choice questions.** Before analyzing, it confirms your industry, analysis goal, and report audience. Don't skip this — it determines what the report analyzes and who it speaks to: an executive summary for your boss, or a detailed diagnosis for the ops team.

3. **Get the report.** It walks through data understanding → cleaning → metric computation → analysis → report generation, and delivers an HTML file you open in a browser.

> **Just have a quick question?** Things like "compute the correlation between these two columns" or "is group B's conversion significantly higher" won't be dragged through the full pipeline — it computes and answers directly, with the same statistical rigor.

## What the report looks like

- **A single HTML file**: double-click to open, interactive charts (zoom, tooltips), ready to share with colleagues (they need internet access to open it too)
- **A fixed six-section structure, conclusions first**: Key findings (3–5) → Background & goals → Data overview → Deep-dive analysis (sectioned by industry themes) → Conclusions & recommendations → Appendix: data processing notes
- **Every chart comes with an interpretation**: what the chart shows and what it implies — it doesn't just dump charts on you
- **Traceable processing**: how missing values were handled, whether outliers were dropped — every decision is recorded in the appendix
- **Report language follows your prompt language**: ask in English, get an English report

## Supported industries and methods

| Industry | Typical scenarios | What the report focuses on |
|----------|-------------------|----------------------------|
| Retail / e-commerce | Marketplaces, online stores, offline/omnichannel retail | GMV, average order value, repeat purchase rate, return rate, category mix |
| Internet / SaaS | Subscription software, internet products, membership services | MRR/ARR, retention, churn, net revenue retention |
| Content creators | Account operations on Xiaohongshu (RED), Douyin, Bilibili, WeChat official accounts, etc. | Engagement rate, completion rate, net follower growth, follower conversion efficiency |
| Corporate finance / FP&A | P&L, expenses, budget, cash flow analysis | Revenue growth, gross margin, expense ratios, budget attainment |
| Funds | Fund product performance and operations data | NAV returns, max drawdown, subscriptions/redemptions, holder structure |
| Everything else | When none of the above fits, it falls back to a general lens | Scale, trends, composition, distributions — without force-fitting another industry's KPIs |

When the task calls for specialized methods — A/B testing, time-series forecasting, causal inference, machine learning — it loads the corresponding method module on demand; you don't have to ask.

## Why you can trust the conclusions

The skill works under professional discipline — it would rather say less than make things up:

- **No fabricated industry benchmarks.** Unless you provide benchmark data or explicitly authorize a web search, it only compares within your own data — it never quotes an industry average "from memory."
- **Correlation ≠ causation.** Without causal-method validation it won't claim "A drove B," and it proactively calls out potential confounders.
- **No forced conclusions from small samples.** When the sample is too small, it tells you plainly that confidence is limited — even if "the boss needs an answer today."
- **Bad data gets a diagnosis first.** If data quality is too poor, it tells you what's missing and how to fix it, instead of fabricating a polished-looking analysis.

## What it doesn't do

- No live dashboards / dashboard apps (the deliverable is a static single-file report)
- No web scraping — it won't fetch data for you
- No direct database connections — export your data to CSV / Excel files first

## FAQ

**The report opens blank / charts don't render?**
Chart libraries load from CDN, so opening the report requires internet access. The CDNs are chosen to be reachable from mainland China.

**Want a PDF or static images instead?**
Just say so ("give me static charts" / "export to PDF") and it switches to a static-chart approach.

**Do I need to set up Python or install packages myself?**
Analysis runs locally inside your AI coding tool using Python. If dependencies like pandas are missing, it tries to install them automatically, with fallbacks if installation fails — generally nothing for you to worry about.

**It asks about my industry and goals — can I skip that?**
The confirmation step before a full report is deliberate: data that looks like retail data doesn't mean you want a retail reading of it. Ten seconds of choices make the report fit much better. Quick single questions skip this step entirely.
