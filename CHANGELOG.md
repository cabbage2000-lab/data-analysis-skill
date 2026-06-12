# Changelog

All notable changes to the `data-analysis-skill` project are documented here.
Version numbers align with the requirements document (`requirements/data-analysis-skill-需求文档-v0.4.md`).

## [Unreleased]

### Planned
- **Stock market template `stock.md`** (#11, design approved 2026-06-10) — individual stock OHLCV + valuation
- **Finance / quant template `finance.md`** (#2, second batch) — portfolio / strategy backtest / credit data
- **Catering / F&B template** — pending user demand confirmation
- **Government / public sector template** — pending user demand confirmation
- **Method modules** (`references/`) enhancement — time-series decomposition, anomaly detection, NLP sentiment (§2.4 roadmap)

### Under consideration
- Interactive data exploration phase before report generation (drill-down charts)
- Export formats beyond HTML (Markdown, PDF via headless browser)
- Multi-language report support beyond auto-detection (§10)
- Community-contributed industry templates via PR

---

## v0.15 — 2026-06-12

- Table dual-mode: static publish table ≤20 rows, auto Grid.js interactive table >20 rows with pagination / search / numeric sort (Grid.js 6.2.0 dual-source CDN lock, bootcdn primary + unpkg fallback)
- Relaxed table data discipline: detail rows now allowed, single-table cap 500 rows, TOP-N truncation with processing_notes
- `validate_template.py` added 13 new assertions (dual-source version lock, threshold constant, numeric parse sort, Chinese locale, print CSS)
- Node unit tests: 21 cases (static table byte-identical ×3, parseNum ×13, numCompare ×5)
- Playwright runtime tests: 13 items (dual-mode, ascending/descending numeric sort, search filter, print media)
- Education template `education.md` delivered (#6, first-batch item) — training institution panorama: student operations + teaching effectiveness + enrollment acquisition
- SKILL.md industry mapping table registered `education.md`

## v0.14 — 2026-06-12

- Report narrative areas now use `@tailwindcss/typography` plugin for block-level rendering (headings, lists, bold via `mdBlock()`)
- Tailwind Play CDN URL locked to `3.4.16?plugins=typography@0.5.16` (versioned plugin param prevents 302 drift)
- `references/visualization.md` added "Narrative Typography (Phase 5)" discipline
- `validate_template.py` added 4 assertions (plugin URL lock, no-version param negative defense, mdBlock wiring)

## v0.13 — 2026-06-11

- Repositioned as cross-AI-coder-tool Agent Skill (not Claude Code exclusive) — README, docs, §1 wording neutralized
- Added MIT open-source license (LICENSE, © 2026 cabbage2000-lab) with README badge and footer

## v0.12 — 2026-06-11

- Renamed skill `data-analysis` → `data-analysis-skill` — aligned GitHub repo, project directory, and skill identity
- Updated SKILL.md `name`, evals.json `skill_name`, sync-to-user.sh paths, report template signature, README, CLAUDE.md

## v0.11 — 2026-06-10

- Construction template `construction.md` delivered (#13, off-list supplement) — construction enterprise panorama: project output/progress + contract/receivables
- Lightweight delivery: no eval/test data (pattern follows v0.6 self-media / v0.8 fund / v0.10 real-estate precedent)
- SKILL.md industry mapping table registered

## v0.10 — 2026-06-10

- Real estate template `real-estate.md` delivered (#12, off-list supplement) — property sales panorama: sales absorption + market dynamics
- Lightweight delivery: no eval/test data
- SKILL.md industry mapping table registered

## v0.9 — 2026-06-10

- Codex CLI adaptation: SKILL.md platform-agnostic clauses (TodoWrite → update_plan, AskUserQuestion → text numbered-choice fallback)
- Graceful degradation path for non-interactive mode (`codex exec` / `claude -p`) — standard EDA + general template fallback
- `sync-to-user.sh` extended with Codex target `~/.codex/skills/data-analysis-skill`
- Smoke-tested on Codex CLI 0.139.0 (both exec and interactive paths)

## v0.8 — 2026-06-10

- Fund template `fund.md` delivered (#10, off-list supplement) — fund product panorama: performance + scale/redemption
- Lightweight delivery: no eval/test data
- SKILL.md industry mapping table registered

## v0.7 — 2026-06-10

- Corporate finance / FP&A template `corporate-finance.md` delivered (#9, off-list supplement) — enterprise P&L, expenses, budget, cash flow
- New eval scenario T7 "Finance template application" with test data `finance_pnl.csv` (24 months × 4 business units × 5 accounts)
- T7 with_skill run-1: 6/6 PASS

## v0.6 — 2026-06-10

- Industry template #8 repositioned: "Content / Media" → "Self-media / Content Creator `self-media.md`" — individual creators, bloggers, MCN operators
- `self-media.md` early-delivered (moved up from second batch)
- SKILL.md industry mapping table registered

## v0.5 — 2026-06-10

- SKILL.md frontmatter defined — CSO discipline (description = trigger-only, no workflow summary)
- Phase execution and gate rules formalized (§3.0) — Stage 1 mandatory gate, Stages 2–5 pass-through
- Visualization rules extracted to `references/visualization.md` — core layer slimmed
- Skill test scenarios T1–T6 defined (§13, TDD discipline)
- Skill shape confirmed: single skill, in-phase execution, industry/method modules loaded on demand

## v0.4 — 2026-06-10

- Dependency delivery reversed: inlined → CDN external links (confirmed always-online usage)
- Tailwind switched to Play CDN (runtime compilation, any utility class usable)
- CDN version locking and source selection requirements added (§4.2) — ECharts 5.4.3, Tailwind 3.4.16
- Acceptance criteria updated: "offline open" → "online open + fixed CDN versions"
- Target runtime confirmed as Claude Code (local)
- Report language strategy: auto-detect from user input or data language
- Industry templates: batch delivery confirmed — first batch general + retail + saas

## v0.3 — 2026-06-10

- Report tech stack finalized: single-file HTML + Tailwind + ECharts + Python data injection
- ECharts replaced Plotly as default chart library
- React explicitly excluded (Out of Scope)
- Asset layer `assets/report_template.html` added — analysis/presentation decoupled
- Single-file and offline-first mandatory requirement (later reversed in v0.4)
- Visualization spec (§4) rewritten — tech分工, no pyecharts, ECharts extension chart types
- Degradation: "report data too large" handling — aggregate/sample before injection

## v0.2 — 2026-06-09

- Five-phase analysis workflow designed (understand → explore → deep-dive → visualize → generate)
- Industry template strategy: three-tier (general → high-frequency → degradation)
- Template content spec: four components per industry (KPI dictionary, analysis themes, narrative language, section weighting)
- Report structure: six-section format (summary → data overview → deep analysis → visualizations → conclusions → appendix)

## v0.1 — 2026-06-09

- Project inception — initial requirements document
- Core positioning: cross-industry data analysis skill transforming raw data into visual narrative reports
- Single-file HTML interactive report as deliverable
