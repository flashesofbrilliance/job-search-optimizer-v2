# Job Search Optimizer v2.0

Enterprise-grade job application tracking and optimization platform with validated learning capabilities.

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

- Live (branch-based) URL: https://flashesofbrilliance.github.io/job-search-optimizer-v2/
- GitHub Actions workflow: `.github/workflows/deploy.yml` (builds `dist/` and deploys via actions/deploy-pages)

## Validated Learning Prompt

An open-source prompt template for iterative strategy and pacing lives at `prompts/validated-learning.md`. Use it with CSV exports to learn segment performance and compute the weekly applications needed to reach, for example, 5 offers in 6 weeks.

## Lenses (Patterns & Bias)

- Presets: Pattern (Top-fit AI/Crypto), Platform (Greenhouse/Lever), Bias (NYC/Onsite highlight), Pacing (This Week), and Custom (JSON).
- Modes: filter (narrows list) or highlight (visual emphasis without filtering).
- Fields supported in Custom: company, roleTitle, jobUrl, jobDomain, tags, location, status, fitScore, vibe, salary.
