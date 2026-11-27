# ADR-001: Adopt a Modular Monolith

- **Status:** Accepted
- **Date:** 2026-11-10
- **Project:** FASTBite
- **Related drivers:** ASR-01 (performance and status visibility); ASR-02 (order and transaction integrity); ASR-03 (cross-module consistency); academic-project cost and operational constraints

## Context

FASTBite has distinct business responsibilities for identity, customers, menu, inventory, ordering, wallets, refunds, receipts, notifications, reporting, and owner-only bank-connection demonstration. The team is building a university project with no project budget and expects to use ChatGPT-assisted development. The architecture must preserve meaningful boundaries without requiring the team to operate distributed infrastructure.

The PRD's order, stock, wallet, and refund consistency requirements do not demonstrate a need for independent service deployment. The academic prototype also does not require independent release cycles or separate scaling of business capabilities.

## Options considered

1. **Unstructured monolith:** One deployable application with few explicit module boundaries. Simple to deploy, but responsibilities and dependencies can become tangled.
2. **Modular monolith:** One backend deployment with explicit business modules and defined interfaces. Requires internal design discipline while keeping deployment simple.
3. **Microservices:** Separately deployed services, potentially with separate data stores. Offers independent deployment but adds networking, monitoring, distributed-data, and operational overhead.

## Decision

Use a **modular monolith** with one frontend application, one backend deployment, and one relational database. Backend modules must have clear responsibilities and public interfaces. A module must not access another module's private internals or directly manipulate its private tables.

## Rationale

This fits the project's current scale, zero-budget constraint, team capacity, and need for reliable multi-record operations. It keeps the architecture understandable for the team and an AI coding agent while preserving separation of concerns. There is no ASR demonstrating a current need for microservices.

## Consequences

- **Positive:** Simpler local development and deployment; lower infrastructure cost; easier initial testing; simpler transactional consistency.
- **Negative:** Backend modules deploy together; independent scaling and release are limited.
- **Risk:** Module boundaries may erode if developers import private internals or write directly to another module's tables.
- **Revisit when:** Measured workload, team organization, or a genuine independent deployment requirement justifies distribution complexity.

## Verification

Review the proposed directory structure and dependency direction. Confirm that business modules use documented interfaces and remain in one backend deployment. Reject unjustified separately deployed services.

## AI-agent instruction derived from this ADR

> Preserve the modular monolith. Do not introduce microservices, an API gateway, service orchestration, or distributed infrastructure without an ASR-based justification, a proposed ADR, and explicit human approval.


## Working-baseline clarification (15 November 2026)

The TA-correction decisions do not change the modular-monolith decision. The Bank Integration Adapter, Staff Access, Refunds, and Reporting/Audit remain internal modules in the same backend deployment. Independent unavailable-item deadlines, demo bank operations, wallet/refund ledger updates, and audit writes are coordinated through application interfaces and PostgreSQL transactions/idempotency; they are not reasons to introduce microservices, a scheduler service, or a message broker for this academic prototype. Use a simple persisted deadline checked by server-side application logic unless a later measured need and approved ADR justify additional infrastructure.
