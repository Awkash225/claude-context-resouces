# AGENTS.md — FASTBite Coding-Agent Instructions

**Version:** 2.0  
**Working requirements source:** `FASTBite_Final_PRD_TA_Corrections.md` (mirrored as `FASTBite_Final_Changed_PRD.md`)  
**Decision record:** `FASTBite_TA_Correction_Decision_Log.md`

## 1. Project intent and source-of-truth hierarchy

FASTBite is a zero-budget university academic prototype that demonstrates a realistic cafe ordering and management system. It is not a production banking, payment-gateway, or commercial system.

Read these files before changing code:
1. `FASTBite_Final_PRD_TA_Corrections.md` — product requirements and behavior.
2. `FASTBite_TA_Correction_Decision_Log.md` — status and traceability of TA-correction decisions.
3. `architecture.md` — architecture and module boundaries.
4. `ADRs/ADR-001-architecture-style.md` through `ADRs/ADR-004-technology-stack.md`.

The PRD governs product behavior. The decision log records the proposed OQ resolutions applied to the working PRD and explicitly says team/TA review is required. Architecture and accepted ADRs govern technical structure. Do not represent proposed OQ resolutions as confirmed client or TA approvals.

**Known source inconsistencies:** The PRD still has stale passages that conflict with Section 15 and the decision log: the FR-count introductory sentence says 14 although FR-01–FR-17 are present; some unavailable-item and bank-connection flows still call resolved behavior open; and FR-10's lockout wording is less precise than OQ-12. For these specific OQs, use Section 15 and the decision log as the latest recorded resolution, and flag the stale wording for editorial cleanup. Do not silently modify requirements or invent new behavior.

## 2. Approved architecture and cost constraints

- Preserve a modular monolith: one React frontend, one Express + TypeScript backend deployment, one PostgreSQL database.
- Use React + TypeScript + Vite, Tailwind CSS, Node.js + Express + TypeScript, PostgreSQL, Prisma, REST, and SSE where useful.
- Keep development runnable locally with free/open-source tools.
- Do not introduce microservices, multiple databases, Redis, message brokers, Kubernetes, API gateways, paid hosting, paid APIs, or commercial payment services without an ASR-based justification, an ADR proposal, and explicit human approval.
- Do not generate the complete product during architecture-validation tasks.

## 3. Three panels and authorization invariants

The frontend has three panel areas in one application:
- Student Panel.
- Cashier / Accountant Panel.
- Owner Panel.

The backend is the security boundary. Hiding navigation or adding client route guards is not authorization.

Enforce these invariants on every protected backend request:
- Students can access only their own profile, Favorites, orders, receipts, and student-wallet records.
- Cashier/accountant users have only the operational permissions assigned by the owner.
- Cancellation/refund and cafe open/close are denied to cashier/accountant by default and may be delegated only as specified in PRD Section 5.6.
- Cafe-wallet balances/transactions, cafe financial reports/exports, bank details, bank connection/disconnection, and simulated bank operations are owner-only and non-delegable.
- The owner has all operational capabilities and all owner-only financial capabilities.
- Denied direct-route/API requests must be rejected by the backend and logged where required.

## 4. Required backend modules

Preserve the boundaries in `architecture.md`:
- Identity & Access
- Customer (including Favorites)
- Staff Access
- Menu
- Inventory (including thresholds and low-stock warnings)
- Ordering
- Student Wallet
- Cafe Wallet & Finance
- Refunds
- Receipts & History
- Notifications
- Reporting & Audit
- Bank Integration Adapter (internal simulator only)

The exact folder names may vary, but business ownership and interfaces must remain clear. The Bank Integration Adapter is an internal module, not a microservice.

## 5. Dependency and data-access rules

1. Frontend code must never access PostgreSQL directly.
2. API controllers handle transport, validation, and response mapping; use cases/services own business rules.
3. Business rules must not exist only in React components or route handlers.
4. Each module exposes explicit public application interfaces.
5. Do not import another module's private repository, internal service, or private Prisma data-access layer.
6. Do not arbitrarily read/write another module's tables. Coordinate cross-module use cases through interfaces.
7. Use PostgreSQL transactions for operations that must update related records.
8. Use database uniqueness and idempotency keys for order submission, wallet debits, simulated bank transfers, refunds, stock deduction/restoration, and other retryable effects.
9. Persist immutable order-item/receipt snapshots so later menu edits do not rewrite history.
10. Financial balances must reconcile to ledger/transaction records; do not silently overwrite balances.
11. PostgreSQL is authoritative. SSE and notifications are delivery mechanisms only.

## 6. Recorded business decisions to implement

These are proposed decisions recorded in PRD Section 15 and the decision log. They are the current working implementation baseline, pending team/TA review:

- **Bank simulator (OQ-01–04):** internal FASTBite demo bank only; predefined demo account; demo credentials and displayed demo OTP; simulated Connected/Failed/Pending states, deposits, withdrawals, transaction history, and failure cases. No external provider, real credentials, external OTP, or real money movement. Label every state and transaction as simulated.
- **Staff access (OQ-05, 06, 19):** owner creates/deactivates staff accounts and assigns operational permissions. Cancellation/refund and cafe open/close default denied unless delegated. Finance/bank permissions cannot be delegated.
- **Order states (OQ-07):** Pending → Approved/Cooking → Ready to pick → Collected; permitted cancellation leads to Cancelled/Refunded. Collected and Cancelled are terminal. Refund state is tracked separately and may remain Pending.
- **Unavailable items (OQ-08–10):** each unavailable item has an independent five-minute server-timed window. Timeout removes that item and continues with remaining available items; if none remain, cancel the order. Whole-order cancellation closes other windows and creates one order-level refund for amounts actually charged. Offline deadlines continue; late responses cannot reverse timeout.
- **Receipt/collection (OQ-11):** collection is blocked until receipt generation succeeds and the receipt is available for verification.
- **Wallet lockout (OQ-12):** five consecutive failed attempts in a rolling 24-hour window trigger a 24-hour lock; successful authentication resets the consecutive-failure count.
- **Preparation (OQ-13):** timer options 1, 2, 3, 5, or 10 minutes; longest accepted To-Cook duration governs; ready-made-only orders skip the cooking timer.
- **Deleted menu item (OQ-14):** unavailable for new orders; historical snapshots preserved; pending orders use unavailable-item handling; accepted/in-preparation orders remain valid.
- **Retention, reporting, audit (OQ-15–18):** three calendar months for customer order history/receipts from completion/cancellation; preserve wallet ledger integrity after account deletion; PKT reporting day boundary with UTC storage; audit actor/role/action/target/UTC timestamp/outcome/relevant before-and-after values. Never log secrets.

If a detail in these resolutions appears to conflict with another PRD passage, cite the conflicting sections and stop for human review rather than inventing a third interpretation. The hierarchy above applies only to the documented stale passages identified in the source caveat.

## 7. Security and secrets

- Hash passwords/PINs using an appropriate one-way password-hashing mechanism; never store or log them in readable form.
- Never commit secrets, tokens, passwords, OTP values, real bank credentials, or private keys.
- The demo OTP may be displayed in the demo UI by design, but must not be logged as a secret or represented as a real external OTP.
- Keep demo credentials clearly identified as test-only values.
- Verify role and permission on the backend for each finance, refund, order, stock, and staff-management operation.
- Apply customer data ownership checks in queries and mutations, not only in the UI.

## 8. Reliability, time, and audit

- Use idempotency and database constraints to prevent duplicate orders, numbering, debits, transfers, refunds, and stock effects.
- Use transaction boundaries for multi-record business operations.
- Use server-side time for unavailable-item deadlines.
- Store timestamps in UTC; use PKT (UTC+05:00) for reporting calendar-day boundaries and display.
- Keep order status and refund status separate.
- Keep receipt generation state explicit; do not allow collection while receipt generation has failed or is pending.
- Keep historical order and receipt snapshots stable.
- Record the audit fields specified by OQ-18. Never claim NFR performance targets are met until measured.

## 9. Testing expectations

At minimum, add or plan tests for:
- Student isolation and own-record access.
- Cashier/accountant denial of cafe finance, reports, bank details, and bank operations, including direct API calls.
- Owner access to all operational and owner-only finance capabilities.
- Delegated versus default-denied staff permissions.
- Concurrent order numbering and idempotent order submission.
- Independent unavailable-item deadlines, whole-order cancellation, offline timeout, and duplicate-refund prevention.
- Receipt failure blocking collection.
- Wallet lockout window and reset behavior.
- Demo bank connection lifecycle, failure behavior, disconnected-state rejection, and idempotent simulated transfers.
- Stock concurrency, restoration, and threshold warnings.
- Retention boundaries and PKT report grouping.
- SSE reconnect followed by authoritative REST refresh.

## 10. Structure proposal and change control

When asked to propose a project structure, provide a directory tree, module responsibilities, dependency direction, Prisma ownership, panel routes, authentication/authorization placement, and ADR/ASR compliance. Do not write a full application unless separately requested.

Do not change architecture style, database, stack, module ownership, role boundaries, or simulator boundary without:
1. identifying the affected ASR/constraint;
2. explaining the problem;
3. presenting alternatives and trade-offs;
4. proposing an ADR update;
5. obtaining human approval.

Do not claim that the university team or TA approved any assistant-generated decisions without recorded evidence.
