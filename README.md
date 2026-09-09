# InfraShield AI — SIH26103

An AI-powered predictive risk dashboard for infrastructure projects, built for the SIH26103 problem statement ("AI for Infrastructure Monitoring" — PAIMANA / MoSPI / IPMD).

## What this is

A single-file, front-end-only React prototype (`InfraShield_AI.html`) — no backend, no build step. Open it directly in a browser. All data is in-memory sample data; nothing is persisted or sent anywhere.

## Outcome coverage (vs. the SIH26103 brief)

| # | Expected outcome (from the brief) | Status | Where |
|---|---|---|---|
| a | Cost Overrun Prediction Model | ✅ Implemented (rule-based) | `runAIAnalysis()`, AI Risk Analysis page |
| b | Time Overrun Prediction Model | ✅ Implemented (rule-based) | `runAIAnalysis()`, AI Risk Analysis page |
| c | Project Risk Scoring Framework | ✅ Implemented | overall risk % + LOW/MEDIUM/HIGH/CRITICAL classification |
| d | Early Warning Alert System | ✅ Implemented | Early Warnings page — auto-generated alerts, assignment, priority, comments |
| e | Benchmarking & Comparative Analytics Module | ✅ Implemented | Benchmarking page — sector averages, project-vs-sector percentile |
| f | Cost Escalation Driver Analysis Module | ✅ Implemented | Driver Analysis page — portfolio-wide and per-sector driver ranking |
| g | AI-powered Monitoring Dashboard | ✅ Implemented | Dashboard page |
| h | LLM-enabled Project Intelligence Assistant | ✅ Prototype | Assistant page — rule-based NLU over the same dataset, **not** a live LLM call (see below) |
| i | Documentation and deployment framework | ✅ This file | Scope, architecture, and deployment notes |

## Honest scope note

This is a demo, not a production system:

- **Data**: 10 hardcoded sample projects, not a live PAIMANA/OCMS/CUF feed. No data ingestion or API layer exists.
- **"AI" prediction engine**: a transparent, weighted rule-based scoring formula (`runAIAnalysis()` in the script), not a trained ML model. It combines progress gap, milestone delays, expenditure ratio, resource gap, prior delays, and contractor performance into risk scores. It is deliberately isolated behind one function so it can be swapped for a real trained model (e.g. XGBoost / scikit-learn served over an API) without touching any UI component.
- **Benchmarking & driver analysis**: computed by aggregating the same rule-based scores across the sample portfolio (grouped by project type as a sector proxy). A production version would benchmark against real historical OCMS/PAIMANA baselines and use proper statistical methods (e.g. z-scores, regression coefficients) rather than an averaged heuristic.
- **"LLM-enabled" assistant**: the Assistant page answers questions by pattern-matching keywords (project name/ID, state, sector, "highest risk", "cost overrun", "delay", "driver") against the in-memory dataset — it does **not** call a real language model. It's labeled as a rule-based demo in the UI itself. The function `answerAssistantQuery()` is isolated so it can be replaced with a real LLM call (e.g. Claude with tool-use/function-calling over the project dataset) for genuine open-ended natural-language reasoning.

## Architecture

- Single HTML file, React 18 + Babel Standalone loaded from CDN (no bundler), Tailwind via CDN.
- All pages are React components in one `<script type="text/babel">` block.
- Two functions are the swap points for real AI/ML/LLM integration:
  - `runAIAnalysis(project)` → cost/time overrun prediction + risk scoring + explanation + recommended actions.
  - `answerAssistantQuery(query, projects)` → project intelligence assistant.
- Charts (gauge, bar, grouped bar, donut, sparkline) are dependency-free inline SVG components — no charting library.

## Deployment

No build step is required.

- **Local**: double-click `InfraShield_AI.html`, or serve the folder with any static server (`python3 -m http.server`) and open it in a browser.
- **Static hosting**: upload `InfraShield_AI.html` as-is to any static host (GitHub Pages, Netlify, Vercel static, S3 + CloudFront). It needs outbound access to the CDN URLs for React, Babel, Tailwind, and Google Fonts.
- **Production path**: to move beyond prototype, replace the CDN script tags with a proper build (Vite/CRA), move `SAMPLE_PROJECTS` to a real API backed by PAIMANA/CUF data, replace `runAIAnalysis()` with a served ML model endpoint, and replace `answerAssistantQuery()` with a real LLM call.

## Login

The login screen is a UI demo only (no real authentication, no backend). Use "Continue with Demo Login" to enter the app.
