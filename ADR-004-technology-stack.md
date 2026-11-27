# ADR-004: Adopt a Free TypeScript-Based Technology Stack

- **Status:** Accepted
- **Date:** 2026-11-10
- **Project:** FASTBite
- **Related drivers:** ASR-01 (performance and update visibility); ASR-02/ASR-03 (data integrity); maintainability; zero-budget academic-project constraint; ChatGPT-assisted development

## Context

The project has no development or infrastructure budget and will be built as a university prototype with substantial ChatGPT assistance. The team has no mandated programming language or framework. The stack should be free, commonly documented, practical for a student team, and compatible with the approved modular-monolith and SQL decisions.

The project does not need paid hosting, commercial banking APIs, or production payment services to demonstrate the agreed product workflows.

## Options considered

1. **React + TypeScript / Express + TypeScript / PostgreSQL / Prisma:** A widely used web stack with one language across client and server, a relatively small backend framework, and relational persistence.
2. **React + TypeScript / NestJS + TypeScript / PostgreSQL / Prisma:** Provides more built-in backend structure and conventions, but introduces more framework concepts and ceremony for this project's current scope.
3. **Python backend (Django or FastAPI) with a JavaScript frontend:** Also viable and well documented, but requires the team to work across two programming languages and their tooling.

## Decision

Use the following free/open-source stack for the initial academic implementation:

- **Frontend:** React + TypeScript + Vite
- **Styling:** Tailwind CSS
- **Backend:** Node.js + Express + TypeScript
- **Database:** PostgreSQL
- **ORM and migrations:** Prisma
- **HTTP interface:** REST
- **Server-to-client updates:** Server-Sent Events (SSE) where needed for order/status updates

Use local development by default. Any optional hosting must have a free tier and must not be a required architectural dependency.

## Rationale

TypeScript can be used across frontend and backend, reducing language switching and making shared types and validation patterns easier to understand. Express has a smaller learning curve and less framework overhead than a more opinionated backend framework. PostgreSQL matches the relational and transactional needs. Prisma provides a consistent schema and migration workflow. The selected tools are free/open source and suitable for local development.

REST handles commands and queries. SSE is a simple one-way mechanism for delivering server-originated status updates; the persisted database state remains authoritative and clients must refresh after reconnecting.

## Consequences

- **Positive:** No license cost; one main programming language; broad learning resources; manageable local development; fits the modular monolith.
- **Negative:** The team must establish its own Express module conventions; TypeScript and Prisma still require learning; SSE reconnect behavior must be handled.
- **Risk:** Free-tier hosting, if used, may have sleep, capacity, or availability limits. Performance claims must be based on tests in the actual demonstration environment.
- **Revisit when:** A course constraint, team capability, measured performance issue, or genuinely necessary integration justifies a stack change.

## Verification

Confirm that the repository uses the approved tools and can be run locally without paid accounts. Review module boundaries in Express. Verify Prisma migrations and PostgreSQL setup. Test REST operations and SSE reconnection/status refresh behavior if SSE is implemented.

## AI-agent instruction derived from this ADR

> Use React, TypeScript, Vite, Tailwind CSS, Node.js, Express, PostgreSQL, and Prisma. Do not introduce a paid service, framework replacement, database, message broker, or infrastructure platform without presenting alternatives and obtaining human approval. Keep the project runnable locally.


## Working-baseline clarification (15 November 2026)

The TA-correction PRD does not require a change to the accepted technology stack. The internal demo bank simulator, staff permissions, audit records, retention job, and order-decision deadlines can be implemented within the existing React/TypeScript + Express/TypeScript + PostgreSQL/Prisma modular monolith. Do not add a banking SDK, external OTP service, paid email/SMS provider, Redis, queue, or additional database for the demo workflow.
