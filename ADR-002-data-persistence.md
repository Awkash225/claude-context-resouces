# ADR-002: Use One PostgreSQL Relational Database

- **Status:** Accepted
- **Date:** 2026-11-10
- **Project:** FASTBite
- **Related drivers:** ASR-02 (order uniqueness and retry safety); ASR-03 (cross-record consistency); ASR-06 (inventory consistency); ASR-07 (refund lifecycle); ASR-08 (retention and audit records)

## Context

FASTBite stores related order, order-item, stock, wallet-ledger, refund, receipt, customer, and reporting records. The PRD requires that retries do not create duplicate orders, wallet debits, refunds, or stock restorations. It also requires consistency between accepted items, order status, stock effects, wallet transactions, refunds, and receipts.

The team has approved SQL persistence and wants a free, locally runnable database for an academic project. The modular monolith does not require separate databases for each module.

## Options considered

1. **One relational database:** A single SQL database supports constraints, relationships, and transactions. Modules share the database but own their tables and expose controlled interfaces.
2. **One document database:** Flexible document storage, but relational integrity and coordinated updates across financial and inventory records require additional application-level discipline.
3. **Multiple databases:** Separate stores for modules could isolate data but would add operational and consistency complexity that the current project does not require.

## Decision

Use **one PostgreSQL relational database** for the initial FASTBite implementation. Use Prisma for schema access and migrations. Each business module logically owns its tables and must expose interfaces for other modules to use its data or operations.

## Rationale

PostgreSQL provides relational constraints and transaction support suited to FASTBite's connected order, inventory, wallet, refund, and receipt records. It is free and open source and can be run locally. One database is appropriate for the modular monolith and avoids unnecessary infrastructure.

## Consequences

- **Positive:** Transactional updates across related records; relational constraints; one local database to install and maintain; no database licensing cost.
- **Negative:** Modules share one database instance and require disciplined logical ownership; schema changes need migration coordination.
- **Risk:** Direct cross-module table access could create hidden coupling even though there is only one database.
- **Revisit when:** A measured operational or compliance need requires a different persistence strategy, and the team can justify the added cost and complexity.

## Verification

Review the Prisma schema for clear module ownership. Check that order identifiers are protected by database uniqueness, and that cross-record operations use appropriate transactions. Confirm that modules do not import private repositories or models from other modules.

## AI-agent instruction derived from this ADR

> Use one PostgreSQL database and Prisma migrations. Keep table ownership aligned with business modules. Do not add another database, a NoSQL store, or a cache as a source of truth without an ASR-based justification and human approval.


## Working-baseline clarification — TA-correction decisions (15 November 2026)

The single PostgreSQL decision is unchanged. The current working PRD adds explicit data-integrity needs that the implementation must support within this same database:

- Store wallet and simulated-bank operations as immutable ledger/transaction records with unique operation/idempotency references.
- Store refund lifecycle separately from order status; a cancelled order may have a refund still Pending.
- Store each unavailable-item decision window independently, including server-created deadline and terminal decision, so multiple items cannot trigger duplicate order-level refunds.
- Preserve immutable order-item and receipt snapshots.
- Persist audit fields for bank connection changes, simulated deposits/withdrawals, refunds, permission changes, and finance actions.
- Apply the distinct retention rules in PRD OQ-15–OQ-18 without deleting ledger/audit records needed for financial integrity.
- Use UTC timestamps in storage and PKT for reporting-day grouping.

These are schema and transaction responsibilities inside the existing PostgreSQL database; they do not justify another database, cache, or event broker. The OQ decisions are proposed and remain subject to team/TA review.
