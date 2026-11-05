---
feature_id: "FEAT-[ID]"
parent_epic: "EPIC-[ID]"
title: "[Feature Title - System & Operational Lenses]"
status: "Draft | Under Review | Approved"
last_updated: "YYYY-MM-DD"
---

# System & Operational Lenses (6 Non-Negotiable Dimensions)

## 1. Temporal & Lifecycle Lens
- **Birth / Creation Trigger:** [How is the record or workflow instance created?]
- **Mutation & Out-of-Order Rules:** [Can updates arrive out of sequence? Which timestamp wins (event time vs. ingestion time)?]
- **Pause / Quarantine Rules:** [How long can an item sit in a paused/quarantined state before SLA escalation?]
- **Archival & Purge Invariant:** [Exact retention duration and automated GDPR/PRA purge behavior.]

---

## 2. Premortem & Failure Modes Lens
- **Upstream Dependency Failure:** [What happens if the upstream feed sends malformed batches or stalls?]
- **Downstream / External Dependency Outage:** [If an external validation service or ledger freezes for 3 hours, do we fail closed, serve cached state, or queue asynchronously?]
- **Partial Failure & Compensation:** [How are half-completed multi-step operations rolled back or compensated?]

---

## 3. Actor & Intent (Bad Actors) Lens
- **Internal Misuse / Human Error:** [Protection against rapid double-clicks, self-approval bypasses, or bulk unverified overrides.]
- **External / Hostile Input:** [Protection against payload injection, enumeration attacks, or malformed identifier spamming.]
- **Privilege & Segregation of Duties:** [Four-eyes verification or role-based execution constraints.]

---

## 4. Cost & Blast Radius Lens
- **Payload & Batch Ceilings:** [Maximum request size, batch count, or pagination limits.]
- **Rate Limiting & Throttling:** [Maximum sustained and burst throughput per caller/tenant before backpressure engages.]
- **Isolation Boundary:** [How do we prevent a runaway query or poison message in this feature from starving shared platform resources?]

---

## 5. Feedback Loop & Observability Lens
- **Primary Business Heartbeat Metric:** [The single real-time metric proving this feature is delivering business value.]
- **Operational SLA / SLO Targets:** [e.g., 99.9% of nominal records processed within < 500ms.]
- **Automated Alerting Triggers:**
  - **P1 (Critical Wake-Up):** [Exact threshold, e.g., Dead-letter queue > 50 records in 5 minutes or 0 heartbeats during banking hours.]
  - **P2 (Degraded Performance):** [Exact threshold, e.g., Quarantine fallout rate spikes > 25% over rolling 1-hour window.]

---

## 6. Reversibility & Experimentation Lens
- **Kill-Switch / Feature Flag:** [How can this feature be disabled at runtime in < 60 seconds without a redeploy?]
- **Data Rollback Protocol:** [If a defect silently corrupts records on Day 2, how do we replay or reverse mutations without losing valid transactions?]
- **Dark-Launch / Canary Strategy:** [How will this slice be validated in shadow mode or with a 1% cohort before full cutover?]
