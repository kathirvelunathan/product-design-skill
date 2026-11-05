---
feature_id: "FEAT-[ID]"
parent_epic: "EPIC-[ID]"
target_entity: "[e.g., PartyLinkage | TransactionMatch | CustomerProfile]"
initial_state: "[e.g., INGESTED]"
terminal_states:
  - "[e.g., LINKED]"
  - "[e.g., REJECTED]"
  - "[e.g., PURGED]"
status: "Draft | Under Review | Approved"
last_updated: "YYYY-MM-DD"
---

# 1. Statechart Visualization (Mermaid.js)
> Use native Mermaid `stateDiagram-v2` so it renders directly in GitLab and Kiro.

```mermaid
stateDiagram-v2
    [*] --> Ingested: Record Received

    Ingested --> ExactMatched: Confidence >= 95%
    Ingested --> AmberQuarantined: Confidence 70-94%
    Ingested --> Rejected: Confidence < 70%

    AmberQuarantined --> ApprovedByOps: Four-Eyes Sign-Off
    AmberQuarantined --> Rejected: Manual Discard / Timeout

    ApprovedByOps --> ExactMatched: Commit Link
    ExactMatched --> Linked: Ledger Entry Created
    Linked --> Suspended: AML/Compliance Hold

    Suspended --> Linked: Clearance Token Received
    Suspended --> Rejected: Blocked Entity

    Rejected --> [*]
    Linked --> [*]
