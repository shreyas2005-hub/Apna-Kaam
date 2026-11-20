# Apna Kaam

**A WhatsApp-based agentic AI platform for trusted rural hiring.**

Hackathon entry for problem 8.2: *Rural youth cannot find work that fits, and small employers cannot find them* (theme: Youth and Women).

> Status: idea submission. The prototype is planned, not yet built. Everything below describes what we will build, and we will mark which parts are live and which are simulated.

## The problem

Young people in rural areas with school, ITI or college qualifications struggle to find local work that fits their skills, location and income needs. Jobs travel through relatives, WhatsApp forwards and agents. According to the challenge brief, small employers take 2 to 3 months to hire and 40 to 50 percent of hires fail within three months. Workers also risk fake listings and unpaid wages.

## What Apna Kaam does

A local-language WhatsApp assistant that guides workers and small employers through one hiring journey:

1. **Worker onboarding**: voice or text; the assistant collects skills, experience, approximate location, expected pay, travel limit and availability, and the worker confirms the profile.
2. **Employer onboarding**: employers describe a vacancy in everyday language; the assistant structures it and asks about anything missing. It never invents details.
3. **Listing screening and human review**: automated checks flag missing information, inconsistent conditions and recruitment-payment requests. In the prototype, an admin approves every listing.
4. **Explainable, bias-aware matching**: hard constraints first (travel limit, minimum pay, availability), then ranking by relevant skills and preferences. Each match explains why it fits and lists open conditions. Names, gender, caste and religion are excluded from matching inputs.
5. **Optional skill demonstrations**: a short task video or a described experience, as supporting information, not certification.
6. **Consent-based employer contact**: workers see exactly which fields will be shared; approval is recorded per employer and job and enforced by backend access controls.
7. **Post-placement feedback**: follow-ups at day 7, 30 and 90 ask whether the worker joined, is still employed and was paid on time. Concerns go to human review.

## Agentic AI design

Five bounded agent workflows (worker onboarding, employer onboarding, listing screening, job matching, post-placement follow-up) run on a shared language model and an orchestrator with explicit states and permissions.

The language model cannot approve listings, bypass eligibility rules or release contact details. Backend rules enforce publication, matching constraints and information sharing, and humans handle flagged cases.

## Architecture

```
Worker / Employer (WhatsApp, voice or text)
        |
Interface: WhatsApp channel + speech-to-text (+ web view for testing)
        |
Orchestrator + language model (extraction, clarifying questions, explanations)
        |
Backend rules: eligibility, publication, consent / sharing
        |
Rules-based matching engine
        |
Database: profiles, employers, listings, applications, consent history, feedback
        |
Admin dashboard (listing review, reported issues) + scheduler (follow-ups)
```

## Hackathon prototype scope

One complete journey, using synthetic workers and listings:

1. A worker creates and confirms a profile by voice or text.
2. An employer submits and confirms a vacancy.
3. Automated checks flag issues and an admin approves the listing.
4. The engine ranks eligible jobs.
5. The assistant explains each match and its open conditions.
6. The worker approves sharing selected details with an employer.
7. A clearly labelled, simulated follow-up collects feedback and routes a concern for review.

**Out of hackathon scope:** full employer verification, automated skill certification, broad language coverage, public employer ratings, real 90-day tracking.

## Evaluation plan

On synthetic data and predefined test cases: extraction accuracy, onboarding completion, adherence to travel, pay and availability limits, consistency of match explanations with recorded data, no contact sharing without recorded consent, and handling of incomplete listings, suspicious inputs and errors.

A real pilot (a few ITIs, skilling centres, employers and panchayats in one district) would be needed to assess placement outcomes, 90-day retention, worker-reported wage timeliness and fairness of matching.

## Repository layout (planned)

```
/docs        pitch deck and architecture diagram
/backend     API, rules, matching engine, scheduler
/bot         WhatsApp / chat interface and agent workflows
/admin       listing review dashboard
/data        synthetic workers and listings
```

## Team

[Team name] · [Members] · [College]
