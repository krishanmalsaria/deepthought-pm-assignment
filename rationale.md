# Design Rationale — Leadership Portfolio Redesign
**DeepThought Product Management Internship Assignment**
Candidate submission · Part A

---

## Overview

The core problem: the Leadership Portfolio looked like a dashboard — metric widgets in a grid, equal visual weight, optimized for monitoring. The goal was to make it feel like a **pitch deck** — narrative-first, story-driven, something an employee would be proud to show a mentor.

My redesign makes one fundamental shift: **story leads, data supports.** Every section opens with a narrative paragraph written for a human reader, with numbers as evidence — not the other way around.

---

## Design Decisions

### 1. Signal first — one unmistakable headline

**Decision:** A dark full-width block at the top with a human sentence as the first thing you read:
*"Strongest month since joining — score jumped from 64 to 71. Delivered 16 of 20 assigned work items. Growing in 4 of 6 areas. Tracking 3 months ahead of V3 plan."*

**Why:** Experiment 1 (from the brief) used metric concatenation — "42 of 54 delivered · 14 IP commits · 4/5 axes above threshold" — which is number soup. The eye doesn't know where to land. A sentence with an adjective ("Strongest") tells you immediately whether this was a good month or not. The dark background creates visual dominance — it's impossible to miss.

**Tradeoff:** A sentence requires the backend to generate it accurately. If the narrative engine produces a wrong adjective (calling a bad month "Strong"), it damages trust. I've assumed server-side narrative generation is reliable — as stated in the brief.

---

### 2. Narrative before data in every section

**Decision:** Each of the 5 sections opens with the narrative paragraph, followed by numbers and evidence.

**Why:** The portfolio's primary audience is the employee reading about themselves, then a mentor or supervisor. For the employee, reading the story of their month first creates context — the numbers then feel like proof, not interrogation. Experiment 2 in the brief confirmed this: narrative-first felt better for employees.

**Tradeoff:** Supervisors often want numbers first. I've resolved this by making the narrative short (3–4 sentences) and placing the data immediately below — so a supervisor can skip the paragraph and go straight to the numbers without losing much. A future "supervisor mode" toggle could flip the order, but for this version I've optimized for the primary reader: the employee.

---

### 3. Six sections — kept all six, but with progressive disclosure

**Decision:** All 6 sections are present. The top 2 (What I Shipped, How I'm Growing) are fully open. The bottom 3 (Target Performance, What Got in the Way, Where I'm Headed) have their narrative and key stats visible, with detailed evidence collapsible.

**Why:** Removing sections loses data fidelity — the 6-axis model is the backbone of PDGMS. But showing everything at equal weight creates overwhelm. The solution is hierarchy through layout: the most emotionally meaningful sections (delivery + growth) dominate visually. Career trajectory is prominent but doesn't compete with the contribution story.

**Tradeoff:** Collapsed sections might be missed by a quick reader. I've kept the summary stats always visible (raised/resolved counts, KPI hit/miss) so even in collapsed state, the section communicates.

---

### 4. Constraint section — "What Got in the Way" framing

**Decision:** Renamed "Constraint Patterns" to "What Got in the Way." Used a resolved/open visual split — green left border for resolved, red for open. Led with the narrative, which contextualizes the blockers as professional challenges rather than complaints.

**Why:** The hardest design challenge in the brief. If you call it "Blockers" or "Problems" with red everywhere, the portfolio feels like a complaint document. If you hide it, the diagnostic value disappears. The solution: frame it as professional communication ("here's what I navigated") and show resolution rate prominently — 5 of 8 resolved demonstrates agency, not victimhood.

**Tradeoff:** The narrative does heavy lifting here. A poorly written narrative could still make this section feel like finger-pointing. The design assumes backend narratives are written in a professional, factual tone — as the mock data demonstrates.

---

### 5. Portability — UID visible, jargon removed

**Decision:** The permanent UID (PDGMS-EMP-00512) appears in three places: identity bar, footer, and print band. Jargon replaced throughout: "IP Commits" → "Original Work", "Rituals" → "Engagement", "QA Pending" → "Awaiting Review", "Frameworks" → "Structured Thinking".

**Why:** The brief states the portfolio follows the employee even after they leave the organization. A mentor or future employer who has never heard of PDGMS should be able to read this and understand it. Internal jargon creates a barrier. The UID in the gold monospace style makes it feel official and permanent — like a document number on a professional certificate.

**Tradeoff:** Some precision is lost. "Frameworks" has a specific technical meaning in PDGMS (verified claims of applying recognized thinking frameworks). "Structured Thinking" is slightly broader. I've accepted this loss of precision in favor of readability for an external audience.

---

## Design Challenges Addressed (from Part 10)

### Challenge 1 — The Signal
Chose a human sentence over a score ring or grade. Reason: a sentence communicates direction and context in one read. A 72/100 ring requires the reader to interpret whether 72 is good — a sentence tells them directly. The dark block treatment creates the visual dominance a score ring would have, without losing the narrative quality.

### Challenge 2 — Story vs Data Ordering
Narrative-first throughout. Optimized for the employee as primary reader. Supervisor needs addressed by keeping narrative short and data immediately adjacent.

### Challenge 4 — Constraint Section
"What Got in the Way" framing, resolution rate as the leading metric, professional narrative tone, and resolved/open visual distinction without making open items feel shameful.

### Challenge 5 — Portability and Identity
UID in three locations. All jargon replaced with plain language. Employee name and role prominent in the identity bar. The portfolio reads as the employee's document, not a company report about them.

---

## What I Would Do Differently With More Time

1. **Month-over-month sparklines** — A small trend line next to each axis score showing the last 3 months would make "growing in 4 of 6 areas" concrete. The data exists (CareerRunrateSnapshotEnriched has delta and direction fields) but rendering it well requires more design iteration.

2. **Supervisor mode** — A toggle that flips section order to data-first for supervisor review conversations. The backend data is the same; only the rendering order changes.

3. **Career runway with confidence band** — The RunwayNode type has a confidenceBand field (leftPct, widthPct, earliest, latest) that would make the projected V3 date feel more honest — "February 2027, give or take 6 weeks" rather than a single date.

4. **Print / PDF optimization** — The portfolio is meant to be a portable artifact. A print stylesheet that collapses all sections and optimizes for A4 would make it genuinely shareable outside PDGMS.

---

## Assumptions Made

- Employee name, role, program, and organization come from user session/auth context (not the portfolio endpoint) — used directly from mock data as the brief confirms this.
- Narrative paragraphs are generated server-side and assumed to be well-written — the design depends on narrative quality.
- The threshold for all axes at V3 is 60 — used this as the threshold marker on capability bars.
- "Original Work" is an acceptable plain-language equivalent of "IP Commits" for an external audience.
- The portfolio is read on a desktop browser as the primary surface — responsive design included but not the primary optimization target.

---

*Submitted as Part A of the DeepThought PM Internship Assignment.*
*HTML prototype in the same repository: `leadership-portfolio.html`*
