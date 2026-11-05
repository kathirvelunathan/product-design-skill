# Spec-Driven Product Design Framework (SDPF) for Kiro & Claude Code Factory

A specification-driven product design framework for enterprise banking environments. This framework transitions Product Owners (POs) from PowerPoint slides and loose Word documents into version-controlled **GitLab Markdown artifacts (Roadmap as Code & Spec as Code)**.

The resulting **Product Specification Bundle (PSB)** produces deterministic, machine-verifiable requirements ready for automated ingestion by downstream **Claude High-Level Design (HLD)** and **Test-Driven Development (TDD) Code Generation Agents**.

---

## 1. Operating Architecture & Granularity Split

To prevent context bloat and ambiguity, requirements are strictly divided into **Macro-Context (Epic Level)** and **Micro-Execution (Feature Level)**:

```text
product-design-skill/
├── .kiro/
│   └── skills/                                  # Active Kiro Skills (Interactive Agents)
│       ├── strategic-horizons-roadmapper.md
│       ├── business-hypothesis-definer.md
│       ├── epic-business-decomposer.md
│       ├── executive-presenter-transformer.md
│       ├── psb-bundle-scaffolder.md
│       ├── feature-scaffolder.md
│       ├── conceptual-model-shaper.md
│       ├── governance-approvals-shaper.md
│       ├── product-design-lens-shaper.md
│       ├── spec-by-example-contract-builder.md
│       └── spec-linter-evaluator.md
│
├── templates/
│   └── psb/                                     # Reusable Blank Starter Schemas
│       ├── epic/
│       │   ├── 00-strategy.md                   # Commercial hypothesis & KPIs
│       │   ├── 01-capability.md                 # Scope boundaries & feature breakdown
│       │   ├── 02-conceptual.md                 # Ubiquitous domain lexicon & OOUX object map
│       │   └── 04-governance.md                 # PRA/FCA mandates, SMCR sign-off & DPIA
│       └── feature/
│           ├── 02-statechart.md                 # Finite state machine, transitions & guards
│           ├── 03-lenses.md                     # Failure modes, blast radius & telemetry
│           └── 05-contracts.md                  # Interface schemas & Given-When-Then tables
│
└── docs/                                        # Working Project Artifacts
    ├── roadmap/
    │   └── ROADMAP.md                           # 3-Year Strategic Horizon Roadmap
    └── specs/
        └── EPIC-104-party-resolution/           # Populated Epic-Level Bundle
            ├── 00-strategy.md
            ├── 01-capability.md
            ├── 02-conceptual.md
            ├── 04-governance.md
            └── features/
                ├── FEAT-01-exact-matching/      # Populated Feature-Level Bundle
                │   ├── 02-statechart.md
                │   ├── 03-lenses.md
                │   └── 05-contracts.md
                └── FEAT-02-quarantine-workflow/
                    ├── 02-statechart.md
                    ├── 03-lenses.md
                    └── 05-contracts.md
