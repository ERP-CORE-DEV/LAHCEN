# Training & Skill Development — First Eagles Request (Brainstorming)

**Developer**: LAHCEN
**Microservice**: Training & Skill Development (DAT 5.7)
**Date**: 2026-02-22
**Session**: First team live development session

---

## Eagles Skill to Execute

```
/gsd-plan
```

## Full Prompt (copy-paste into Claude Code)

```
/gsd-plan Training & Skill Development microservice (DAT 5.7) — Brainstorming + Phased Roadmap

== IDENTITY ==
Developer: LAHCEN
Microservice: Training & Skill Development
Namespace: TRAINING.AND.SKILL.DEVELOPMENT
DAT: 5.7 | Watching: 5.6, 5.8
Repo: rh-optimerp-training-and-skill-development (greenfield — no src/ yet)

== AZURE RELEASE CONSTRAINT ==
A first release of RH-OptimERP is already deployed in Azure (AKS + CosmosDB + ACR + Helm).
Every phase MUST produce artifacts deployable to this existing Azure environment.
Backend APIs must be callable. Frontend pages must be visible and functional.

== TECH STACK (from INSTRUCTIONS.md) ==
Backend: .NET 8 (ASP.NET Core Web API) + CosmosDB SDK 3.54 (direct, NOT EF Core)
Frontend: React 18 TypeScript + Ant Design 5.14 + Redux Toolkit
Infra: Azure AKS + ACR + Key Vault + Helm
CI/CD: Azure Pipelines (ELYSTEK org)
Pattern: Controller-Service-Repository (NOT CQRS/MediatR)
Domain: French HR (SMIC, CPF, OPCO, RNCP, CNIL, GDPR)

== PHASED PLAN (brainstorm these) ==

WAVE 1 — Foundation (parallel tasks):
  Phase 1a: /scaffold-microservice TrainingAndSkillDevelopment
            --entities=Training,Skill,Certification,TrainingPlan,TrainingSession,SkillAssessment
            --port=5007 --with-gdpr --with-tests
  Phase 1b: /init-project (local dev: docker-compose, appsettings.Development.json)
  Phase 1c: /update-docs official --preview (plan documentation structure)

WAVE 2 — Domain Models + Database (parallel tasks):
  Phase 2a: Domain entities with French HR compliance (CPF eligibility, OPCO codes, RNCP certifications)
  Phase 2b: CosmosDB containers + partition key strategy per entity
  Phase 2c: DTOs with static ToDomain() / FromDomain()
  Phase 2d: /update-docs diagrams (Eraser.io: System Context C4 L1 + Data Model ERD)

WAVE 3 — API Layer (parallel tasks):
  Phase 3a: Controllers with CRUD + business endpoints (/api/v1/{resource})
  Phase 3b: Services with business logic + FluentValidation
  Phase 3c: Repositories with CosmosDB SDK 3.54 direct mode
  Phase 3d: /update-docs diagrams (Eraser.io: Component C4 L3 + API Flow Sequence)

WAVE 4 — Frontend (parallel tasks):
  Phase 4a: React pages per entity (list, detail, create, edit)
  Phase 4b: Redux Toolkit slices + API integration
  Phase 4c: Ant Design 5.14 components + French locale
  Phase 4d: /update-docs diagrams (Eraser.io: Container C4 L2)

WAVE 5 — Quality + Integration:
  Phase 5a: /tdd for each service (xUnit + FluentAssertions + Moq)
  Phase 5b: /french-hr-validate (CPF, OPCO, RNCP compliance check)
  Phase 5c: /contract-test for inter-service APIs (5.6, 5.8)
  Phase 5d: /update-docs diagrams (Eraser.io: Deployment + Security Flow)

WAVE 6 — Deploy + Documentation:
  Phase 6a: /helm-deploy to existing Azure AKS release
  Phase 6b: /create-azure-pipeline for CI/CD
  Phase 6c: /update-docs all --force (FULL doc generation: 5 agents, 8 diagrams, HTML site)
  Phase 6d: /gsd-verify (final validation against all requirements)

== MANDATORY RULES FOR EVERY PHASE ==
1. Use Eagles /skill for every action (never freeform code)
2. /update-docs diagrams after every wave (Eraser.io C4/Arc42 diagrams — MANDATORY)
3. Documentation = modern HTML (Tailwind + glassmorphism + dark mode) as in eagles-claude-config/docs/
4. Every phase has: verify command (dotnet build / npm run build) + done criteria
5. Track progress in .planning/STATE.md after every wave
6. Use team-sync MCP to check integration impact before cross-service changes

== EXPECTED OUTPUT ==
.planning/PROJECT.md      — Vision, scope, entity definitions
.planning/REQUIREMENTS.md — Acceptance criteria per entity
.planning/ROADMAP.md      — 6 waves with parallel phases (XML format for Claude)
.planning/STATE.md        — Progress tracker (empty, ready for /gsd-execute)
```

---

## Eagles Micro-Step Workflow (after brainstorming)

| Step | Eagles Command | Purpose |
|------|---------------|---------|
| 1 | `/gsd-plan` | Brainstorming + phased roadmap |
| 2 | `/gsd-execute phase-1a` | Scaffold microservice |
| 3 | `/gsd-execute phase-1b` | Local dev environment |
| 4 | `/gsd-execute phase-1c` | Preview docs structure |
| 5 | `/update-docs diagrams` | First Eraser.io diagrams |
| 6 | `/gsd-execute phase-2a` | Domain models |
| 7 | `/gsd-execute phase-2b` | CosmosDB design |
| 8 | `/gsd-execute phase-2c` | DTOs |
| 9 | `/update-docs diagrams` | ERD + System Context diagrams |
| 10 | `/gsd-execute phase-3a` | Controllers |
| 11 | `/gsd-execute phase-3b` | Services |
| 12 | `/gsd-execute phase-3c` | Repositories |
| 13 | `/update-docs diagrams` | Component + API Flow diagrams |
| 14 | `/gsd-execute phase-4a` | React pages |
| 15 | `/gsd-execute phase-4b` | Redux slices |
| 16 | `/gsd-execute phase-4c` | Ant Design components |
| 17 | `/update-docs diagrams` | Container diagram |
| 18 | `/tdd` | Tests per service |
| 19 | `/french-hr-validate` | CPF/OPCO/RNCP compliance |
| 20 | `/contract-test` | Inter-service contracts |
| 21 | `/update-docs diagrams` | Deployment + Security diagrams |
| 22 | `/helm-deploy` | Deploy to Azure AKS |
| 23 | `/create-azure-pipeline` | CI/CD pipeline |
| 24 | `/update-docs all --force` | Full HTML docs + all 8 Eraser.io diagrams |
| 25 | `/gsd-verify` | Final validation |
| 26 | `/gsd-progress` | Status check anytime |

**Every single step is an Eagles skill. Zero freeform prompting.**

---

## Documentation Pipeline (dispatches 5 agents)

```
/update-docs all
  |— doc-hub-architect     -> docs/INDEX.md
  |— doc-official-writer   -> docs/project/ (11 Diataxis + Arc42 + Stripe docs)
  |— doc-code-analyst      -> docs/code/ (13 Rust Book progressive teaching docs)
  |— doc-diagram-artist    -> docs/diagrams/ (8 Eraser.io C4/Arc42 diagrams)
  |— doc-orchestrator      -> Cross-links + verification
```

### Eraser.io Diagrams (mandatory — 8 total)

| # | Diagram | C4/Arc42 Level | Used In |
|---|---------|---------------|---------|
| 1 | System Context | C4 L1 | OVERVIEW + INDEX |
| 2 | Container | C4 L2 | ARCHITECTURE |
| 3 | Component | C4 L3 | ARCHITECTURE |
| 4 | Data Model (ERD) | Arc42 S5 | DATA-MODEL |
| 5 | API Flow (Sequence) | Arc42 S6 | API-REFERENCE |
| 6 | Deployment | Arc42 S7 | DEPLOYMENT |
| 7 | Security Flow | Arc42 S8 | SECURITY |
| 8 | Data Flow | Arc42 S6 | DATA-FLOW |
