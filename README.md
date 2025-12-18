# Exit Narrative Generator

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10-blue" />
  <img src="https://img.shields.io/badge/Streamlit-Interactive-red" />
  <img src="https://img.shields.io/badge/scikit--learn-ML-orange" />
  <img src="https://img.shields.io/badge/pandas-dataframe-lightgrey" />
  <img src="https://img.shields.io/badge/Explainable-AI-green" />
  <img src="https://img.shields.io/badge/Counterfactual-Reasoning-yellow" />
  <img src="https://img.shields.io/badge/Interpretable-Models-blueviolet" />
  <img src="https://img.shields.io/badge/Systems-Thinking-black" />
  <img src="https://img.shields.io/badge/Narrative-Modeling-critical" />
  <img src="https://img.shields.io/badge/Human--Centered-ML-purple" />
  <img src="https://img.shields.io/badge/Instability-First-red" />
  <img src="https://img.shields.io/badge/Failure-Process-lightcoral" />
  <img src="https://img.shields.io/badge/HR-Analytics-informational" />
</p>

### Reconstructing Attrition as an Accumulated Decision Process

> People do not leave jobs suddenly.
> They leave when staying no longer feels defensible.

The **Exit Narrative Generator** is a systems-level interpretability engine that transforms employee attrition data into **coherent, human-readable narratives** explaining *why* exit pressure accumulates, *how* stabilizing forces erode, and *which small interventions could have plausibly changed the outcome*.

This project is not a prediction engine.
It is a **post-hoc explanatory system** designed to surface *meaning*, not alerts.

---

## Project Structure

```text
Exit-Narrative-Generator/
│
├── app/
│   └── app.py
│       # Streamlit application
│       # Interactive narrative report, peer context,
│       # dominant pressure visualization, and intervention builder
│
├── src/
│   ├── cli.py
│   │   # Command-line interface for data preparation,
│   │   # model training, and narrative export
│   │
│   ├── data_prep.py
│   │   # Data loading, cleaning, encoding, and
│   │   # feature normalization logic
│   │
│   ├── features.py
│   │   # Feature definitions and grouping
│   │   # (pressure vs retention anchor features)
│   │
│   ├── train_model.py
│   │   # Interpretable logistic regression training
│   │   # with transparent coefficient handling
│   │
│   ├── explain.py
│   │   # Per-employee contribution extraction
│   │   # (coefficient × feature value decomposition)
│   │
│   ├── narrative.py
│   │   # Narrative synthesis engine
│   │   # Converts numerical contributions into
│   │   # structured human-readable explanations
│   │
│   └── counterfactuals.py
│       # Counterfactual intervention logic
│       # Tests small, realistic changes to
│       # controllable features and ranks leverage
│   
│     
│
├── data/
│   └── HR-Employee-Attrition.csv
│       # Original dataset used for training and analysis
│
├── models/
│   └── attrition_model.joblib
│       # Trained interpretable model
│
├── reports/
│   └── narratives/
│       # (Optional) Exported narrative reports
│
├── requirements.txt
│   # Python dependencies
│
└── README.md
    # Project documentation and conceptual explanation
```

---

## Structural Design Rationale

* **`app/`**
  Contains only presentation logic.
  No modeling decisions are hidden in the UI.

* **`src/`**
  Holds all analytical logic, making the system:

  * testable
  * reusable
  * auditable

* **Narrative logic is isolated**
  (`narrative.py`) so explanations are:

  * deterministic
  * inspectable
  * decoupled from modeling

* **Counterfactual reasoning is explicit**
  (`counterfactuals.py`) instead of embedded in UI logic.

This separation reinforces the project’s core principle:

> **Interpretability is an architectural decision, not a post-hoc feature.**

---

## Application Walkthrough & Visual Explanations

This section documents the core views of the **Exit Narrative Generator** using real screenshots from the Streamlit application.
Each view is explained not as a UI demo, but as a **decision system** that transforms attrition data into interpretable narratives and actionable counterfactuals.

---

## Narrative Report, From Probability to Story

<img width="1318" height="431" alt="Screenshot 2025-12-18 at 02-40-38 Exit Narrative Generator" src="https://github.com/user-attachments/assets/14990d93-d647-4416-bf05-06687cd6fd9d" />

### What this view represents

The **Narrative Report** is the heart of the system.
Instead of stopping at *“P(exit) = 0.727”*, the model translates statistical pressure into **human-readable reasoning**.

This view answers:

* *Is attrition sudden or accumulated?*
* *Which forces are actively pushing the employee out?*
* *Which anchors are slowing that exit, even if they are insufficient?*

### Key concepts explained

* **Exit Probability**
  A calibrated ML probability, used only as a *signal*, not a prediction.

* **Exit Narrative**
  A synthesized explanation describing how pressure accumulates over time
  (overtime → fatigue → reduced recovery → rational exit).

* **Staying Narrative**
  The counter-force story: what still ties the employee to the organization, and why those anchors may fail under sustained pressure.

This reframes attrition as a **process**, not an event.

---

## Dominant Pressures vs Retention Anchors

<img width="1108" height="207" alt="Screenshot 2025-12-18 at 02-41-00 Exit Narrative Generator" src="https://github.com/user-attachments/assets/3c15c17f-d3ba-492e-925b-6f5b411b1b62" />

---

<img width="1110" height="203" alt="Screenshot 2025-12-18 at 02-41-11 Exit Narrative Generator" src="https://github.com/user-attachments/assets/f18d7c23-9df9-4674-9357-4a30ec881125" />

---

### Why this decomposition matters

Most attrition dashboards list features.
This system **separates forces by direction**:

* **Dominant Pressures** → factors increasing exit likelihood
* **Retention Anchors** → stabilizers resisting exit

### How to read these charts

* Bar length = magnitude of contribution (log-odds space)
* Direction matters more than absolute value
* A strong anchor does *not* guarantee retention if opposing forces are stronger

This mirrors real systems: **stability fails when opposing forces overwhelm buffers**.

---

## Peer Context, Relative, Not Absolute Risk

<img width="1096" height="535" alt="Screenshot 2025-12-18 at 02-41-48 Exit Narrative Generator" src="https://github.com/user-attachments/assets/2fa97c8d-ae71-48ae-8c60-4f34b535acc6" />

### What this view answers

Attrition risk is meaningless without context.

This panel compares the selected employee **only against true peers**:

* Same department
* Same job role
* Same job level (when available)

### Why percentiles matter

An employee can:

* Have *high exit risk* but still be *more stable than peers*
* Or have *moderate risk* but be an *outlier within their cohort*

This avoids false alarms caused by population-wide pressure.

---

## Intervention Builder, Counterfactual Levers

<img width="1096" height="564" alt="Screenshot 2025-12-18 at 02-44-10 Exit Narrative Generator" src="https://github.com/user-attachments/assets/2101bc8d-4f88-445b-9b28-91e22803fe1c" />

### What this tool does (and does NOT do)

This is **not a simulator of the future**.
It is a **counterfactual search engine**.

The system asks:

> “If I could change *one thing*, which change reduces exit pressure the most?”

### Output interpretation

* Each row is a *single-step intervention*
* Ranked by **Δ exit probability**
* Reveals **leverage**, not certainty

This allows leaders to act where effort produces **maximum stability gain**.

---

## Manual What-If, Human-Driven Exploration

<img width="1114" height="548" alt="Screenshot 2025-12-18 at 02-45-07 Exit Narrative Generator" src="https://github.com/user-attachments/assets/0e434b73-156a-4baf-bbc0-0e86551e84da" />

### Why this exists

Not all decisions should be automated.

This panel lets humans:

* Adjust levers manually
* Observe how probability responds
* Develop intuition about pressure sensitivity

It turns the model into a **thinking tool**, not a black box.

---

## Why This System Is Different

Traditional attrition models answer:

> “Who will leave?”

**Exit Narrative Generator answers:**

* *Why leaving becomes rational*
* *Which forces matter most*
* *Where intervention still works*
* *When optimization is already too late*

It treats attrition as:

* A **dynamic system**
* Governed by **pressure accumulation**
* Stabilized by **buffers**
* Explained through **narratives**, not labels

---

## 1. The Central Claim

Attrition is not an outcome.
Attrition is a **transition**.

Most HR analytics systems fail because they treat resignation as a binary label instead of the **final observable moment of a long, invisible process**.

This project is built on one foundational claim:

> **By the time attrition is predicted with confidence, the system has already failed.**

The Exit Narrative Generator focuses on the **pre-collapse phase**, the period where:

* pressure accumulates
* buffers erode
* recovery time disappears
* leaving becomes psychologically rational

---

## 2. Why Prediction Is the Wrong Abstraction

Prediction assumes:

* the system is stationary
* interventions do not change dynamics
* accuracy improves decision quality

In reality:

* employees adapt
* managers react
* incentives shift
* culture responds

This makes attrition **reflexive**, not predictive.

Therefore, this system replaces:

> *“Who will leave?”*
> with
> **“Why does leaving make sense *now*?”**

---

## 3. Attrition as a Pressure, Buffer System

The Exit Narrative Generator models attrition as a **force balance**, not a probability:

```
Accumulated Exit Pressure
Remaining Retention Anchors
= Net Instability
```

### Exit Pressure Builds From:

* sustained overtime
* role life conflict
* stalled progression
* social isolation
* repeated identity resets (job changes)
* commute friction
* emotional exhaustion

### Retention Anchors Resist Through:

* income security
* tenure inertia
* age-related risk aversion
* role familiarity
* geographic stability
* residual satisfaction pockets

Attrition does not occur when pressure exists.
It occurs when **anchors can no longer compensate**.

---

## 4. Narrative Report: Explaining a Single Exit Trajectory

This is the primary interpretive view of the system.

### What This View Is For

* understanding *why* an employee is at risk
* explaining decisions to managers
* reconstructing failures after the fact
* learning which pressures matter structurally

### What This View Is Not For

* firing decisions
* automated interventions
* ranking employees

### Key Elements Explained

#### Exit Probability

A **directional signal**, not a promise.
It answers:

> *“Is pressure currently dominating anchors?”*

#### Narrative Headline

A qualitative state descriptor:

* “Exit narrative is forming”
* “Exit pressure dominates anchors”
* “Stability is fragile but intact”

This prevents false certainty.

#### Exit Narrative

A **pressure-centric explanation**, describing:

* how multiple weak signals aligned
* how recovery capacity eroded
* why continuing to stay feels increasingly irrational

This is not generated by an LLM.
It is built from deterministic mappings between feature contributions and narrative templates.

#### Staying Narrative

A **buffer-centric explanation**, describing:

* what is still delaying exit
* why the employee has not yet left
* which anchors are weakening fastest

This avoids the false assumption that non-exit equals health.

---

## 5. Separating Forces: Why This Matters

Most explainability tools rank features by importance.
This system **separates them by direction**.

### Dominant Pressures

These actively push the system toward exit:

* chronic overtime
* poor work life balance
* relationship dissatisfaction
* promotion stagnation
* frequent employer changes

These are **accelerants**, not triggers.

### Retention Anchors

These slow exit but rarely reverse it:

* income relative to peers
* age-related stability
* tenure inertia
* geographic proximity
* role familiarity

Anchors delay collapse they do not prevent it.

This separation mirrors how humans reason:

> *“I know I should leave... but not yet.”*

---

## 6. Peer Context: Why Absolute Metrics Lie

A salary number is meaningless without context.
So is satisfaction.
So is tenure.

Attrition is **relative instability**, not absolute dissatisfaction.

### What Peer Context Does

* defines a **local comparison group**
* normalizes metrics within role + department + level
* converts raw values into deviations

### Questions This View Answers

* Is this employee underpaid *for their role*?
* Is promotion delay structural or personal?
* Is dissatisfaction unique or systemic?

Without peer context, narratives become misleading.

---

## 7. Intervention Builder: Counterfactual Reasoning, Not Promises

The Intervention Builder does **not** suggest policies.
It tests **single-step counterfactuals**.

### Why Single-Step Matters

Large hypothetical changes:

* break realism
* hide leverage
* create false hope

Small changes reveal:

* sensitivity
* leverage points
* asymmetries

### Automatic Intervention Search

The system:

1. Perturbs one controllable variable
2. Recomputes exit pressure
3. Ranks changes by impact efficiency

This answers:

> *“What is the cheapest stabilizing action?”*

### Manual What-If Testing

Users can manually adjust:

* overtime
* satisfaction dimensions
* training exposure
* work life balance

This enables:

* manager-level reasoning
* policy stress-testing
* assumption validation

---

## 8. Why This Is Not an Optimization Engine

Optimization assumes:

* objectives are known
* constraints are stable
* systems respond linearly

Human systems do not.

This project intentionally avoids:

* automated recommendations
* global optimization
* KPI-driven control loops

Because optimization often **borrows stability from the future**.

---

## 9. Technical Transparency

### Model Choice

* Logistic regression
* No hidden layers
* No embeddings
* No post-hoc explainers

### Why This Matters

* coefficients map directly to narratives
* explanations are stable
* behavior is reproducible
* reasoning is inspectable

This is not a performance race.
It is an **epistemic choice**.

---

## 10. Failure Is Visible Before It Is Measured

The Exit Narrative Generator operationalizes a simple but neglected truth:

> **By the time metrics collapse, the system has already crossed its point of no return.**

This tool exists to surface:

* early pressure alignment
* anchor erosion
* narrative inevitability

Before resignation becomes inevitable.

---

## 11. Who This Project Is For

* HR teams tired of dashboards without meaning
* Managers seeking explanations, not alerts
* Data scientists building interpretable systems
* Researchers studying failure as a process
* Anyone skeptical of prediction-first thinking

This is not HR analytics.
This is **systems analysis applied to human behavior**.
