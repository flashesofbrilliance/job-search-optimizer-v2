# Failure To Land (FTL) — Job Search Optimizer v2.0

Failure To Land (FTL) is an enterprise‑grade job application tracking and optimization platform with validated learning capabilities.

## Features
- 50+ curated crypto/AI/fintech product leadership roles
- Drag & drop kanban pipeline management
- Real job URLs with referral link support
- Advanced analytics and success pattern recognition
- Goal setting with velocity tracking
- CSV import/export functionality
- Archive/restore system
- Master activity log with gamification

## Quick Start
Follow these steps to run, build, and deploy v2 locally.

### 1) Install

```bash
cd job-search-optimizer-v2
npm install
```

### 2) Develop locally

```bash
# Starts a simple dev server at http://127.0.0.1:3000/index.html
npm run dev
```

Alternative local server:

```bash
# Serves current directory at http://127.0.0.1:8080
npm start
```

### 3) Lint and format (optional)

```bash
npm run lint
npm run format
```

### 4) Build (minified assets in dist/)

```bash
npm run build
# Outputs:
# - dist/style.min.css
# - dist/app.min.js
```

### 5) Deploy (GitHub Pages via gh-pages)

```bash
# Publishes the current directory to the gh-pages branch
npm run deploy
```

Notes:
- The default deploy script publishes the repository root (.) so index.html loads unminified assets. If you prefer serving the minified build, change the deploy script to `gh-pages -d dist` and ensure your index.html in dist references the minified files.
- Ensure your Git remote is set and you have push permissions before running `npm run deploy`.

## Deployment Status

- Live URL: https://flashesofbrilliance.github.io/job-search-optimizer-v2/
- Deploy workflow: `.github/workflows/deploy.yml` (builds `dist/` and deploys via actions/deploy-pages)
- Status badges:
  - [![Deploy to GitHub Pages](https://github.com/flashesofbrilliance/job-search-optimizer-v2/actions/workflows/deploy.yml/badge.svg)](https://github.com/flashesofbrilliance/job-search-optimizer-v2/actions/workflows/deploy.yml)
  - [Open Actions runs](https://github.com/flashesofbrilliance/job-search-optimizer-v2/actions)

### Live Demo

[![GitHub Pages](https://img.shields.io/badge/FTL-Live_Demo-2ea44f?logo=github&logoColor=white)](https://flashesofbrilliance.github.io/job-search-optimizer-v2/)
[Open FTL](https://flashesofbrilliance.github.io/job-search-optimizer-v2/) and try Discover (Explore slider, Novel badge, auto‑accept), Lenses (Pattern, Pacing, Bias, Platform, Prompt), and dashboard (Milestones, Pace, Coaching).

### UAT/QA Tips
- Watch deploy status via the badge above; click through for logs.
- Hard refresh or use a private window to avoid cache after deploy.
- Validate core flows: Lenses summary/tooltip, Discover (Yes/No/Skip, Undo, Explore slider), Suggestion banner, Dashboard (Milestones, Pace bars, Coaching), Needs Review filter, Export Bundle + Validation Report.

## Multi‑Environment Deploys

- Pages settings: set Pages to "Deploy from a branch" → `gh-pages` → `/ (root)`.
- Env paths (published by CI under `gh-pages`):
  - Dev latest: `/env/dev/latest/` (feature branches `feat/*`)
  - QA latest: `/env/qa/latest/` (branches `qa/*` and `main` builds)
  - Stage latest: `/env/stage/latest/` (release candidates `v*.*.*-rc.*`)
  - Prod latest: `/env/prod/latest/` (release tags `v*.*.*`)

Example URLs:
```
https://<org>.github.io/<repo>/env/dev/latest/
https://<org>.github.io/<repo>/env/qa/latest/
https://<org>.github.io/<repo>/env/stage/latest/
https://<org>.github.io/<repo>/env/prod/latest/
```

Each build includes `_provenance.json` (SHA256 hashes and commit SHA) for provability.

## Promote Between Environments (Provable)

- Actions → "Promote Artifact (env -> env)" → Run workflow with inputs:
  - `source_path`: e.g., `env/qa/latest` or `env/qa/main-<sha>`
  - `target_env`: one of dev/qa/stage/prod
  - `target_name` (optional): default derives from source
- Gates enforced:
  - Fails if open issues labeled `blocker` or `ac-fail` exist
  - Verifies `_provenance.json` file hashes match the copied artifact (0% error, deterministic)
- On success: publishes to `env/<target>/<target_name>` and updates `env/<target>/latest`.

## Validated Learning Prompt

An open-source prompt template for iterative strategy and pacing lives at `prompts/validated-learning.md`. Use it with CSV exports to learn segment performance and compute the weekly applications needed to reach, for example, 5 offers in 6 weeks.

## Lenses (Patterns & Bias)

- Presets: Pattern (Top-fit AI/Crypto), Platform (Greenhouse/Lever), Bias (NYC/Onsite highlight), Pacing (This Week), and Custom (JSON).
- Modes: filter (narrows list) or highlight (visual emphasis without filtering).
- Fields supported in Custom: company, roleTitle, jobUrl, jobDomain, tags, location, status, fitScore, vibe, salary.

## Data Interoperability

- Schemas (JSON Schema) in `schemas/`:
  - `jobs.v1.schema.json`, `feedback.v1.schema.json`, `lens.v1.schema.json`, `model.v1.schema.json`.
- Exports:
  - CSV: `jobs.csv` (stable, additive-safe headers)
  - JSONL: `jobs.jsonl` (jobs.v1 records), `feedback.jsonl` (CloudEvents-like feedback)
  - Bundle ZIP: `Export Bundle` packs jobs.csv, jobs.jsonl, feedback.jsonl, lenses.json, model.json, README.txt, checksums.txt
- Conventions:
  - ISO-8601 times, ISO 3166 country codes, ISO 4217 currency, schema_version in each JSON record.
