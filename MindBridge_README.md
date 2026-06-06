# MindBridge — Mental Health Digital Therapeutic
### UX Design · Service Design · Behaviour Change Architecture · Digital Health

**Portfolio project** · Nada Abdelhalim · MSc Digital Health, TH Deggendorf · 2026  
**Product:** MindBridge — a mental health DiGA for depression and anxiety  
**Regulatory framework:** §139e SGB V · BfArM DiGA certification · DSGVO

---

## The Brief

Design the full product experience of a mental health digital therapeutic — from the moment a patient downloads the app to the moment their doctor decides whether to renew their prescription. Map both sides of that experience: what the patient lives through, and what the clinician needs to act on.

The constraint: everything has to work within the real regulatory infrastructure of the German DiGA system. This is not a consumer wellness app. It is a prescription medical device delivered as software — and that changes almost every design decision.

---

## What I Built

Four interconnected artefacts, each addressing a different layer of the product:

| # | Artefact | Format | Purpose |
|---|---|---|---|
| 01 | Lo-Fi Wireframes | HTML (interactive) | 8 patient onboarding screens, annotated |
| 02 | HCP Clinical Dashboard | HTML (interactive) | GP monitoring interface, 3 patient profiles |
| 03 | Intervention Loop Diagram | HTML (animated) | System-level behaviour change architecture |
| 04 | Break Point Analysis | Embedded in diagram | Where the loop fails and what to do about it |

---

## 01 · Patient Onboarding Wireframes

Eight low-fidelity screens mapping the patient's first experience of MindBridge — from welcome screen to first session unlock.

### Screen Sequence

| Screen | Purpose | Key Design Decision |
|---|---|---|
| Welcome | First impression | Hero image before any request — establish value before asking for anything |
| Freischaltcode Entry | Activate prescription | Code split into 4×4 groups matching paper format. Auto-capitalise. Error states designed before happy path. |
| Account Creation | Register or log in | KK (Krankenkasse) SSO as primary path — reduces friction, pre-populates patient data |
| DSGVO Consent | Mandatory compliance | Required and optional consents visually separated. Never labelled "agree to all." |
| Health Intake — Part 1 | Condition type | One question per screen. Plain language, not clinical terminology. |
| Health Intake — Part 2 | Symptom severity | Emoji scale + slider. Optional free text. Cultural translation validated. |
| Programme Preview | Set expectations | Patient sees their personalised programme before committing. Adjust without restarting. |
| Onboarding Complete | Launch first session | Celebration → notification setup → first session. No detours. |

### The Core Wireframe Argument

The highest drop-off points in DiGA onboarding are not motivation failures — they are friction failures. The code entry screen, the consent screen, and the intake survey are where patients leave. Each wireframe annotation documents the specific friction point and the design response.

---

## 02 · HCP Clinical Dashboard

A high-fidelity interface showing what a prescribing GP sees when monitoring their MindBridge patients. Designed for a 10-minute appointment slot — every data point visible must earn its place.

### Patient List View

Summary bar with live alert counts (2 critical, 3 review due, 9 stable). Filterable table with PHQ-9 scores, severity badges, 5-week sparkline trends, GAD-7 anxiety scores, session adherence bars, and status indicators. Prioritised by clinical urgency — alerts at the top, stable patients below.

### Patient Detail View — Three Interactive Profiles

**Anna Müller (alert state)**
PHQ-9 worsening from 14 → 18 over two weeks. Adherence at 52%. Declining mood chart. Red risk indicators across relapse risk and dropout probability. Alert banner with direct actions — schedule urgent review or dismiss.

**Thomas Hartmann (stable/review)**
PHQ-9 plateau at 11. 78% adherence. Flat trend line. Review due but no immediate clinical concern.

**Sarah Keller (improving)**
PHQ-9 down from 13 → 7 over four weeks. 91% adherence. Upward mood trajectory. Example of what a functioning intervention loop looks like in the data.

Each detail view includes: PHQ-9 item-level breakdown, 7-day mood bar chart, clinical risk indicator bars, GAD-7 subscale scores, current medication list, clinical timeline, and a live notes field.

### The Dashboard Design Argument

Most clinical dashboards fail because they present data rather than decisions. This interface is organised around urgency — who needs attention now, who is stable, who is improving. The HCP should know where to look within five seconds of opening the screen.

---

## 03 · Intervention Loop Diagram

A system-level diagram showing the behaviour change architecture that makes MindBridge work — and where it breaks.

### Two Concentric Loops

#### Patient Inner Loop (daily)

```
Trigger → Action → Feedback → Reward → repeat
```

| Node | Description | Design Component |
|---|---|---|
| Trigger | Push notification, scheduled reminder, or internal emotional cue | Notification system · In-app prompt |
| Action | CBT module, mood log, breathing exercise — must take ≤10 minutes | Session UI · Logging interface |
| Feedback | PHQ-9 trend, mood graph, progress message — must feel meaningful, not mechanical | Data visualisation · Progress screen |
| Reward | Progress visibility, completed module, confirmation that the HCP has seen their data | Achievement system · HCP signal |

#### HCP Outer Loop (weekly to monthly)

```
PGHD Aggregation → HCP Review → Clinical Decision → Loop Re-entry
```

| Node | Description | Actor |
|---|---|---|
| PGHD Aggregation | Patient-generated health data compiled into weekly report | System (automated) |
| HCP Review | Doctor reviews report at follow-up appointment | HCP |
| Clinical Decision | Renew DiGA, escalate care, adjust medication, or discharge | HCP |
| Loop Re-entry | HCP decision feeds back into patient app experience | ⚠ Break point |

### Bridge Pathways

Two connectors link the inner and outer loops:

- **Patient Feedback → PGHD Aggregation** (patient to HCP): session data flows up to the clinical layer
- **HCP Clinical Decision → Patient Trigger** (HCP to patient): the decision should update the patient's programme — but currently does not

The second bridge is where the system breaks.

---

## 04 · The Break Point

The most important insight in this project is not what works — it is what does not.

### The Gap

When the HCP reviews the data, makes a decision, and renews or adjusts the DiGA — that decision lives in the PVS. It does not automatically reach the patient's app. The patient continues the same programme regardless of what the doctor decided. The outer loop does not close.

### Three Failure Modes

**No HCP → app feedback channel**
No standardised pathway exists for an HCP's clinical decision to update a patient's DiGA programme in real time. Renewal, programme adjustment, and escalation decisions are all manual, verbal, or delayed to the next appointment.

**No standardised PGHD report format**
Every DiGA manufacturer sends different data to HCPs — some via KIM messages, some PDF reports, some requiring HCP login to a separate portal. A GP managing five DiGA patients across different apps has five different data formats to interpret. This makes HCP review inconsistent, time-consuming, and often skipped.

**Renewal gap equals treatment gap**
If the HCP does not renew the DiGA before day 90, the patient's programme closes without warning. There is no automated renewal prompt, no grace period, and no patient notification before expiry. A delayed renewal appointment means an unplanned interruption in treatment.

### Three Proposed Solutions

**Bidirectional data pathway**
HCP clinical decision triggers an update in the patient app — renewal extends the programme automatically, programme adjustment is reflected in the next session, escalation triggers a care coordination message. Technically feasible via ePA integration and KIM webhooks. Not yet implemented in any current DiGA.

**Standardised HCP report format**
A single-page clinical summary embedded directly in PVS — no external login, no PDF attachment. Consistent across all DiGA manufacturers. Would require BfArM to mandate a reporting standard, or a consortium of manufacturers to adopt one voluntarily.

**Automated renewal prompt**
A KIM message or PVS alert at day 80: "Patient X's DiGA expires in 10 days. Renew?" One-click response. Currently non-existent.

---

## Evidence Base

### BJ Fogg — Behaviour Model
Trigger × Motivation × Ability. The patient inner loop maps directly: Trigger (prompt) → Action (ability meets motivation) → Feedback (reinforcement) → Reward (motivation increase). Engagement drops when any of the three elements is insufficient — and in DiGA onboarding, the most common failure is ability, not motivation.

### Self-Determination Theory
Autonomy, competence, relatedness. The reward node must address all three. Streak counters address competence only. HCP acknowledgement of patient data addresses relatedness — the dimension most DiGA apps ignore entirely.

### DiGA Engagement Data
Approximately 40% of DiGA users disengage before day 30. Peak drop-off occurs at weeks 3–4. The primary driver is not motivation failure — it is weak feedback quality in the inner loop. Patients complete sessions but receive no meaningful reflection of their progress.

---

## Key Design Principles

**One question per screen**
Front-loading an intake survey causes abandonment. Progressive disclosure keeps completion rates higher.

**Never block on optional data**
Every intake field, every optional consent, every profile completion prompt — if it is not mandatory, it must not gate access.

**Design the error state before the happy path**
The code entry screen, the consent screen, the renewal gap — these were designed first because they are where the system fails most patients.

**Feedback must feel clinical, not gamified**
In a mental health context, a PHQ-9 trend graph communicates more trust and utility than a badge. The audience is a patient who has been prescribed this by a doctor — the product must honour that clinical frame.

**The HCP dashboard is a decision support tool, not a data display**
Every element is organised around: who needs attention now, who is stable, who is improving. Data that does not support a decision does not belong on the screen.

---

## Files

| File | Description |
|---|---|
| `mindbridge_wireframes.html` | Lo-fi wireframes — 8 screens, annotated, screen navigator |
| `mindbridge_hcp_dashboard.html` | High-fidelity HCP dashboard — interactive, 3 patient profiles |
| `mindbridge_intervention_loop.html` | Intervention loop diagram — animated, break point analysis, design notes |

---

## About

**Nada Abdelhalim**  
Medical Advisor · Scientific Communications · Digital Health Specialist  
FCB Health Reaktör (remote, Germany) · MSc Digital Health, TH Deggendorf (Grade 1.7)  
6+ years pharma medical affairs across EU and MENA markets  

`Medical Writing` `DiGA Regulation` `UX Research` `Behaviour Change` `§139e SGB V` `DSGVO` `PHQ-9` `HCP Dashboard Design` `Digital Therapeutics`
