---
epic_id: "EPIC-[ID]"
jira_key: "[JIRA-KEY]"
title: "[Business Capability Title]"
initiative_ref: "INIT-[ID]"
target_increment: "YYYY-QX"
business_lead: "@[po-handle]"
status: "Draft | Under Review | Ready for Feature Scaffolding"
last_updated: "YYYY-MM-DD"
---

# 1. Epic Overview & Scope Boundaries
[Comprehensive summary of the operational capability being introduced in strictly business and domain terms.]

## In-Scope Business Capabilities
- [Capability 1]
- [Capability 2]
- [Capability 3]

## Out-of-Scope (Explicit Boundaries)
- [Explicitly excluded scope 1]
- [Explicitly excluded scope 2]

---

# 2. Capability Slicing & Child Features

### Feature 1: `FEAT-01-[slug]` — [Feature Title]
- **Summary:** [1-sentence summary of the vertical business capability slice]
- **Business Value Statement:**
  - *As a:* [Business User / Operational Persona / Downstream Domain]
  - *I want:* [Operational capability]
  - *So that:* [Quantifiable business outcome]
- **Business Acceptance Criteria (BAC):**
  1. **Nominal Rule:** [Standard deterministic business condition that must be met]
  2. **Boundary / Exception Rule:** [What happens when validation fails, thresholds are breached, or data is missing]
  3. **Audit / Regulatory Rule:** [What regulatory trace, immutable log, or state record must be preserved]

### Feature 2: `FEAT-02-[slug]` — [Feature Title]
- **Summary:** [1-sentence summary of the vertical business capability slice]
- **Business Value Statement:**
  - *As a:* [Business User / Operational Persona / Downstream Domain]
  - *I want:* [Operational capability]
  - *So that:* [Quantifiable business outcome]
- **Business Acceptance Criteria (BAC):**
  1. **Nominal Rule:** [Standard deterministic business condition that must be met]
  2. **Boundary / Exception Rule:** [What happens when validation fails, thresholds are breached, or data is missing]
  3. **Audit / Regulatory Rule:** [What regulatory trace, immutable log, or state record must be preserved]

---

# 3. Handoff Checklist for Feature Refinement & Claude HLD Agent
- [ ] Zero technical solutioning or premature tech-stack terms (no Kafka, MongoDB, AWS, etc.).
- [ ] Ubiquitous banking domain terminology used consistently with `02-conceptual.md`.
- [ ] Every child feature represents an independently testable vertical capability slice.
- [ ] Every child feature defines complete Business Acceptance Criteria (Nominal, Boundary/Exception, Audit).
