# EAGLES Kickoff - LAHCEN

## Assigned Microservice: [5.2] Candidate Evaluation

**Repo**: [rh-optimerp-candidate-evaluation](https://github.com/ERP-CORE-DEV/rh-optimerp-candidate-evaluation)
**Syncs with**: HATIM (5.1 Sourcing) upstream, HOUSSINE (5.3 Hiring) downstream

---

## Phase 1 - Plan (uses 1 planner agent, isolated context)
```
/plan candidate-evaluation microservice - Controller-Service-Repository, .NET 8, CosmosDB SDK 3.54, React 18 + Ant Design, French HR compliance (grilles d'evaluation, scoring objectif, entretiens structures, non-discrimination). Reference: rh-optimerp-sourcing-candidate-attraction repo.
```

## Phase 2 - Scaffold (after plan approval)
```
/scaffold candidate-evaluation
```

## Phase 3 - TDD first feature
```
/tdd candidate-scoring-engine
```

## Phase 4 - Pre-PR validation
```
/code-review
/security-scan
/gdpr-check
```

---

## Key Rules
- **Pattern**: Controller-Service-Repository (NOT CQRS/MediatR)
- **Database**: CosmosDB SDK 3.54 direct (NOT EF Core)
- **GDPR**: AnonymizeXxx() on personal data models + IsAnonymized flag
- **French HR**: Grilles d'evaluation, entretiens structures, scoring objectif, non-discrimination
- **Tests**: xUnit + FluentAssertions + Moq, minimum 80% coverage
- **Commits**: Conventional commits (feat/fix/refactor/test/docs)
- **Integration dependencies**: Watches [5.1] Sourcing & Candidate Attraction and [5.3] Hiring Management

## Reference Repo
Use [rh-optimerp-sourcing-candidate-attraction](https://github.com/ERP-CORE-DEV/rh-optimerp-sourcing-candidate-attraction) as the architecture reference.
