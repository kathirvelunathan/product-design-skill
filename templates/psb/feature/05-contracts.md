---
spec_id: "SPEC-[EPIC_ID]-[FEAT_ID]"
feature_id: "FEAT-[ID]"
parent_epic: "EPIC-[ID]"
title: "[Feature Title - Executable Contracts & Spec-by-Example]"
data_classification: "Internal | Confidential | Restricted - Banking PII"
regulatory_jurisdiction: "FCA / PRA / UK GDPR"
status: "Draft | Ready for HLD & TDD Agent"
last_updated: "YYYY-MM-DD"
---

# 1. Interface & Data Contract Schema

```yaml
Contract:
  name: "[Command / Event / API Contract Name]"
  type: "event_or_api_payload"
  version: "1.0.0"
  idempotency_key: "request_id"
  fields:
    request_id:
      type: uuid
      nullable: false
      pii_tier: Non_PII
      description: "Unique idempotency identifier for the operation"
    party_id:
      type: uuid
      nullable: false
      pii_tier: Tier_1_Direct
      retention_policy: "7_YEARS_POST_TERMINATION"
      description: "Immutable internal party identifier"
    company_reg_number:
      type: string
      format: "UK_CRN_8_CHARS"
      nullable: false
      pii_tier: Non_PII
      validation: "^[A-Z0-9]{8}$"
      description: "8-character UK Companies House registration number"
    match_confidence:
      type: decimal
      range: [0.00, 1.00]
      nullable: false
      pii_tier: Non_PII
      description: "Normalized entity resolution confidence score"
```

---

# 2. Field-Level PII & Governance Traceability
> Every PII field must correlate to a retention policy and security invariant declared in the parent Epic's `04-governance.md`.

| Field Name | Data Type | Nullable | PII Classification Tier | Masking / Encryption Invariant | Retention Policy |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `request_id` | `uuid` | `false` | `Non-PII` | Cleartext allowed in structured logs | 90 days operational log |
| `party_id` | `uuid` | `false` | `Tier 2 - Pseudonymous` | Tokenized in external telemetry | 7 years post-termination |
| `company_reg_number` | `string` | `false` | `Non-PII (Corporate)` | Cleartext allowed | 7 years post-termination |
| `[pii_field_name]` | `string` | `false` | `Tier 1 - Direct PII` | Masked (`***`) in all logs; AES-256 at rest | 7 years post-termination |

---

# 3. Executable Spec-by-Example Matrix (Given-When-Then)
> **Linter Requirement:** Every feature contract MUST define at least **1 Nominal (`NOM`)**, **2 Boundary (`BND`)**, and **2 Failure/Error (`ERR`)** scenarios. Downstream TDD agents synthesize unit tests directly from each row.

| Scenario ID | Category | Given (Pre-State & Context) | When (Trigger & Input Payload) | Then (Expected State, Output & Audit Side-Effects) |
| :--- | :--- | :--- | :--- | :--- |
| **NOM-01** | Nominal | `Party` `P-100` exists in `Active` state with CRN `"01234567"`; idempotency key `"req-001"` is unseen. | `MatchRequest` received with `company_reg_number: "01234567"`, `match_confidence: 0.98`. | Transition state to `ExactMatched`; emit `ExactMatchConfirmedEvent`; write immutable audit log. |
| **BND-01** | Boundary | `Party` `P-100` exists; confidence score is at exact lower auto-match boundary (`0.95`). | `MatchRequest` received with `match_confidence: 0.95`. | Transition state to `ExactMatched`; emit `ExactMatchConfirmedEvent`. |
| **BND-02** | Boundary | `Party` `P-100` exists; confidence score is 1 basis point below auto-match threshold (`0.94`). | `MatchRequest` received with `match_confidence: 0.94`. | Transition state to `AmberQuarantined`; enqueue item to Ops Quarantine Queue. |
| **ERR-01** | Failure / Malformed | Any system state; incoming payload has invalid CRN format (`"123"`). | `MatchRequest` received with `company_reg_number: "123"`. | Reject immediately with error code `INVALID_CRN_FORMAT`; do not mutate state; increment validation failure metric. |
| **ERR-02** | Failure / Duplicate | `request_id: "req-001"` was already processed within the 24h idempotency window. | Duplicate `MatchRequest` received with `request_id: "req-001"`. | Return cached prior outcome (`IDEMPOTENT_REPLAY`); zero duplicate state transitions or events emitted. |
