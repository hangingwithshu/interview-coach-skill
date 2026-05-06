# Interview Coach

A Claude Code-based interview coach that covers the full job search lifecycle, from JD analysis and resume optimization through mock interviews to post-offer negotiation. 23 commands across application materials, interview prep, practice, analysis, and comp coaching. It scores your answers across five dimensions, diagnoses root causes behind weak spots, builds a storybank you can retrieve under pressure, and adapts its coaching to your specific patterns. Not a generic question bank. An adaptive system that gets sharper the more you use it.

Say `kickoff`, share your resume, and you're being coached in under 2 minutes.

---

## Fork Modifications

This is a fork of [noamseg/interview-coach-skill](https://github.com/noamseg/interview-coach-skill), which is no longer actively maintained.

The main motivation for this fork is token efficiency. Every unnecessary prompt costs tokens, and in a session that runs dozens of commands, that adds up. These changes trim low-value back-and-forth so sessions stay focused.

Two changes from the upstream:

1. The `decode` command saves its output to `prep/<company>/decode.md` and opens it in Obsidian. JD analysis persists across sessions and stays linked to the company folder, so you don't re-run it and pay for it twice.

2. The session-start recommendation no longer leads with "any news from X companies?" before suggesting the next move. The coach goes straight to the highest-leverage action (`hype` when an interview is within 48h, `stories` when the storybank is empty, etc.), cutting back-and-forth that burns tokens without adding coaching value.

---

## What It Does

| Feature | Description |
|---|---|
| Scoring and diagnosis | Every answer scored on five dimensions: Substance, Structure, Relevance, Credibility, and Differentiation, calibrated to your seniority. Scores map to root causes (status anxiety, narrative hoarding, conflict avoidance) with targeted fixes. |
| Adaptive coaching | After scoring, a decision tree triages your bottleneck and routes you to the right drill. Relevance gap gets question-decoding practice. Substance gap builds raw material. The system doesn't run the same sequence for every candidate. |
| Transcript analysis | Paste raw transcripts from Otter, Zoom, Grain, Google Meet, Teams, Tactiq, Granola, or any other tool. Auto-detects the format and normalizes it. Behavioral interviews get Q&A parsing, system design gets phase-based analysis, panel interviews track cross-interviewer dynamics. |
| Storybank management | Full STAR text, earned secrets, strength ratings, and rapid-retrieval drills. Story-to-question mapping uses a 4-level fit scoring system with portfolio optimization that resolves conflicts, tracks freshness, and detects overuse. Narrative identity extraction finds 2-3 core themes so every answer reinforces a coherent thesis. |
| Practice and mocks | 8-stage drill progression plus full 4-6 question mock interviews in behavioral, system design, case study, panel, and technical+behavioral formats. Every round includes the interviewer's inner monologue. |
| Outcome calibration | Tracks whether practice scores predict real interview outcomes. After 3+ real interviews, runs scoring drift detection and recalibrates. Also learns from successes, tracking which stories and patterns correlate with advancement. |
| Role-fit assessment | Evaluates fit across five dimensions: requirement coverage, seniority alignment, domain relevance, competency overlap, and trajectory coherence. Distinguishes strong fits from investable stretches and long shots, so you focus energy where you're competitive. |
| Company research | Three depth levels (Quick Scan, Standard, Deep Dive) with a structured search protocol. Every company-specific claim maps to a source tier: verified, general knowledge, or unknown. |
| Interview intelligence | Learns from your real interviews. Transcripts, debriefs, and recruiter feedback build a personalized knowledge base with temporal decay; stale data is flagged, not silently relied on. |
| Application materials | Resume optimization across 8 dimensions, LinkedIn profile optimization against platform mechanics, a core positioning statement with variants at every duration (10s to 90s), and networking outreach coaching across 9 message types. Everything cross-references your storybank and positioning statement for consistency. |
| JD analysis | Six-lens decoding with confidence labels on every interpretation. Maps extracted competencies against your profile for a fit verdict. Batch triage mode compares 2-5 JDs and finds your market-validated sweet spot. |
| Presentation coaching | Coaches narrative structure using four arc frameworks, calibrates content density against time limits, and prepares Q&A with predicted questions and answer strategies. Three depth levels from quick framework to full talk track review. |
| Comp coaching | Covers the recruiter screen "what are your salary expectations?" question, salary history handling, and application form strategy. Hands off to `negotiate` when a formal offer arrives. |
| Session continuity | A persistent `coaching_state.md` file tracks your storybank, scores, patterns, drill progression, interview loops, and calibration state across sessions. Saves are automatic. |
| Guided flow | Recommends a specific next step after every command based on your coaching state. Detects multi-step intent (e.g. "prepare me for my Google interview") and walks you through the full sequence with natural transitions. |
| Challenge protocol | At Level 5, the coach red-teams stories through five lenses, runs pre-mortems before interviews, mines rejections for leverage, and names avoidance patterns directly. Levels 1-4 are unaffected. |
| Differentiation | Earned secrets and spiky points of view are a first-class dimension. The system pushes past "competent" toward "memorable." |
| Self-awareness | Tracks the gap between your self-assessment and actual coach scores. Knows if you're an over-rater or under-rater, and adjusts coaching accordingly. |

---

## Quick Start

### Option 1: Claude Code (recommended)

1. Clone the repo:

```bash
git clone https://github.com/hangingwithshu/interview-coach-skill.git
cd interview-coach-skill
```

Or [download it as a ZIP](https://github.com/hangingwithshu/interview-coach-skill/archive/refs/heads/main.zip) and unzip.

2. Activate the coach by renaming the skill file:

```bash
mv SKILL.md CLAUDE.md
```

3. Open the folder in Claude Code and say `kickoff`.

Requires any paid Claude plan. Also works with Claude Code (terminal), Cursor, or any environment with file system access.

### Option 2: OpenAI Codex

1. Clone the repo:

```bash
git clone https://github.com/hangingwithshu/interview-coach-skill.git
cd interview-coach-skill
```

Or [download it as a ZIP](https://github.com/hangingwithshu/interview-coach-skill/archive/refs/heads/main.zip) and unzip.

2. Activate the coach by renaming the skill file:

```bash
mv SKILL.md AGENTS.md
```

3. Open the folder in Codex and say `kickoff`.

Requires any paid ChatGPT plan.

---

For both options, the coach will ask for your resume, target role, and timeline — then build your profile, assess your starting point, and give you a prioritized action plan. Everything saves automatically to `coaching_state.md` so you pick up where you left off next session.

---

## Commands

### Getting Started

| Command | Purpose | Typical Output |
|---|---|---|
| `kickoff` | Setup profile, track, and preferences | Kickoff summary + time-aware action plan |

### Interview Round Prep

| Command | Purpose | Typical Output |
|---|---|---|
| `research [company]` | Company research + structured fit assessment (3 depth levels) | Company snapshot, culture signals, fit assessment, claim-verified findings |
| `decode` | JD analysis + batch triage (3 depth levels, 6 lenses) | Confidence-labeled decoding, competency extraction, fit assessment, recruiter verification questions, batch comparison, teaching layer |
| `prep [company]` | Build role-specific prep brief (format-aware, culture-aware, role-fit assessment) | Format guidance, culture read, role-fit assessment, interviewer intelligence, competencies, predicted Qs, story mapping |
| `concerns` | Anticipate interviewer concerns | Concern-counter-evidence map |
| `questions` | Generate interviewer questions | 5 tailored, non-generic questions |
| `present` | Presentation round coaching (3 depth levels) | Narrative arc selection, content structuring, timing calibration, opening/closing optimization, Q&A preparation, constraint versions |

### Application Materials

| Command | Purpose | Typical Output |
|---|---|---|
| `linkedin` | LinkedIn profile optimization (3 depth levels) | Section-by-section audit, rewritten sections, content strategy |
| `resume` | Resume optimization (3 depth levels, JD-targeted when available) | ATS audit, section-by-section assessment, bullet rewrites, seniority calibration, keyword analysis, storybank-to-bullet pipeline |
| `pitch` | Core positioning statement + context variants | Core statement, constraint ladder, context-specific pitches, positioning consistency check |
| `outreach` | Networking outreach coaching (3 depth levels, 9 message types) | Message frameworks, draft critique + rewrite, follow-up sequences, multi-channel campaign strategy |

### Pre-Conversation

| Command | Purpose | Typical Output |
|---|---|---|
| `salary` | Early/mid-process comp coaching (3 depth levels) | Comp research guidance, range construction, stage-specific scripts, total comp education, salary history handling |
| `hype` | Pre-interview confidence + psychological warmup. At Level 5: includes a pre-mortem with failure prevention | 60-second reel + 3x3 sheet + focus cue + recovery playbook |

### Practice and Simulation

| Command | Purpose | Typical Output |
|---|---|---|
| `practice` | Run drill rounds (with progression gating). At Level 5: challenge notes, expanded interviewer read, optional warmup skip | Round debrief + self-assessment delta + targeted adjustment |
| `mock [format]` | Full simulated interview (4-6 Qs) — behavioral screen, deep behavioral, panel, bar raiser, system design/case study, technical+behavioral mix | Holistic arc feedback, signal-reading notes, energy trajectory |
| `stories` | Build/manage storybank + rapid-retrieval drill. At Level 5: stories get red-teamed with 5 challenge lenses | Story table + earned secrets + gap analysis + retrieval drill |

### Analysis, Tracking, and Post-Interview

| Command | Purpose | Typical Output |
|---|---|---|
| `analyze` | Analyze transcript with format-aware parsing, triage-based coaching, and interviewer's inner monologue. At Level 5: includes structured challenge | Auto-detected format, per-unit scoring (Q&A/phases/exchanges), format-specific dimensions, decision tree + interview delta |
| `debrief` | Post-interview rapid capture (same day) | Questions recalled, interviewer signals, stories used, coaching state updates |
| `progress` | Trends, self-calibration, outcome tracking, scoring calibration. At Level 5: includes a Hard Truth section | Self-assessment delta + outcome correlation + scoring drift detection + root cause tracking + coaching meta-check |
| `feedback` | Capture recruiter feedback, outcomes, corrections, context, or coaching meta-feedback. At Level 5: rejections include structured leverage extraction | State updates + next step suggestion |
| `thankyou` | Post-interview follow-up drafts | Thank-you note + variants |
| `negotiate` | Post-offer negotiation coaching | Offer analysis + strategy + scripts + specific language |
| `reflect` | Post-search retrospective + archive | Journey arc, breakthroughs, transferable skills, archived state |
| `help` | Show command menu (context-aware) | Full command list + recommended next based on coaching state |

---

## Fast Workflow Examples

### 1) Initial setup

```text
kickoff
```

Expected output:

- Track selected (`Quick Prep` or `Full System`)
- Profile snapshot (strength signals and concern areas)
- Interview readiness assessment
- Time-aware action plan (adjusted to your interview timeline)

### 2) Company research (before committing to prep)

```text
research Notion
```

Expected output:

- Company snapshot (stage, size, culture signals — claim-verified with source tiers)
- Fit assessment against your profile
- "If you decide to apply" next steps

For high-priority targets, mention you want a deep dive: "Do a deep dive on Notion" — gets you employee posts, product reviews, competitor analysis, and leadership profiles on top of the standard research.

### 3) Before an interview

```text
prep Stripe
```

Then provide:

- Job description
- Role/seniority
- Optional interviewer LinkedIn URLs (for per-interviewer intelligence)

Expected output:

- `Interview Format` (with format-specific coaching boundaries)
- `Company Culture Read`
- `Interviewer Intelligence` (if profile links provided — per-interviewer lens, focus areas, rapport hooks, story recommendations)
- `What They Optimize For`
- `Your Best Positioning`
- `Likely Concerns + Counters`
- `Predicted Questions (7-10)`
- `Story Mapping`
- `Questions To Ask Them`
- `Day-Of Cheat Sheet`

### 4) Right after an interview

```text
debrief
```

Rapid capture while details are fresh — works with or without a transcript. Get:

- Questions recalled and reconstructed answers
- Interviewer signals observed (engagement, skepticism, interest)
- Stories used (auto-updates storybank `Last Used` dates)
- Coaching state updated for the next session

### 5) Analyzing a transcript

```text
analyze
```

Then paste raw transcript text from any tool (Otter, Zoom, Grain, Teams, etc.). The system auto-detects the format and normalizes it.

Expected output:

- Format detection and normalization
- Per-unit score blocks (Q# for behavioral, P# for system design phases, E# for panel exchanges)
- `Scorecard`
- `Triage Decision` (data-driven coaching path based on your patterns)
- `What Is Working`
- `Top 3 Gaps To Close`
- `Storybank Changes`
- `Priority Move (Next 72 Hours)`

### 6) Drill practice

```text
practice
```

Drills (in progression order — advance when you meet gating thresholds):

- `practice ladder` — Constraint drills (30s, 60s, 90s, 3min)
- `practice pushback` — Handle skepticism and interruption
- `practice pivot` — Redirect when questions don't match prep
- `practice gap` — Handle "I don't have an example" moments
- `practice role` — Role-specific specialist scrutiny
- `practice panel` — Multiple interviewer personas
- `practice stress` — High-pressure simulation
- `practice technical` — Thinking out loud, clarification-seeking, tradeoff articulation (system design / case study / mixed format only)

Standalone (not gated):

- `practice retrieval` — Rapid-fire story matching under time pressure

Expected output each round:

- `Round Debrief`
- `What Worked`
- `Gaps`
- `Scorecard` (5 dimensions)
- `Self-Assessment Delta`
- `Next Round Adjustment`

### 7) Full mock interview

```text
mock behavioral Stripe
```

Runs a complete 4-6 question interview simulation. Formats: behavioral screen, deep behavioral, panel, bar raiser, system design/case study, technical+behavioral mix. Holistic feedback on:

- Overall impression and hiring signal
- Energy trajectory and pacing across the full arc
- Story diversity and selection quality
- Signal-reading (did you adapt to interviewer cues?)
- Per-question scoring + holistic patterns only visible across the full session

### 8) Decode a JD before applying

```text
decode
```

Then paste the job description. Get:

- Competency extraction with confidence labels (HIGH/MEDIUM/LOW)
- 6-lens analysis (repetition frequency, order, required vs. nice-to-have, verb choices, between-the-lines signals, what's missing)
- Fit assessment against your profile (Strong Fit / Investable Stretch / Long-Shot Stretch / Weak Fit)
- Recruiter verification questions for uncertain interpretations
- Teaching layer so you learn to decode JDs yourself

For multiple JDs: paste 2-5 and get batch triage with ranking, your market-validated sweet spot, and allocation recommendations.

### 9) Build your positioning statement

```text
pitch
```

Get:

- Core positioning statement anchored to your strongest earned secret
- Context variants: 10-second elevator, 30-second networking, 60-second recruiter, 90-second interview TMAY
- Positioning consistency check across resume, LinkedIn, and interview narrative

### 10) Coach an outreach message

```text
outreach
```

Then specify message type (cold LinkedIn, warm intro, recruiter reply, etc.) and target. Get:

- Draft critique (if you bring a draft) or guided construction
- Rewritten message within platform constraints (300 chars for LinkedIn connection requests)
- Follow-up sequence with timing
- Earned secret hooks pulled from your storybank

### 11) Post-offer negotiation

```text
negotiate
```

Then provide offer details, competing offers, and ideal outcome. Get:

- Market position analysis
- Negotiation strategy with priority ordering
- Exact scripts for the conversation
- Fallback language for pushback

---

## Tracks

### Quick Prep

Best when interview timeline is short.

- Company research
- Prep brief
- Focused transcript analysis
- Immediate next actions

### Full System

Best when running a multi-week search.

- Storybank management with rapid-retrieval drills and portfolio-optimized story mapping
- Multi-format transcript analysis (behavioral, system design, panel, mixed) with decision tree triage
- Pattern and trend tracking with self-assessment calibration
- Differentiation coaching integrated into all workflows
- Full mock interview simulations (behavioral, system design, case study, panel, technical+behavioral mix)
- Drill progression with gating thresholds (8 stages + standalone retrieval)
- Post-interview debrief and rapid capture
- Outcome tracking (correlate practice with real results) with scoring calibration (drift detection, recalibration)
- Interview intelligence — learns question patterns, what works/doesn't, and company-specific insights from your real interviews, with temporal decay on stale data
- Interview loop awareness across company rounds
- Post-offer negotiation coaching
- Post-search retrospective and archiving

Choose during `kickoff`. You can switch later.

---

## Repository Structure

```text
interview-coach-skill/
├── SKILL.md                            # Core skill — rename to CLAUDE.md to activate
├── README.md                           # This file
├── LICENSE                             # MIT License
├── coaching_state.md                   # Created on first kickoff (persistent memory, auto-saved)
└── references/
    ├── commands/                       # Per-command workflows (loaded on demand)
    │   ├── kickoff.md
    │   ├── research.md
    │   ├── prep.md
    │   ├── analyze.md
    │   ├── debrief.md
    │   ├── practice.md
    │   ├── mock.md
    │   ├── stories.md
    │   ├── concerns.md
    │   ├── questions.md
    │   ├── linkedin.md
    │   ├── resume.md
    │   ├── pitch.md
    │   ├── outreach.md
    │   ├── decode.md
    │   ├── present.md
    │   ├── salary.md
    │   ├── hype.md
    │   ├── thankyou.md
    │   ├── progress.md
    │   ├── negotiate.md
    │   ├── feedback.md
    │   ├── reflect.md
    │   └── help.md
    ├── cross-cutting.md                # Shared modules: gap-handling, signal-reading, differentiation, cultural awareness, psychological readiness, cross-command dependencies
    ├── rubrics-detailed.md             # Scoring anchors, root causes, seniority calibration
    ├── role-drills.md                  # Role-specific drills + interviewer archetypes
    ├── differentiation.md              # Earned secrets, spiky POVs, clarity under pressure
    ├── transcript-processing.md        # Step-by-step transcript analysis guide (format-aware parsing)
    ├── transcript-formats.md           # Format detection + per-format normalization (Otter, Zoom, Grain, etc.)
    ├── storybank-guide.md              # Story management + rapid-retrieval drill
    ├── story-mapping-engine.md         # Portfolio-optimized story mapping with fit scoring
    ├── calibration-engine.md           # Scoring drift detection, root cause tracking, success patterns
    ├── challenge-protocol.md           # Five-lens challenge framework (Level 5 only): assumption audit, blind spot scan, pre-mortem, devil's advocate, strengthening path
    └── examples.md                     # Worked examples: scored answers, triage, rewrites, system design analysis
```

---

## Best Results

1. Share a real resume (not a high-level summary).
2. Include a full job description for `prep` — and the interview format if you know it.
3. Use real transcripts for `analyze`. The more you give it, the better the triage.
4. Keep a living storybank with `stories`. Extract earned secrets for every story.
5. Run `progress` weekly — it tracks your self-assessment accuracy, not just scores.
6. After real interviews, log outcomes. The system correlates practice scores with real results.
7. When you hear back from a recruiter — good or bad — run `feedback` to capture it. The system learns from your real experiences over time.
8. Run `mock` before important interviews. Individual drills build skills; mocks test the full arc.
9. Use `debrief` the same day as a real interview — capture signals while they're fresh.
10. Run `decode` before applying — analyze the JD's language, assess your fit, and decide if the role is worth your time. Use batch triage to compare multiple JDs at once.
11. Run `salary` before your first recruiter call — the recruiter screen is the highest-leverage comp moment, not the offer negotiation.
12. Run `present` before a presentation round — structure your content and prepare for Q&A before you ever open PowerPoint.

---

## FAQ

**How is this different from asking ChatGPT for interview help?**
Generic LLM interview help gives you the same advice regardless of your patterns. This system scores you on five dimensions, tracks your scores over time, diagnoses root causes behind weak spots, builds a storybank with retrieval drills, and adapts its coaching based on what the data reveals. It remembers your previous sessions, knows which stories you've already used at a company, and changes its approach when something isn't working. It's the difference between a textbook and a coach.

**Does this only work for tech roles?**
No. Core workflows are role-agnostic; role drills include PM, Engineering, Design, Data Science, Research, Operations, and Marketing.

**Why is the feedback direct?**
The skill is intentionally high-candor and evidence-based. It uses strengths-first delivery and self-reflection before critique. It also periodically checks whether the coaching is landing and adapts if not. You can set your feedback directness level (1-5) during kickoff. At Level 5, the Challenge Protocol activates: stories get red-teamed, progress includes a Hard Truth, rejections get mined for leverage, and avoidance patterns are named directly. Levels 1-4 are gentler — same rigor, softer delivery.

**How does it work across multiple sessions?**
The skill writes a `coaching_state.md` file that tracks your storybank, scores, patterns, drill progression, interview outcomes, interview loops, and more. At the start of each session, it reads this file and picks up where you left off. Saves happen automatically after every major workflow — not just at session end.

---

## Contributing

Open an issue or PR with:

- Repro steps
- Current behavior
- Expected behavior
- Suggested fix (optional)

---

## Credits

Created by [Noam Segal](https://www.linkedin.com/in/noamsegal/).

---

## License

MIT
