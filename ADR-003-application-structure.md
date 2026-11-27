# ADR-003: Use Three Frontend Panels with One Modular Backend

- **Status:** Accepted
- **Date:** 2026-11-10
- **Project:** FASTBite
- **Related drivers:** ASR-04 (three-panel security and data access); ASR-05 (owner-only financial boundary); maintainability; academic-project simplicity

## Context

The validated PRD defines three distinct user experiences: Student, Cashier / Accountant, and Owner. The Student Panel is customer-facing. The Cashier / Accountant Panel supports permitted operational work but must not expose cafe-wallet finances or bank-connection functions. The Owner Panel includes operational capabilities plus owner-only finance and bank-connection functions.

The team has agreed that these experiences should be implemented as three panels in one frontend application, backed by one modular backend. Separate frontend/backend deployments for each panel would duplicate work and add unnecessary coordination for the academic project.

## Options considered

1. **Three independent applications and backends:** Strong separation at deployment level, but duplicates setup and creates unnecessary API and data coordination.
2. **One frontend with three panel areas and one modular backend:** Shared application foundation with clear panel routes and one set of backend modules. Requires strict backend authorization.
3. **One undifferentiated interface for all roles:** Less frontend structure, but makes panel responsibilities and role-specific workflows harder to understand and test.

## Decision

Use **one React frontend application** containing Student, Cashier / Accountant, and Owner panel areas, connected to **one Express modular backend**. Panel navigation and routes reflect the authenticated role. The backend independently enforces role and permission checks on every protected operation.

## Rationale

This preserves the three-panel product structure without duplicating application infrastructure. It is practical for a small student team and AI-assisted development. Central backend authorization is necessary because frontend hiding alone cannot protect finance or personal data.

## Consequences

- **Positive:** Shared UI foundation; one backend API; consistent authentication and common components; less setup and maintenance.
- **Negative:** The frontend and backend are not independently deployed per panel; careful route and permission testing is required.
- **Risk:** Developers may mistake hidden UI controls for security. Backend authorization must remain authoritative.
- **Revisit when:** There is a justified requirement for independent client applications or deployment boundaries.

## Verification

Inspect the frontend route structure and verify all three panel areas exist. Test direct API calls as Student, Cashier / Accountant, and Owner users. Confirm that cashier/accountant requests for cafe finance, reports, bank details, or bank connection are denied by the backend.

## AI-agent instruction derived from this ADR

> Keep the three panels in one frontend application and use one modular backend. Do not create separate backend deployments for the panels. Never rely on frontend route guards or hidden controls as the only authorization mechanism.


## Working-baseline clarification — three-panel permissions and demo bank (15 November 2026)

The three-panel structure remains unchanged. The updated permission contract is:

- Student: access only to the authenticated student's own profile, Favorites, orders, receipts, and student-wallet records.
- Cashier / Accountant: operational capabilities only, constrained by owner-assigned permissions. Cancellation/refund and cafe open/close are denied by default unless delegated.
- Owner: all operational capabilities plus cafe-wallet finance, financial reports/exports, and bank-connection/simulator operations.
- Cafe-wallet finance, financial reports/exports, connected demo-bank details, and all bank simulator operations are owner-only and non-delegable.

Enforce these rules in backend middleware and use-case authorization checks, not only in React route guards. Direct API calls and reused sessions must be tested.

The bank feature is an internal simulator module accessed only by owner-authorized Cafe Wallet & Finance use cases. It is not an external provider integration or a separate service. Its demo connection lifecycle and simulated transfers follow PRD Section 15 (OQ-01–OQ-04). All visible outcomes must be labelled simulated.

The owner may create/deactivate staff accounts and assign operational permissions under OQ-05/OQ-06/OQ-19. These OQ resolutions are proposed working decisions recorded in the decision log, pending team/TA review.
