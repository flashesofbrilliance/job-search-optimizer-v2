# Validated Learning Prompt (Open Source)

Use this prompt to analyze a job search dataset, learn what’s working, and refine the strategy toward a concrete goal (e.g., 5 offers in 6 weeks). It’s designed to run with any LLM and works best when you provide your latest exported CSV.

---

Goal
- Produce a weekly application target and a prioritized strategy to reach N offers within T weeks, based on observed conversion rates and segment performance.

Inputs
- CSV: export from the app with columns [Company, Role, Job URL, Status, Fit Score, Vibe, Salary, Applied Date, Location, Notes, Tags]
- Target offers: default 5
- Timeline (weeks): default 6

Analysis Dimensions
- Company: sector, stage, geography
- Role: level, function (IC vs Manager), domain (AI, Crypto, FinTech), product surface
- Source: referral, cold, recruiter, inbound
- Location: time zone alignment, onsite vs remote
- Compensation band
- Fit score and vibe trends over time
- Application status timeline: not-started → research → applied → interviewing → offer → rejected
- Job link quality: canonical URL availability, broken links
- Activity cadence: weekly volume, stalls, time-to-first-response

Core Tasks
1) Clean and segment
- Parse tags (split by ; or ,). Normalize sector, seniority, and location.
- Validate Job URL and mark broken/empty links.

2) Funnel and pacing
- Compute conversion rates:
  - p_app_to_interview = interviews / applications
  - p_interview_to_offer = offers / interviews
  - p_offer_total = p_app_to_interview * p_interview_to_offer
- Compute required totals for target offers N in T weeks:
  - applications_needed = ceil(N / p_offer_total)
  - weekly_applications = ceil(applications_needed / T)
  - interviews_needed = ceil(N / p_interview_to_offer)
  - per-stage backlogs to keep the funnel primed

3) Segment lift
- Identify top-3 performing segments by offer/interview rates and response time.
- Identify bottom segments to de-emphasize.

4) Strategy and experiments (validated learning)
- Generate 5–8 concise experiments (A/B style) across:
  - Sourcing: referral outreach templates, recruiter targets, company lists
  - Positioning: resume bullets, narrative variations, portfolio ordering
  - Timing: days/hours to apply, follow-up schedules
  - Geography/remote policy and compensation ranges
- Each experiment includes: hypothesis, change, success metric, sample size, expected lift, stop/continue rule.

5) Risk and focus
- Call out risks (e.g., over-reliance on one sector) and propose diversification.
- Create a weekly checklist covering apply, follow-ups, referrals, interview prep.

Outputs
- Human-readable summary: pacing, top segments, experiment list, weekly plan.
- JSON block (optional) for import to dashboards:
```json
{
  "pacing": {
    "target_offers": 5,
    "timeline_weeks": 6,
    "applications_needed": 72,
    "weekly_applications": 12,
    "interviews_needed": 20
  },
  "segments": {
    "top": [{"name": "AI Director Remote", "lift": "+28%"}],
    "bottom": [{"name": "FinTech NYC Onsite", "delta": "-15%"}]
  },
  "experiments": [
    {"hypothesis": "Referrals lift interview rate", "change": "Reach 10 warm contacts/wk", "metric": "p_app_to_interview", "sample": 30, "expected_lift": "+20%", "decision": ">+10% continue, else stop"}
  ],
  "risks": ["Overweight crypto", "Narrow geo filter"],
  "weekly_checklist": ["12 targeted applications", "6 follow-ups", "3 referral asks"]
}
```

How to Use
- Export CSV from the app.
- Paste the prompt and CSV summary (or a link) into your LLM of choice.
- Provide N (offers) and T (weeks) if different from defaults.
- Ask for both the narrative and the JSON to wire into analytics.

License
- MIT. Contributions welcome — PR ideas: additional segment taxonomies, more robust URL canonicalization, and confidence interval handling.
