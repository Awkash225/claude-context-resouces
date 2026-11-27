# FASTBite — Integrated Product Requirements Document (PRD)

**Project:** FASTBite  
**Document type:** Integrated Product Requirements Document  
**Version:** Final changed PRD — three-panel version  
**Date:** 10 November 2026  
**Status:** Final consolidated PRD reflecting the latest three-panel decision; explicitly listed open questions remain subject to team decisions  
**Language:** English

## Source and decision policy

This revision is based on the uploaded integrated PRD, FASTBite Project Context and Source of Truth, the area PRDs, recorded integration decisions, and the latest instruction to use three panels.

The latest panel decision changes the earlier two-panel structure. The system shall have three distinct panels:

1. Student Panel — remains unchanged from the previously agreed student-facing scope.
2. Cashier / Accountant Panel — retains the operational features previously assigned to the cashier/accountant, but has no access to wallet finances and cannot connect or manage any bank account.
3. Owner Panel — includes all cashier/accountant operational capabilities and has full access to cafe wallet finances, financial reports, and bank-account connection functionality.

**Important financial-scope qualification:** Earlier project decisions describe FASTBite wallets as simulated and explicitly exclude real bank, payment-gateway, and mobile-wallet integrations. The latest instruction explicitly adds the ability for the owner to connect a bank account to the cafe wallet. This is recorded here as a new scope change for the Owner Panel. The bank provider, connection method, authorization protocol, supported banking operations, and whether the connection is live or a demonstration/sandbox connection have not been specified. They remain open and must not be invented. The cashier/accountant panel must not receive this capability under any interpretation.

Where earlier requirements conflict with the latest three-panel decision, this revision applies the latest panel separation. Other unresolved behavior remains identified as open rather than being silently decided.

---

## 1. Product overview

FASTBite is a university-cafe ordering and operations system for the cafe at FAST NUCES. It combines customer ordering, menu and stock visibility, simulated student-wallet functions, order processing, receipts, collection verification, cafe financial management, and reporting.

FASTBite provides separate user experiences for students, cashier/accountant staff, and the cafe owner. Students use the Student Panel to browse the menu, place orders, use their student wallet, receive updates, and access their own records. Cashier/accountant staff use the Cashier / Accountant Panel to perform permitted operational work. The owner uses the Owner Panel to perform all cashier/accountant work and, in addition, control cafe-wallet finances, connect the cafe bank account, and access financial records.

The product addresses the cafe's reported problems: reused or fake payment proofs, receipt swapping, mismatches between recorded sales and money received, uncertainty about item availability, inventory visibility, and rush-hour queues.

### 1.1 Main capabilities

- Student registration, login, PIN entry, and account recovery.
- Menu browsing, search, filtering, and availability display.
- Cart management and order submission.
- Order review, item approval/cancellation, Final Accept, and order-status tracking.
- Unavailable-item decisions and applicable refunds.
- Preparation, readiness, receipt generation, and collection verification.
- Menu editing, stock management, availability updates, and configurable low-stock thresholds.
- Customer Favorites lists with current price and availability information.
- Reordering from a previous order in Order History, with current stock and pricing validation.
- Student wallet deposits, withdrawals, fees, notifications, and transaction history.
- Cafe wallet access, authentication, withdrawals, transaction history, and financial reporting, restricted to the Owner Panel.
- Owner-only bank-account connection capability.
- Cafe opening and closing.
- Order history, receipts, reports, exports, and operational records.
- Permission enforcement separating student, cashier/accountant, and owner capabilities.

## 2. Problem and user needs

### 2.1 Student / customer needs

Students and other eligible customers need to:

- Register and sign in.
- Browse the current menu and see prices and availability.
- Search and filter menu items.
- Add multiple items to a cart and place an order.
- Pay through the supported student-wallet workflow.
- Receive an order number, receipt, and relevant notifications.
- Follow order progress and respond to unavailable-item prompts.
- View their own order history, receipts, wallet balance, and wallet transactions.
- Recover account access through the approved process.

A customer must not access another customer's personal, order, receipt, or wallet information.

### 2.2 Cashier / accountant needs

Cashier/accountant staff need to perform the operational tasks assigned to them, subject to their permissions. These include:

- Viewing and reviewing incoming orders.
- Performing permitted approval, cancellation, and preparation actions.
- Handling unavailable items and customer decisions.
- Verifying receipts and recording collection.
- Managing menu items, availability, and stock where permission is granted.
- Opening and closing the cafe where permission is granted.
- Viewing operational order information needed for their work.

The Cashier / Accountant Panel must not expose cafe-wallet balances as financial information, wallet transactions, withdrawals, financial reports, bank-account connection, bank-account details, or any other wallet-finance controls. No bank account can be connected from this panel.

### 2.3 Owner needs

The owner needs all operational capabilities available in the Cashier / Accountant Panel, plus complete access to cafe financial management. The Owner Panel shall provide:

- All cashier/accountant operational features.
- Access to the cafe wallet and its financial information.
- Cafe-wallet transaction history and withdrawals.
- Financial reports and permitted exports.
- The ability to connect the cafe bank account to the cafe wallet.
- The ability to review the connected bank-account status and manage the connection, subject to the connection behavior that the team will define.

The owner is the only one of these three panel roles with cafe-wallet finance and bank-connection access.

## 3. Goals

- **G-01 — Customer ordering:** Enable customers to browse the menu and place orders.
- **G-02 — Three-panel separation:** Provide distinct Student, Cashier / Accountant, and Owner panels with the access boundaries in this PRD.
- **G-03 — Order processing:** Support order review, approval, unavailable-item handling, preparation, and collection.
- **G-04 — Student wallet:** Support the approved student-wallet operations and personal transaction history.
- **G-05 — Menu and stock:** Keep menu and stock information current.
- **G-06 — Cafe finance:** Give the owner exclusive access to cafe-wallet finances, reports, and bank-account connection.
- **G-07 — Records and receipts:** Maintain the required order, receipt, wallet, and operational records.
- **G-08 — Cafe operations:** Support manual cafe opening and closing.
- **G-09 — Reliability:** Prevent lost or duplicated orders, stock effects, and financial effects.
- **G-10 — Performance and usability:** Meet the measurable performance and usability targets.
- **G-11 — Favorites:** Allow customers to save, view, and remove favorite menu items with current item information.
- **G-12 — Reordering:** Allow customers to rebuild a cart from a previous order while applying current availability, stock, and prices.
- **G-13 — Low-stock monitoring:** Allow authorized cafe staff to configure stock thresholds and identify countable items at or below those thresholds.

## 4. Scope and exclusions

### 4.1 In scope

- The three panels and their role-based access boundaries.
- Existing Student Panel functionality, unchanged by this panel restructuring.
- Cashier/accountant operational functionality, excluding all cafe-wallet finance and bank-account connection functionality.
- Owner operational functionality, including all cashier/accountant features and owner-only financial functionality.
- Simulated student-wallet functions and the existing cafe-wallet requirements, subject to the bank-connection scope change stated above.
- Owner-only cafe bank-account connection capability. Detailed integration behavior remains open.
- The ordering, menu, stock, receipt, collection, reporting, and retention requirements recorded in this PRD.
- Customer Favorites lists and reorder-from-history functionality.
- Configurable minimum stock thresholds and low-stock warnings for countable menu items.

### 4.2 Out of scope or not yet specified

- Cashier/accountant access to cafe-wallet finances or bank-account connection.
- Real-money payment processing by the Student Panel.
- Any bank provider, API, technical protocol, or banking operation not explicitly selected by the team.
- Automatic bank transfers or claims that an external transfer has completed without a confirmed integration result.
- A separate kitchen-staff panel.
- Languages other than English.
- Technologies, frameworks, databases, or hosting choices not established by a team decision.

**Scope-change note:** The previous integrated PRD treated real bank integration as out of scope. The latest owner-panel instruction changes that boundary by requiring an owner-only bank-account connection capability. This PRD records the capability as required but leaves its exact behavior open pending a team decision.

## 5. Users, panels, and permissions

### 5.1 Student Panel

The Student Panel remains as previously agreed. This revision does not remove, redesign, or reassign its existing features.

Student capabilities include:

- Registration and login.
- Menu browsing, search, and filtering.
- Cart management and order placement.
- PIN entry at the applicable order step.
- Student-wallet balance, deposits, and withdrawals.
- Order status and notifications.
- Personal order history and receipts.
- Personal wallet transaction history and supported export.
- Account recovery and other previously approved student-side features.

Students may only access their own personal and financial records.

### 5.2 Cashier / Accountant Panel

The Cashier / Accountant Panel contains the operational features previously assigned to the cashier/accountant. Depending on the staff member's assigned permissions, these include:

- Incoming-order viewing and review.
- Order approval or cancellation actions.
- Preparation timer and order-status actions.
- Unavailable-item processing.
- Receipt verification and collection recording.
- Menu creation, editing, deletion, availability, and stock management.
- Cafe opening and closing.
- Operational order records and other permitted non-financial operational functions.

**Explicit restrictions:**

- No cafe-wallet finance access.
- No cafe-wallet transaction-history access.
- No cafe-wallet withdrawal access.
- No cafe financial-report access.
- No bank-account connection or disconnection.
- No viewing or editing of connected bank-account details.
- No wallet-finance settings or owner-only finance controls.

The cashier/accountant may not gain financial access merely because they can perform operational actions.

### 5.3 Owner Panel

The Owner Panel shall include all operational capabilities provided by the Cashier / Accountant Panel. The owner shall not need to switch to the cashier/accountant account to perform those tasks.

In addition, the Owner Panel provides complete cafe-finance access, including:

- Cafe-wallet balance and financial information.
- Cafe-wallet authentication and operations.
- Cafe-wallet withdrawals.
- Cafe-wallet transaction history.
- Cafe sales and financial reports.
- Refund logs and permitted financial exports.
- Bank-account connection to the cafe wallet.
- Viewing the connection status and managing the connection, to the extent defined by the final bank-connection decision.

The owner is the only role authorized to use these finance and bank-connection functions.

### 5.4 Permission model

The system shall enforce permissions at the action and data level, not merely by hiding panel navigation. A cashier/accountant must be denied access to owner-only finance functions even if they attempt to open a direct route or reuse an existing session.

The owner has all operational permissions. Cashier/accountant access is permission-based and assigned by the owner. The initial default permission set is:

- Order viewing and review: permitted staff.
- Order approval, Final Accept, preparation-status updates: permitted order-processing staff.
- Order cancellation and refund initiation: owner only by default; a cashier/accountant may do these only if the owner explicitly grants the corresponding permission.
- Receipt verification and collection: permitted collection staff.
- Menu and stock management, including minimum-stock threshold configuration: permitted inventory staff.
- Cafe opening and closing: owner only by default; may be delegated explicitly.
- Cafe-wallet finance, cafe-wallet transaction history, financial reports/exports, bank connection, deposits, withdrawals, and bank details: owner only and non-delegable in this prototype.

Every staff permission is checked by the backend. Denied actions are logged. The owner can review and change staff permissions. Staff-account creation/deactivation is included as an owner administrative capability; credential recovery follows the system's account-recovery process.

### 5.5 Panel access summary

| Capability | Student Panel | Cashier / Accountant Panel | Owner Panel |
|---|---:|---:|---:|
| Browse menu | Yes | As operationally needed | As operationally needed |
| Place customer orders | Yes | No, unless separately defined | No, unless separately defined |
| Student wallet | Own wallet only | No access | No access to another student's wallet |
| View incoming orders | No | Permission-based | Yes |
| Approve / process orders | No | Permission-based | Yes |
| Manage menu and stock | No | Permission-based | Yes |
| Verify receipt / mark collected | No | Permission-based | Yes |
| Open / close cafe | No | Permission-based | Yes |
| Cafe wallet finances | No | **No** | **Full access** |
| Cafe financial reports | No | **No** | **Full access** |
| Connect cafe bank account | No | **No** | **Owner only** |
| View cafe-wallet transactions | No | **No** | **Full access** |

### 5.6 Operational permission matrix

| Action | Student | Cashier / Accountant | Owner |
|---|---|---|---|
| View incoming orders | No | If granted | Yes |
| Review order details | No | If granted | Yes |
| Approve / Final Accept | No | If granted | Yes |
| Cancel order / initiate refund | No | Only if explicitly granted; default denied | Yes |
| Update preparation / ready status | No | If granted | Yes |
| Verify receipt / mark Collected | No | If granted | Yes |
| Create / edit / delete menu items | No | If granted | Yes |
| Update stock / configure minimum threshold | No | If granted | Yes |
| View low-stock list | No | If granted | Yes |
| Open / close cafe | No | Only if explicitly granted; default denied | Yes |
| Manage staff accounts and operational permissions | No | No | Yes |
| View cafe-wallet finance / bank details | No | No | Yes |
| Connect / disconnect demo bank account; simulate deposits / withdrawals | No | No | Yes |

The owner may delegate only the operational permissions identified as delegable above. Finance and bank-connection permissions remain owner-only.

## 6. Glossary

| Term | Meaning / status |
|---|---|
| Student / Customer | A person using the customer-facing Student Panel. |
| Cashier / Accountant | A staff user performing permitted cafe operational work without cafe-wallet finance or bank-connection access. |
| Owner | The cafe owner using the Owner Panel, with all cashier/accountant operational capabilities plus exclusive cafe-finance and bank-connection access. |
| Student Panel | Customer-facing panel; its previously agreed scope remains unchanged. |
| Cashier / Accountant Panel | Staff operational panel with finance and bank-connection access removed. |
| Owner Panel | Owner panel containing all cashier/accountant features plus owner-only financial functions. |
| Countable item | An item whose remaining quantity is tracked and shown. |
| Availability-based item | An item shown as available or unavailable, with availability updated manually. |
| Final Accept | The cafe-side acceptance step after which the student-wallet balance is rechecked and payment is processed under the applicable order flow. |
| Pending | Customer-facing order status before the relevant counter response. |
| Exceptional Cases | Order-management area for unavailable-item decisions, as described in the area requirements. |
| Ready to Pick | Order status indicating that the order is ready for collection. |
| Collected | Order status recorded after receipt/order verification and handover. |
| Simulated wallet | An in-system balance and transaction record that is not, by itself, proof of a real-money transfer. |
| Favorites | A customer-specific saved list of menu items that can be viewed and removed by that customer. |
| Reorder | Starting a new cart using items and quantities from a previous order, subject to current menu, stock, and price validation. |
| Minimum stock threshold | A staff-configured quantity for a countable menu item; reaching or falling below it triggers a low-stock warning. |
| Bank-account connection | New owner-only capability requested in this revision. The provider, technical method, and actual financial operations remain open. |

## 7. Functional requirements

The functional requirements are consolidated into **14** complete user capabilities. Each FR combines related requirements from the previous integrated PRD and the area PRDs.

### FR-01 — Student account access and personal data

The system shall allow eligible customers to register, log in, set and use their PIN, recover account access through the approved process, and access only their own personal records.

**Includes:**
- Registration and login using the approved customer details and verification process.
- PIN setup and PIN entry at the applicable ordering step.
- Incorrect PIN feedback without customer PIN lockout.
- Approved Forgot PIN / account-recovery flow.
- Isolation of customer profile, order, receipt, and wallet information.
- Previously agreed account-management behavior, subject to the applicable open retention/deletion decisions.

**Acceptance criteria:**
- A person can register and access the Student Panel using the approved process.
- A customer can access only their own private records.
- An incorrect PIN displays an error message; repeated incorrect attempts do not lock the customer PIN.
- Recovery follows the approved channel and verification steps.

### FR-02 — Menu browsing, search, filters, and availability

The system shall display the cafe menu to customers, including item name, price, optional picture, category, and availability; countable items shall also show remaining quantity. Customers shall be able to search and filter by the approved price-range and category options.

**Includes:**
- Menu browsing while the cafe is open or closed.
- Search and category / price-range filtering, including combined filters.
- “No items found” when no item matches.
- Current availability and remaining countable quantity.
- Prevention of ordering items that are unavailable or have insufficient stock.
- Latest price display and cart-total refresh if an item's price changes before placement.

**Acceptance criteria:**
- The menu remains viewable while the cafe is closed, but new ordering is blocked.
- Combined filters return only items matching all selected filters.
- An item without an optional picture remains visible with its other information.
- A newly unavailable item cannot be ordered.

### FR-03 — Cart management and order submission

The system shall allow customers to select multiple eligible menu items, review and update their cart, enter their PIN at the applicable step, and submit one order through the approved ordering workflow.

**Includes:**
- Adding and removing items before submission.
- Reviewing quantities, prices, and total.
- Validating item availability and countable stock.
- Submitting one multi-item order.
- Handling insufficient student-wallet balance according to the approved payment stage.
- Preventing a repeated tap or retry from creating a duplicate order.

**Acceptance criteria:**
- A valid cart submission creates one order containing the selected items.
- An item that is unavailable or exceeds available quantity is rejected from the order.
- A repeated submission of the same request does not create a second order.
- The system provides clear feedback if submission cannot complete.

### FR-04 — Order numbering, order records, and status tracking

The system shall create and maintain order records, assign unique continuous order numbers, and show the current order status to the customer and authorized cafe users.

**Includes:**
- Continuous order numbering from the previous day's last number; numbers do not restart at 1 or repeat.
- One order number per order.
- Customer-facing statuses: Pending, Approved/Cooking, Ready to pick, Collected, and Cancelled/Refunded, subject to the approved status model.
- Main Orders and Exceptional Cases order-management views where applicable.
- Order event recording and status visibility.
- Correct status restoration after connectivity returns.

**Acceptance criteria:**
- Concurrent orders receive different order numbers.
- Order numbers are not reused across days.
- Pending orders remain pending until the authorized counter response.
- Customers and authorized staff see the same current order record.
- Reconnection does not create a duplicate order.

### FR-05 — Order review, approval, Final Accept, and preparation

The system shall allow authorized cashier/accountant staff and the owner to review incoming orders, check fulfilment, perform permitted approval or cancellation actions, complete Final Accept, and manage preparation status.

**Includes:**
- Reviewing order and item details.
- Item-level approval or cancellation where required.
- Final Accept after unavailable-item decisions are resolved.
- Rechecking the student's wallet balance at Final Accept.
- Deducting payment for accepted items only when the balance is sufficient.
- Returning the order to Pending and requiring a new order if the balance is insufficient at Final Accept.
- Preparation timers and readiness behavior from the approved GRILL requirements.
- Timer choices of 1, 2, 3, 5, or 10 minutes where the timer requirement applies.
- Whole-order countdown based on the longest required preparation time.
- Ready-made-only orders becoming Ready to pick after approval where applicable.

**Acceptance criteria:**
- Only users with the required permission can perform protected order actions.
- Final Accept rechecks the current student-wallet balance.
- Insufficient balance prevents acceptance and payment.
- The preparation timer follows the approved timer choices and status behavior.
- Reviewing an order does not itself count as Final Accept.

### FR-06 — Unavailable-item decisions, cancellation, and refunds

The system shall manage unavailable items by notifying the customer, collecting the applicable decision, updating the order, and applying the approved refund behavior.

**Includes:**
- Moving affected orders into the applicable Exceptional Cases / Pending Orders workflow.
- A separate five-minute decision window for each unavailable item, as specified in the area PRD.
- Customer choice to continue without an unavailable item or cancel the whole order.
- Excluding unavailable items when the customer continues.
- Whole-order cancellation when the customer declines the order.
- If the five-minute decision window expires without a customer response, the affected unavailable item is removed from the order, the customer is notified, and the order continues with the remaining available items. If no items remain, the order is cancelled. Any amount already charged for the removed item is refunded through the approved refund process; if the cafe wallet lacks sufficient funds, the refund remains pending until funded.
- Refund records and customer notifications.
- Underfunded cafe-wallet handling: an item remains uncancelled until the cafe wallet has sufficient funds for the required refund.
- No refund for an amount that was never charged.

**Acceptance criteria:**
- The customer is told which item is unavailable.
- Each affected item has its own recorded decision window.
- Continuing without an item excludes that item and applies the approved item-refund process.
- Choosing whole-order cancellation applies the full-order cancellation/refund process.
- A refund is not shown as completed before its required conditions are met.
- The timeout outcome is applied consistently even if the customer is offline; the deadline is measured from the notification timestamp using server time. A late response cannot reverse a completed timeout decision, but the customer can contact cafe staff for support.

### FR-07 — Receipt generation, history, and collection verification

The system shall generate receipts for accepted and paid orders, provide eligible customers with their order history and receipts, and allow authorized staff to verify an order and mark it Collected only once.

**Includes:**
- Receipt shared between customer and cafe sides.
- Receipt details including order number, item names, quantities, prices, total, time, cancelled items, and refunded amounts where applicable.
- Automatic receipt-generation retry without a fixed retry limit.
- An order cannot be marked Collected until a receipt has been successfully generated and is available for verification. Receipt-generation failure leaves the order in Ready to pick (or its current eligible state), displays a failure/pending indicator to staff, and triggers retry. Staff may not bypass this condition.
- Receipt-generation status on the cafe counter screen.
- Customer order history and downloadable receipt access.
- Three-month retention for customer order history and receipts.
- Receipt and order-number verification before collection.
- Single-time collection; a collected order cannot be collected again.

**Acceptance criteria:**
- A successfully accepted and paid order receives a receipt.
- Receipt content reflects the final accepted items and applicable refunds.
- Receipt-generation failure triggers automatic retry and visible status.
- Authorized staff verify the receipt/order before marking Collected.
- A second collection attempt is rejected.
- Customer order history shows eligible records within the retention period.

### FR-08 — Menu and stock management

The system shall allow authorized cashier/accountant staff and the owner to create, edit, delete, and maintain menu items and stock according to their permissions.

**Includes:**
- Item name, price, optional picture, fixed category, preparation classification, and stock type.
- Fixed categories: Drinks; Meals/Saalan; Fast Food; Small Items.
- Countable-item starting quantities and automatic stock deduction.
- Availability-based item manual available/unavailable setting.
- Next-day quantity configuration and midnight reset when a quantity has been configured.
- Missing next-day quantity flagging rather than an assumed reset.
- Stock restoration after a qualifying cancellation.
- Prevention of over-ordering and duplicate stock restoration.
- Menu deletion at any time; existing orders retain their original item details.
- Duplicate item-name validation according to the accepted rule.

**Acceptance criteria:**
- Only authorized staff can manage menu and stock.
- Countable items require a starting quantity.
- Stock is not allowed to become negative through an accepted order.
- Cancellation restores the relevant stock once only.
- Editing or deleting an item does not rewrite historical order details.
- If no next-day quantity is configured, the system flags the missing configuration rather than resetting automatically.

### FR-09 — Student wallet operations

The system shall allow customers to view and manage their own simulated student wallet through the Student Panel.

**Includes:**
- Wallet balance display.
- Deposits from PKR 50 through PKR 20,000 per transaction.
- Withdrawals from PKR 50 through PKR 20,000 per transaction.
- Insufficient-balance validation.
- 2% withdrawal fee.
- Transaction notifications and personal transaction history.
- Date-range transaction-history export where supported.
- Indefinite retention of student-wallet transaction history, separate from order-history retention.

**Acceptance criteria:**
- Amounts outside the permitted transaction range are rejected with an explanatory message.
- A PKR 100 withdrawal debits PKR 100, records PKR 2 as the fee, and records PKR 98 as the amount received.
- A withdrawal exceeding the available balance is rejected.
- A customer can view only their own wallet transactions.
- Wallet history remains retained under the approved indefinite-retention rule.

### FR-10 — Cafe wallet and owner-only financial operations

The system shall provide cafe-wallet access and financial operations exclusively through the Owner Panel. The Cashier / Accountant Panel shall have no access to these functions.

**Includes:**
- Cafe-wallet balance display and wallet authentication.
- Cafe-wallet withdrawals from PKR 500 through PKR 80,000 per transaction.
- Insufficient-balance rejection.
- No deduction on cafe-wallet withdrawals, as specified by the cafe-wallet area requirement.
- Cafe-wallet transaction history retained without a time limit.
- Password lockout after five incorrect attempts within one day for 24 hours, unless email OTP recovery unlocks access sooner.
- Re-authentication after each successful wallet operation and locking on Back, according to the area requirement.
- Single active wallet session behavior across devices, as specified by the area requirement.
- Owner-only access to wallet transaction records and finance controls.
- Owner-only financial reporting and export access.

**Acceptance criteria:**
- A cashier/accountant cannot view or operate cafe-wallet finances, including by direct route or reused session.
- Only the owner can access the cafe wallet's protected operations and transaction history.
- Invalid withdrawal amounts and withdrawals exceeding the balance are rejected.
- The wallet applies the recorded lockout and re-authentication rules.
- Cafe-wallet history remains available without a time limit.

### FR-11 — Owner bank-account connection

The system shall provide the owner, through the Owner Panel only, with the ability to connect a bank account to the cafe wallet.

**Includes:**
- An owner-only entry point to connect a predefined FASTBite demo bank account to the cafe wallet.
- Demo account credentials/details supplied by the application; no external bank/provider is used.
- Simulated verification and connection outcomes: Connected, Failed, or Pending.
- A simulated OTP step using a clearly displayed demo OTP for demonstration purposes; no SMS or email provider is required.
- Owner ability to view connection status and demo account identifier, disconnect, and reconnect.
- Simulated deposits from the demo bank account to the cafe wallet and simulated withdrawals from the cafe wallet to the demo bank account.
- A transaction record for every simulated operation, including amount, timestamp, operation type, status, and demo reference.
- Simulated failure responses for invalid demo credentials/OTP, disconnected account, insufficient cafe-wallet funds, and temporary simulator failure.
- Clear labels stating that the account and every transaction are simulated.

**Acceptance criteria:**
- The bank-connection feature is visible and usable only in the Owner Panel.
- A cashier/accountant or student is denied access even if a direct API route is attempted.
- A connection is shown as Connected only after simulated verification succeeds.
- The owner can disconnect and reconnect the demo account.
- Deposits and withdrawals update the simulated cafe-wallet ledger exactly once and create an auditable transaction record.
- Failed operations do not change balances.
- Duplicate requests do not duplicate a simulated transfer.
- No real banking credentials, provider APIs, or real money movement are used.

### FR-12 — Cafe opening, closing, and operational continuity

The system shall allow authorized cashier/accountant staff and the owner to open and close the cafe and shall apply the approved order-handling rules when the cafe closes.

**Includes:**
- Manual opening and closing.
- Browsing the menu while closed.
- Blocking new orders while closed.
- Cancelling orders awaiting counter approval or customer decisions at closure, with applicable refund handling.
- Allowing already-approved and Ready to Pick orders to continue through collection after closure.
- Maintaining order records and status consistency during closure.

**Acceptance criteria:**
- Only authorized staff can open or close the cafe.
- New orders cannot be accepted while the cafe is closed.
- Orders awaiting approval or customer decisions follow the approved closure-cancellation rule.
- Already-approved and Ready to Pick orders are not cancelled merely because the cafe closes.

### FR-13 — Reports, financial records, and exports

The system shall provide operational reporting to authorized users and full cafe financial reporting to the owner only.

**Includes:**
- Today's sales total.
- Order history by selected calendar date.
- Cafe-wallet balance and withdrawal history.
- Refund logs.
- Cafe-wallet transaction history export as PDF, filtered by date range and transaction type.
- Excel and PDF exports for other report data where explicitly supported.
- Owner-only access to cafe financial reports and financial exports.
- No cafe-wallet or financial-report access from the Cashier / Accountant Panel.

**Acceptance criteria:**
- The owner can view the required cafe financial reports and exports.
- A cashier/accountant cannot view or export cafe financial data.
- An empty selected order-history date displays “No orders.”
- The selected date filter applies to order history only where the approved reporting rule says so.
- Today's sales subtract refunds issued today, regardless of the original order date.
- Exported data matches the authorized records and selected filters.

### FR-14 — Audit records, retention, and data integrity

The system shall preserve the operational and financial records required by the approved project decisions, apply separate retention rules, and prevent duplicate or inconsistent data effects.

**Includes:**
- Records of relevant order events, including new orders, approvals, cancellations, and order-status changes.
- Records supporting wallet transactions, refunds, and financial reports.
- Customer order-history and receipt deletion after the approved three-month period.
- Indefinite student-wallet transaction-history retention.
- Cafe-wallet transaction-history retention without a time limit.
- Preservation of historical order-item details after menu edits or deletion.
- Prevention of duplicate order creation, duplicate order numbering, duplicate debits, duplicate refunds, and duplicate stock restoration.
- Enforcement of role and data boundaries.

**Acceptance criteria:**
- Repeated requests do not duplicate orders or financial effects.
- Historical order details remain unchanged after menu changes.
- Retention rules are applied separately to each record category.
- Audit/report records support the approved operational and financial review needs.
- Owner-only financial records are inaccessible to cashier/accountant users.

### FR-15 — Customer Favorites

The system shall allow customers to add menu items to a personal Favorites list, view their saved items, and remove items from the list. The system shall display each favorite item's current price and availability and clearly identify items that are no longer available for ordering.

**Includes:**
- Adding an eligible menu item to the signed-in customer's personal Favorites list.
- Viewing the customer's saved Favorites items.
- Removing an item from the Favorites list.
- Displaying the current menu price for each favorite item.
- Displaying current availability and clearly identifying items that are unavailable for ordering.
- Keeping each customer's Favorites list private to that customer.

**Acceptance criteria:**
- A customer can add a menu item to their own Favorites list.
- A customer can view and remove items from their own Favorites list.
- Each favorite item displays its current menu price and current availability.
- An unavailable favorite remains identifiable in the list but is clearly marked as unavailable for ordering.
- A customer cannot view or modify another customer's Favorites list.

### FR-16 — Reorder from Order History

The system shall allow customers to start a new order using items and quantities from a previous order available in their Order History. The system shall check current item availability and stock, apply current menu prices, and allow customers to modify the cart before placing the new order through the existing ordering and payment workflow.

**Includes:**
- Selecting an eligible previous order from the customer's Order History.
- Starting a new cart using the items and quantities recorded in that previous order.
- Rechecking current menu availability and countable stock for each item.
- Applying current menu prices rather than historical prices.
- Identifying items that are no longer available or whose requested quantities exceed current stock.
- Allowing the customer to modify the new cart, including quantities and items, before submission.
- Submitting the new order through the existing order submission, PIN, approval, Final Accept, and payment workflow.
- Creating a new order record and order number; the previous order remains unchanged.

**Acceptance criteria:**
- A customer can initiate a new cart from an order available in their own Order History.
- The new cart initially uses the previous order's items and quantities where they remain eligible.
- Current availability and stock are checked before the new order is submitted.
- Current menu prices are used in the new cart and total.
- Unavailable items and quantities exceeding current stock are clearly identified and cannot be submitted as-is.
- The customer can modify the cart before placing the new order.
- Reordering creates a new order and does not alter the previous order, receipt, or transaction history.
- The new order follows the existing ordering and payment workflow, including duplicate-submission prevention.

### FR-17 — Configurable minimum stock thresholds and low-stock warnings

The system shall allow authorized cafe staff to configure a minimum stock threshold for each countable menu item. The system shall display a low-stock warning when an item's remaining quantity reaches or falls below its configured threshold and provide authorized staff with a list of all items currently below their thresholds.

**Includes:**
- Configuring and updating a minimum stock threshold for each countable menu item by staff with the required menu/stock permission.
- Evaluating the remaining quantity of each countable item against its configured threshold.
- Displaying a low-stock warning when remaining quantity is equal to or less than the configured threshold.
- Providing an authorized staff view/list of all countable items currently at or below their configured thresholds.
- Updating warning/list status when stock quantity or the configured threshold changes.
- Restricting threshold configuration and low-stock information to authorized cafe staff; customers do not receive staff stock-management controls.

**Acceptance criteria:**
- Authorized staff can set and update a minimum stock threshold for a countable menu item.
- When remaining quantity reaches or falls below the configured threshold, the system displays a low-stock warning.
- The low-stock list includes all countable items whose remaining quantity is at or below their configured thresholds.
- Items above their configured thresholds are not shown as currently low-stock.
- The warning and list update when stock quantity or the threshold changes.
- Staff without the required permission cannot configure thresholds or access restricted stock-management functions.
- Thresholds apply to countable menu items; availability-based items without tracked quantities are not assigned a quantity threshold under this requirement.

## 8. Non-functional requirements

The integrated PRD consolidates the project NFRs into four measurable requirements.

### NFR-01 — Performance and capacity

The system shall:
- Support at least 5,000 orders in a 24-hour test period.
- Support a peak test rate of 100 orders per minute.
- Make 95% of covered order creation and status-update events visible on relevant screens within 3 seconds.
- Make the latest order status visible within 10 seconds after connectivity is restored.

Covered events include new orders, approvals, cancellations, and order-status changes.

### NFR-02 — Reliability and transaction integrity

The system shall demonstrate:
- Zero lost or duplicated orders during the agreed 24-hour, 5,000-order test.
- No repeated order number across days or concurrent submissions.
- No duplicate wallet debit, refund, or stock restoration from retries or repeated actions.
- Consistency between order status, accepted items, stock changes, wallet transactions, refunds, and receipts.

### NFR-03 — Security and role-based access

The system shall:
- Enforce the three-panel access boundaries on every protected operation and data request.
- Prevent cashier/accountant users from accessing cafe-wallet finances, bank-account connection, bank-account details, financial reports, and finance exports.
- Restrict bank-account connection and cafe financial operations to the owner.
- Restrict customers to their own personal, order, receipt, and wallet records.
- Store customer PINs in a non-readable protected form.
- Apply the distinct customer PIN and cafe-wallet password failure rules.
- Deny unauthorized direct-route and reused-session access.

### NFR-04 — Usability and task completion

Under the approved usability-test conditions:
- At least 4 out of 5 first-time customers shall complete sign-up, find an item, place an order, and view the receipt without assistance in less than 3 minutes.
- The main counter approval action shall require no more than 2 taps in the approved workflow.
- The three panels shall identify their user context clearly and shall not expose controls that the current role is not authorized to use.
- Order, payment, receipt, wallet, and bank-connection outcomes shall clearly communicate success, failure, or pending status.

## 9. Business rules and constraints

1. Customers may use FASTBite regardless of FAST affiliation.
2. The Student Panel remains unchanged by the panel restructuring.
3. The Cashier / Accountant Panel has operational capabilities only and no cafe-wallet financial access.
4. The Owner Panel includes all cashier/accountant capabilities and all cafe financial capabilities.
5. Only the owner can connect or manage the cafe bank-account connection.
6. Student and cafe wallets are simulated under the previously approved wallet rules. The newly requested bank connection is a separate scope change whose live/sandbox behavior must be decided.
7. Customer PINs do not lock after repeated incorrect attempts; the system displays an incorrect-PIN message.
8. Cafe-wallet access follows its own password lockout and re-authentication rules.
9. Order numbers continue from the previous day's last number and are never reused.
10. One valid submission creates one order; retries must not duplicate it.
11. Countable stock is deducted and restored according to the approved stock rules.
12. Menu deletion is allowed at any time and must not erase historical order details.
13. Final Accept rechecks the student's wallet balance before charging accepted items.
14. If the cafe wallet cannot fund a required refund, the affected item remains uncancelled until funds are sufficient.
15. A collected order cannot be collected a second time.
16. The cafe can be opened and closed manually by authorized operational users.
17. New orders are blocked while the cafe is closed; already-approved orders continue according to the approved closure rules.
18. Customer order history and receipts follow the three-month retention rule; student-wallet and cafe-wallet histories follow their separate retention rules.
19. Financial reports and cafe-wallet exports are owner-only under the three-panel model.

## 10. User flows

This section describes the sequence of screens and actions from each user's perspective. These are textual user flows; they define navigation and user interaction without claiming that final visual wireframes have already been designed.

### 10.1 Student Panel — registration and login flow

1. Student opens FASTBite.
2. Student selects the Student Panel.
3. Student chooses Sign Up or Log In.
4. For sign-up, student enters the required registration details.
5. System performs the approved verification step.
6. Student sets a PIN at the applicable first-login stage.
7. System creates/authenticates the account.
8. Student lands on the Student Panel home screen.
9. If login or verification fails, the system displays the applicable error and permits the approved retry/recovery path.

### 10.2 Student Panel — browse and place order flow

1. Student opens Menu.
2. System displays menu items, prices, pictures where available, categories, and availability/quantity.
3. Student searches or filters by category and/or price range.
4. Student opens an item and selects a quantity where applicable.
5. Student adds the item to Cart.
6. Student repeats the selection for additional items.
7. Student opens Cart and reviews items, quantities, and total.
8. System revalidates availability, quantity, and latest prices.
9. Student proceeds to order submission and enters the PIN at the applicable step.
10. System processes the order according to the approved order/payment sequence.
11. System displays the order number and current status.
12. Once Final Accept and payment are successful, the receipt is generated and made available to the student and cafe.

### 10.3 Student Panel — Favorites flow

1. Student opens Favorites from the Student Panel.
2. System displays the student's saved menu items.
3. For each item, system displays its current menu price and availability.
4. System clearly marks items that are no longer available for ordering.
5. Student may remove an item from Favorites.
6. Student may return to the menu to browse or add other items to Favorites.

### 10.4 Student Panel — reorder from Order History flow

1. Student opens My Orders / Order History.
2. Student selects a previous order available in their history.
3. Student selects the option to start a new order from that previous order.
4. System creates a new cart using the previous order's items and quantities.
5. System checks current item availability and countable stock.
6. System applies current menu prices and recalculates the cart total.
7. System identifies unavailable items or quantities that exceed current stock.
8. Student modifies the cart as needed.
9. Student proceeds through the existing order submission and payment workflow.
10. System creates a new order record and order number; the previous order remains unchanged.

### 10.5 Student Panel — wallet flow

1. Student opens Wallet.
2. System displays the student's own wallet balance.
3. Student selects Deposit or Withdraw.
4. Student enters an amount.
5. System validates the permitted range and, for withdrawals, available balance.
6. System applies the approved simulated transaction and 2% withdrawal fee where relevant.
7. System updates the wallet balance and transaction history.
8. System sends the applicable notification.
9. Student may open transaction history and use the supported date-range export.

### 10.6 Student Panel — unavailable-item decision flow

1. Cafe-side processing identifies an unavailable item in an order.
2. System moves the affected order into the applicable exceptional-case workflow.
3. System notifies the student and identifies the affected item.
4. Student chooses Continue Without Item or Cancel Whole Order, subject to the applicable decision window.
5. System records the decision.
6. If continuing, the unavailable item is excluded and the remaining order follows the approved Final Accept and payment process.
7. If cancelling the whole order, the system follows the approved full-cancellation and refund process.
8. If a required refund cannot be funded by the cafe wallet, the affected item remains uncancelled until sufficient funds are available.
9. The system updates the order and receipt records when the relevant processing succeeds.

**Open behavior:** The exact outcome for an expired decision window, overlapping item windows, and a customer who reconnects after expiry must follow an explicit team decision; it is not inferred in this flow.

### 10.7 Cashier / Accountant Panel — operational order flow

1. Staff member opens FASTBite and selects Cashier / Accountant Panel.
2. System authenticates the staff account and loads only its permitted operational functions.
3. Staff opens the order-management view.
4. System displays incoming orders and relevant lists/tabs.
5. Staff opens an order and reviews items and fulfilment information.
6. Staff performs only the actions allowed by their assigned permissions.
7. If preparation is required, authorized staff select the approved timer.
8. Staff update the order through the approved preparation/readiness lifecycle.
9. When the customer presents the receipt/order number, authorized staff verify it against the cafe record.
10. Staff record Collected after the required verification.
11. System prevents a second collection of the same order.

At no point in this flow does the cashier/accountant receive a cafe-wallet finance or bank-connection option.

### 10.8 Cashier / Accountant Panel — menu and stock flow

1. Staff opens Menu Management.
2. System checks the staff member's menu permissions.
3. Staff adds or edits an item, its category, price, optional picture, preparation classification, and stock type.
4. For countable items, staff enters the required starting quantity or next-day quantity.
5. For availability-based items, staff sets Available or Unavailable.
6. Staff saves the change.
7. System validates the data and updates the customer menu.
8. System preserves historical item details in existing orders.
9. Authorized staff may configure or update the item's minimum stock threshold.
10. System compares remaining countable stock with the configured threshold and displays a low-stock warning when stock is at or below it.
11. Authorized staff may open the low-stock list to view all countable items currently at or below their thresholds.
12. If staff lacks permission, the system denies the action and records the applicable access outcome.

### 10.9 Owner Panel — operational flow

1. Owner opens FASTBite and selects Owner Panel.
2. System authenticates the owner.
3. Owner sees the owner dashboard.
4. Owner can perform all cashier/accountant operational actions, including order processing, menu/stock management, receipt verification, collection, and cafe opening/closing.
5. Owner can also open the finance area, which is not available in the Cashier / Accountant Panel.

### 10.10 Owner Panel — cafe wallet and finance flow

1. Owner opens Finance / Cafe Wallet.
2. System requests the cafe-wallet credentials where required.
3. Owner authenticates.
4. System grants access to the permitted cafe-wallet operations.
5. Owner may view transaction history, perform an allowed withdrawal, or open financial reports.
6. System locks/requires re-authentication according to the cafe-wallet rules after an operation or Back action.
7. System records the relevant financial event.

### 10.11 Owner Panel — bank-account connection flow

1. Owner opens Owner Panel.
2. Owner opens Finance / Bank Account Connection.
3. System verifies that the current user has the owner role.
4. Owner selects Connect Bank Account.
5. System starts the bank-connection process using the method/provider approved by the team.
6. Owner completes the required bank-side authentication/authorization.
7. System displays Connected only after receiving a successful confirmation from the approved connection process.
8. If the process fails or is cancelled, system displays the corresponding outcome and does not claim a successful connection.

**Not yet specified:** provider selection, authentication steps, account verification, consent, connection expiry, disconnection, supported transfers, error handling, and whether the integration is live or sandbox.

### 10.12 Owner Panel — reports and exports flow

1. Owner opens Reports.
2. System displays the authorized financial and operational report categories.
3. Owner selects an order-history date where applicable.
4. System displays the selected date's order history or “No orders.”
5. Owner selects an available export format.
6. System validates the owner's access and produces the export using the selected filters.
7. System records the export event where required by the audit rules.

## 11. Process flows

Process flows describe the system-side sequence, decisions, and resulting state changes. They complement the user flows above.

### 11.1 Order processing process

1. Receive order submission.
2. Validate customer, PIN, cart contents, item availability, and stock.
3. Check whether the request has already been processed.
4. If duplicate, return the existing order result rather than creating another order.
5. If valid, create one order record and assign the next continuous unique order number.
6. Display the order to the appropriate cafe-side users.
7. Keep the order Pending until the authorized counter action.
8. Process approval, unavailable-item handling, and Final Accept according to the applicable rules.
9. At Final Accept, recheck student-wallet balance.
10. If sufficient, charge accepted items and continue acceptance.
11. If insufficient, prevent acceptance, return the order to Pending, and require a new order as specified.
12. Generate the receipt and update the relevant status.
13. Continue preparation and readiness.
14. Verify receipt/order information at pickup.
15. Mark Collected once only.

### 11.2 Unavailable-item and refund process

1. Detect or record an unavailable item.
2. Notify the customer and create the item's decision window.
3. Record the student's choice or the applicable timeout result only where that outcome has been explicitly approved.
4. If customer continues, exclude the unavailable item.
5. If customer cancels the whole order, apply the full-order cancellation path.
6. Determine whether the relevant amount was charged.
7. Do not create a refund for an amount that was not charged.
8. If a required cafe-wallet-funded refund is underfunded, keep the affected item uncancelled and the refund pending.
9. When sufficient funds exist, process the refund once and update the item/order/receipt records.
10. Notify the relevant user according to the approved notification behavior.

### 11.3 Stock process

1. Staff create or update a menu item.
2. System validates required item fields.
3. For countable items, save the configured quantity.
4. For availability-based items, save the manually selected availability.
5. On qualifying order placement, deduct countable stock once.
6. On qualifying cancellation, restore stock once.
7. Block requests that exceed remaining stock or select unavailable items.
8. At the configured daily reset, apply the latest saved next-day quantity if present.
9. If no next-day quantity exists, do not perform an assumed reset; flag the missing configuration.

### 11.4 Cafe closure process

1. Authorized user selects Close Cafe.
2. System changes cafe state to Closed.
3. System blocks new order acceptance.
4. System identifies orders awaiting approval or customer decisions.
5. System applies the approved cancellation/refund behavior to those orders.
6. System leaves already-approved and Ready to Pick orders active for normal completion.
7. System continues to allow menu browsing.
8. Authorized user may reopen the cafe manually.

### 11.5 Owner bank-connection process

1. Receive a bank-connection request from the Owner Panel.
2. Verify the authenticated user is the owner.
3. Reject requests from student or cashier/accountant identities.
4. Start the approved provider/connection flow.
5. Receive and validate the provider's connection result.
6. Store/display connection status according to the approved security and data-handling decision.
7. Do not expose connection credentials or sensitive bank data in the Cashier / Accountant Panel.
8. Record connection success/failure for audit where required.

The exact provider-specific steps remain open.

## 12. Wireframe flows (screen-to-screen structure)

This section records the required wireframe flows as a textual screen map. It does not claim that final pixel-level wireframes or visual designs are complete.

### 12.1 Entry and panel selection

```text
[FASTBite Launch]
       |
       v
[Sign In / Sign Up]
       |
       v
[Choose / Resolve User Panel]
       |--------------------|----------------------|
       v                    v                      v
[Student Panel Home] [Cashier / Accountant] [Owner Panel Home]
```

The system must show only the panel available to the authenticated account. If role selection is not used in the final authentication design, the system resolves the panel from the authenticated account role.

### 12.2 Student Panel wireframe flow

```text
[Student Home]
   |----> [Menu] ----> [Search / Filter] ----> [Item Details]
   |                                      \----> [Cart]
   |                                             |
   |                                             v
   |                                      [Review Cart]
   |                                             |
   |                                             v
   |                                      [PIN / Submit]
   |                                             |
   |                                             v
   |                                      [Order Status]
   |                                             |
   |                                             v
   |                                      [Receipt]
   |
   |----> [Student Wallet] ----> [Deposit / Withdraw]
   |                         \--> [Transaction History]
   |
   |----> [My Orders] --------> [Order Details / Receipt] ----> [Reorder]
   |
   |----> [Favorites] --------> [Saved Items / Current Price / Availability]
   |
   \----> [Profile / Recovery]
```

### 12.3 Cashier / Accountant Panel wireframe flow

```text
[Cashier / Accountant Home]
   |----> [Orders] ----> [Order Details]
   |                    |----> [Review / Approve / Cancel]
   |                    |----> [Unavailable Item Handling]
   |                    |----> [Preparation / Timer / Status]
   |                    \----> [Receipt Verification / Collected]
   |
   |----> [Menu Management] ----> [Add / Edit / Delete Item]
   |                           \-> [Availability / Stock / Minimum Threshold]
   |                           \-> [Low-Stock Warnings / Low-Stock List]
   |
   |----> [Cafe Open / Close]
   |
   \----> [Operational Records / Permitted Views]

[No Cafe Wallet Finance]
[No Bank Account Connection]
[No Cafe Financial Reports]
```

### 12.4 Owner Panel wireframe flow

```text
[Owner Home]
   |----> [Orders] ----------------> [Same Operational Flow as Cashier]
   |
   |----> [Menu / Stock] ----------> [Same Operational Flow as Cashier]
   |                                  -> [Minimum Thresholds / Low-Stock List]
   |
   |----> [Cafe Open / Close]
   |
   |----> [Cafe Wallet / Finance] -> [Authenticate]
   |                              -> [Balance / Transactions]
   |                              -> [Withdraw]
   |
   |----> [Reports / Exports]
   |
   \----> [Bank Account Connection]
                                  -> [Connect Bank]
                                  -> [Connection Status]
                                  -> [Manage Connection]
```

Owner Panel includes the cashier/accountant functions, but the finance and bank-connection screens are not available in the Cashier / Accountant Panel.

## 13. Edge cases and failure handling

### 13.1 Account and access

- Invalid registration or verification details.
- Incorrect customer PIN; show error without customer PIN lockout.
- Customer attempts to access another customer's record.
- Cashier/accountant attempts to open an owner-only finance route.
- Cashier/accountant attempts to view bank-account connection details or initiate a connection.
- Owner session expires while using finance functions.
- A user attempts an operation without the required permission.

### 13.2 Menu and stock

- Item has no optional picture.
- Search/filter returns no results.
- Item becomes unavailable while customer is browsing or has it in the cart.
- Requested countable quantity exceeds remaining stock.
- Countable item has no starting quantity or has zero quantity.
- Next-day quantity is changed before midnight.
- No next-day quantity is configured.
- Duplicate item names are entered; identical names are blocked under the accepted rule, while capitalization-only differences are not treated as duplicates.
- Item is deleted while existing orders refer to it; historical details remain intact.
- Staff without menu permission attempts to edit or delete an item.
- A countable item's remaining quantity reaches or falls below its configured minimum stock threshold.
- A threshold is changed while the item's current quantity is already below the new threshold.
- A countable item has no configured minimum stock threshold.
- A staff member without stock permission attempts to view the low-stock list or change a threshold.

### 13.3 Favorites and reorder

- Customer has no saved Favorites items.
- A favorite item is edited, repriced, or marked unavailable after it was saved.
- Customer attempts to add an unavailable favorite to a cart.
- Customer attempts to access another customer's Favorites list.
- A previous order contains an item that has since been deleted or made unavailable.
- A previous order contains a quantity greater than the item's current remaining stock.
- Menu prices have changed since the previous order.
- Customer removes or changes items/quantities in a reorder cart before submission.
- The original order is no longer available in the customer's Order History under the applicable retention rule.

### 13.4 Order submission and numbering

- Customer taps Place Order repeatedly.
- Connection is lost during submission or payment.
- Two or more orders are submitted concurrently.
- Order-number allocation is attempted across a day boundary.
- Student wallet balance is insufficient at the applicable payment step.
- Item price changes while it is in the cart.
- Cafe closes while the customer is preparing to submit an order.

### 13.5 Unavailable items and refunds

- One or multiple items become unavailable.
- Each item has a separate five-minute decision window.
- Customer does not respond before the window expires.
- Customer is offline during the decision window.
- Customer reconnects after a decision window expires.
- Customer cancels the whole order while other item decision windows remain open.
- Cafe wallet does not have sufficient funds for a required refund.
- A retry attempts to process the same refund twice.
- A refund is requested for an amount that was never charged.

Timeout outcome and interactions between multiple windows remain open wherever the decision log has not resolved them.

### 13.6 Receipt and collection

- Receipt generation fails.
- Automatic receipt retry is still in progress.
- Customer presents an incorrect order number or receipt.
- Receipt details do not match the cafe-side order.
- An order is already Collected.
- Staff without collection permission attempts to mark Collected.
- Collection is attempted while receipt generation is still failing; the system rejects collection and explains that receipt generation must succeed first.

### 13.7 Cafe wallet and owner finance

- Five incorrect cafe-wallet password attempts occur within the defined one-day window.
- Email OTP recovery is requested.
- Owner presses Back after wallet authentication.
- A wallet operation completes and the wallet must lock.
- A new wallet session starts on another device.
- Withdrawal is below PKR 500 or above PKR 80,000.
- Withdrawal exceeds cafe-wallet balance.
- Owner attempts a bank connection but cancels or fails authentication.
- Provider returns pending, failed, or unsuccessful connection status.
- Cashier/accountant attempts to connect, disconnect, or view the bank connection.
- Bank connection is lost or expires; exact behavior requires the bank-integration decision.

### 13.8 Cafe closure

- Cafe closes while an order awaits approval.
- Cafe closes while a customer decision is pending.
- Cafe closes after an order is approved.
- Cafe closes while an order is Ready to Pick.
- A new order is submitted while cafe is closed.
- An approved order remains uncollected after closing.

### 13.9 Reports and retention

- Selected order-history date has no orders.
- Refund issued today relates to an older order.
- Export is requested by an unauthorized cashier/accountant user.
- Selected date range or transaction-type filter returns no records.
- Customer order history is older than three months.
- Student-wallet transaction history is older than three months and must still remain.
- Cafe-wallet transaction history is old and must remain available.
- Customer account deletion conflicts with wallet-history retention; follow the open decision rather than silently deleting retained financial records.

## 14. Acceptance criteria summary

The PRD is accepted for implementation planning when the following can be demonstrated:

1. Three separate panels exist: Student, Cashier / Accountant, and Owner.
2. The Student Panel's previously agreed features remain unchanged.
3. Cashier/accountant users can perform only their assigned operational actions.
4. Cashier/accountant users cannot access cafe-wallet finances, financial reports, bank-account details, or bank-account connection.
5. Owner users can perform all cashier/accountant operational actions.
6. Owner users alone can access cafe-wallet finances, reports, and bank-account connection.
7. Customers can register, log in, browse, filter, cart, and submit orders.
8. Order numbering is continuous and unique.
9. Orders cannot be duplicated by retries or repeated submissions.
10. The order review, Final Accept, unavailable-item, refund, receipt, preparation, and collection processes follow their approved rules.
11. Menu and stock changes are reflected correctly and historical order details are preserved.
12. Student wallet operations apply the approved limits and 2% withdrawal fee.
13. Cafe wallet operations apply the approved limits, authentication, lockout, and re-authentication rules.
14. Cafe closure prevents new orders while already-approved orders continue.
15. Reports and exports are restricted to the owner where they contain cafe financial information.
16. Retention rules are applied separately to order history, receipts, and wallet histories.
17. The system meets the four measurable NFRs.
18. Customers can add, view, and remove Favorites items, with current price and availability displayed.
19. Customers can start a new order from Order History using current prices and stock validation, modify the cart, and submit through the existing workflow.
20. Authorized staff can configure minimum stock thresholds, receive warnings at or below thresholds, and view the low-stock item list.

## 15. Decisions resolving implementation-critical questions

The following decisions close the implementation-critical questions identified during TA review. Where the original PRD did not prescribe a precise behavior, the selected rule is a conservative project decision made to make the prototype implementable and testable. These decisions do not introduce new product features beyond defining the behavior of existing requirements.

| ID | Decision | Resolution |
|---|---|---|
| OQ-01 | Bank integration type | Internal simulated/demo bank account only. No live bank integration. |
| OQ-02 | Bank/provider | FASTBite's own internal simulator; no external provider. |
| OQ-03 | Supported bank operations | Demo account verification/connection, status display, simulated deposits, simulated withdrawals, transaction history, and simulated success/failure. |
| OQ-04 | Connection/authentication lifecycle | Owner opens Bank Connection, selects the predefined demo account, enters demo credentials and displayed demo OTP, and submits. Simulator returns Connected, Failed, or Pending. Owner can disconnect/reconnect. A disconnected account cannot transact. No real credentials or external OTP service. |
| OQ-05 | Staff account administration | Owner can create, deactivate, and assign operational permissions to cashier/accountant accounts. Students cannot access staff administration. |
| OQ-06 | Cashier/accountant permissions | Use the permission matrix in Section 5.6. Operational access is assigned by the owner. Cancellation/refund and cafe open/close are denied by default unless explicitly delegated. Finance and bank functions are always owner-only. |
| OQ-07 | Order-state model | Valid lifecycle: Pending → Approved/Cooking → Ready to pick → Collected. Cancellation may occur from Pending or Approved/Cooking only where the business rules permit; final state is Cancelled/Refunded (refund may remain Pending). Collected and Cancelled are terminal and cannot be reopened. Ready-made-only orders may move from Approved to Ready to pick without a cooking timer. |
| OQ-08 | Five-minute unavailable-item timeout | Each unavailable item has its own five-minute server-timed window. If no response arrives, remove that item and continue with remaining available items; if none remain, cancel the order. Refund only amounts already charged. Notify the customer. |
| OQ-09 | Multiple unavailable items | Each item has an independent decision record and deadline. If the customer chooses whole-order cancellation, close all other open windows as Cancelled by order decision and process one order-level refund for the amount actually charged. No duplicate item/order refunds. |
| OQ-10 | Customer offline during decision | The five-minute deadline continues using server time. On reconnect, show the recorded outcome. A late response cannot reverse the timeout outcome. |
| OQ-11 | Receipt failure and collection | Collection is blocked until receipt generation succeeds and the receipt is available for verification. Retry continues and staff see the failure/pending state. |
| OQ-12 | One-day failed-password window | Use a rolling 24-hour window from the first failed authentication attempt. The wallet is locked after five consecutive failed attempts within that window. A successful authentication resets the consecutive-failure count. Unlock occurs 24 hours after the lock timestamp; owner support may follow the approved recovery process but does not bypass audit logging. |
| OQ-13 | Preparation timer and statuses | For To-Cook items, staff select the applicable approved timer value (1, 2, 3, 5, or 10 minutes). The order's countdown uses the longest preparation time among accepted To-Cook items. Ready-made-only orders become Ready to pick after approval/Final Accept. When the countdown completes, status becomes Ready to pick. |
| OQ-14 | Menu item deleted while in-flight | Deletion prevents the item from appearing in new orders but does not delete historical order snapshots or invalidate an already accepted order. For a Pending order, staff must resolve the item through the unavailable-item process. For an accepted/in-preparation order, preserve the accepted item and fulfilment record; do not silently remove it. |
| OQ-15 | Three-month retention calculation | Retain customer order history and receipts for three calendar months from order completion/cancellation timestamp, then delete or anonymize them through a scheduled daily retention job. Preserve records that must remain for financial/audit integrity in the separately governed ledger/audit records, without exposing deleted customer-facing history. |
| OQ-16 | Student-wallet history after account deletion | Do not erase wallet ledger entries needed for financial integrity. Deactivate/anonymize the customer identity association as permitted, while retaining transaction records and required audit references. Customer-facing access ends when the account is deleted. |
| OQ-17 | Reporting day/time zone | Use Pakistan Standard Time (PKT, UTC+05:00) and a calendar-day boundary of 00:00 PKT for daily cafe sales reports. Store timestamps in UTC and convert for display/report grouping. |
| OQ-18 | Audit fields and retention | Record actor ID/role, action, target record, timestamp (UTC), outcome, and relevant before/after values for bank connection changes, simulated deposits/withdrawals, refunds, permission changes, and finance actions. Retain these audit/financial records for the lifetime of the academic dataset; restrict access to the owner and authorized technical administrators. Do not log passwords, OTP values, or secrets. |
| OQ-19 | Owner operational access | Owner has all operational capabilities and does not require a cashier account. Owner actions remain auditable. Operational permissions can be delegated to cashier/accountant staff, but cafe-wallet finance and bank-connection permissions cannot be delegated. |

### 15.1 Order status transition rules

| Current status | Event / condition | Next status | Rule |
|---|---|---|---|
| Pending | Staff begins review | Pending | Review alone does not approve the order. |
| Pending | Staff approves and Final Accept succeeds | Approved/Cooking | Accepted items and payment/stock effects are committed consistently. |
| Pending | All accepted items are ready-made | Ready to pick | May skip Cooking timer. |
| Pending | Whole order cancelled | Cancelled/Refunded | Refund status is tracked separately and may remain Pending. |
| Approved/Cooking | Preparation timer completes / staff marks ready where permitted | Ready to pick | Only accepted items are included. |
| Approved/Cooking | Permitted cancellation | Cancelled/Refunded | Apply applicable refund and stock-restoration rules exactly once. |
| Ready to pick | Receipt generated and verified at pickup | Collected | Collection is recorded once only. |
| Collected | Any later status change request | No change | Terminal state; reject request. |
| Cancelled/Refunded | Any later status change request | No change | Terminal order state; refund lifecycle may continue independently. |

The order status and refund status are separate concepts. An order may be Cancelled while its refund is Pending; the system must not label the refund completed until the wallet transaction succeeds.

### 15.2 Demo bank connection lifecycle

```text
Disconnected
    |
    | Owner starts connection
    v
Verification Pending
    |                 |
    | verification    | invalid credentials / OTP
    | succeeds        v
    v               Failed
Connected             |
    |                  | Owner retries
    | Owner disconnects
    v
Disconnected
```

A Pending or Failed connection cannot initiate simulated deposits or withdrawals. A Connected account may initiate the supported simulated operations. A disconnect blocks new operations but does not erase historical demo transactions.

### 15.3 Decisions that remain subject to review

These decisions resolve the questions needed to implement and test the prototype. The team should review them against course policy and any later client/TA clarification. If the team changes a decision, update this section, the relevant FR/acceptance criteria, user/process flows, edge cases, and architecture/ADRs together.

## 16. Change log for this revision

| Area | Previous integrated PRD | Change in this revision |
|---|---|---|
| Panel structure | Two panels: Student and Admin/Cafe | Three panels: Student, Cashier / Accountant, Owner |
| Student Panel | Existing customer functionality | Explicitly preserved without changes from this panel restructuring |
| Cashier / Accountant Panel | Combined cafe-side operational and finance access was not cleanly separated | Retains operational features; all cafe-wallet finance and bank-connection access removed |
| Owner Panel | No separate owner panel | Added; includes all cashier/accountant features plus full cafe finance |
| Cafe wallet | Cafe wallet access governed by earlier integrated role arrangement | Owner-only access |
| Bank connection | Real bank integration previously excluded | Added as an owner-only requested capability; technical and provider details remain open |
| Functional requirements | Earlier integrated requirement set | Current PRD contains 17 functional requirements (FR-01 to FR-17), including Favorites, Reorder, and Low-Stock Thresholds |
| Flows | Main user scenarios existed, but not a dedicated three-panel flow structure | Added user flows, process flows, and textual wireframe flows for all three panels |
| Edge cases | Existing edge cases | Expanded to cover three-panel permissions, owner bank connection, Favorites, reordering, and low-stock thresholds |
| Customer convenience | Menu and Order History capabilities | Added Favorites management and reorder-from-history functionality |
| Stock monitoring | Stock quantities and availability management | Added configurable minimum stock thresholds, low-stock warnings, and an authorized low-stock list |
| NFRs | Multiple detailed NFR entries | Consolidated into four measurable NFRs |

## 17. Decision governance

- The latest explicit three-panel instruction governs the panel structure in this revision.
- The Student Panel is not to be altered as part of this change.
- The Cashier / Accountant Panel must not have access to cafe-wallet finances or bank-account connection.
- The Owner Panel includes the cashier/accountant operational features and exclusive cafe-finance/bank-connection capabilities.
- The bank-connection capability is recorded as a new requirement, but its implementation scope remains open until the team decides whether it is live or sandbox and defines the provider and supported behavior.
- Previously accepted decisions remain applicable unless this revision explicitly changes them.
- Open questions remain open until a team member makes and records a decision.
- Favorites, reorder-from-history, and low-stock threshold requirements are included as explicit functional requirements in this revision.
- Threshold configuration and low-stock visibility remain subject to the existing staff permission model.
- No technology, provider, financial operation, or permission is to be inferred without a recorded decision.

**End of FASTBite Integrated PRD.**
