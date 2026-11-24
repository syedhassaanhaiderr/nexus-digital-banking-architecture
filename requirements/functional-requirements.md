
# NEXUS Functional Requirements

## 1. Purpose

This document defines the functional requirements of the NEXUS Digital Banking and Payments Platform.

The requirements establish the business capabilities, system behaviour, operational processes and expected outcomes that the platform shall support.

These requirements will serve as inputs to architecture design, API specifications, database modelling, implementation and system testing.

## 2. Scope

The functional scope of NEXUS includes:

- Customer management
- Authentication and authorization
- Account management
- Digital wallet management
- Fund transfers
- Merchant payments
- Financial ledger management
- Transaction management
- Notification management
- Banking operations
- Reconciliation
- Reporting and audit

NEXUS is an educational reference platform. All customer information, financial transactions and external integrations shall be simulated.

## 3. Requirement Prioritization

Requirements are prioritized using the MoSCoW method.

| Priority | Description |
|---|---|
| Must Have | Essential for the platform to function |
| Should Have | Important but not essential for the initial release |
| Could Have | Desirable enhancement |
| Won't Have | Excluded from the current release |

## 4. Customer Management

### FR-CUS-001: Customer Registration

**Description**

The system shall allow new customers to register using basic fictional personal and contact information.

**Priority:** Must Have

**Stakeholders:** ST-01, ST-04

**Architecture Concerns:** CON-01, CON-04, CON-09

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-06

**Acceptance Criteria**

- A customer can submit valid registration information.
- Mandatory fields are validated.
- Duplicate registered email addresses are rejected.
- A unique customer identifier is generated.
- A customer profile is created successfully.

### FR-CUS-002: Customer Profile Retrieval

**Description**

The system shall allow authenticated customers to retrieve their own profile information.

**Priority:** Must Have

**Stakeholders:** ST-01

**Architecture Concerns:** CON-01, CON-09

**Architecture Viewpoints:** VP-03, VP-04, VP-06

**Acceptance Criteria**

- An authenticated customer can retrieve their profile.
- Unauthorized access to another customer's profile is rejected.
- Sensitive authentication information is excluded from the response.

### FR-CUS-003: Customer Profile Update

**Description**

The system shall allow authenticated customers to update permitted profile information.

**Priority:** Should Have

**Stakeholders:** ST-01, ST-03

**Architecture Concerns:** CON-01, CON-04, CON-07

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-06

**Acceptance Criteria**

- Customers can update permitted profile fields.
- Invalid information is rejected.
- The unique customer identifier cannot be modified.
- Profile changes are recorded for audit purposes.

### FR-CUS-004: Customer Status Management

**Description**

The system shall allow authorized banking operations staff to manage customer account-access status.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-07, ST-08

**Architecture Concerns:** CON-01, CON-04, CON-07

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-06

**Acceptance Criteria**

- Customer status can be Active, Suspended or Closed.
- Only authorized staff can modify customer status.
- Suspended and closed customers cannot initiate financial transactions.
- Status changes are recorded in the audit trail.

## 5. Authentication and Authorization

### FR-AUTH-001: Customer Authentication

**Description**

The system shall authenticate registered customers using valid login credentials.

**Priority:** Must Have

**Stakeholders:** ST-01, ST-07

**Architecture Concerns:** CON-01, CON-09

**Architecture Viewpoints:** VP-03, VP-05, VP-06

**Acceptance Criteria**

- Valid credentials result in successful authentication.
- Invalid credentials are rejected.
- Passwords are not stored or returned in plaintext.
- Suspended and closed customers are denied access.

### FR-AUTH-002: Session Management

**Description**

The system shall establish and manage authenticated user sessions.

**Priority:** Must Have

**Stakeholders:** ST-01, ST-05, ST-07

**Architecture Concerns:** CON-01, CON-09

**Architecture Viewpoints:** VP-03, VP-05, VP-06

**Acceptance Criteria**

- A successful login establishes an authenticated session.
- Sessions expire according to configured security policies.
- Expired or invalid sessions are rejected.
- Users can terminate their sessions through logout.

### FR-AUTH-003: Role-Based Access Control

**Description**

The system shall restrict access to functionality based on assigned user roles and permissions.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-05, ST-07, ST-08

**Architecture Concerns:** CON-01, CON-04, CON-07

**Architecture Viewpoints:** VP-03, VP-04, VP-06

**Acceptance Criteria**

- The system supports Customer, Merchant and Operations roles.
- Each role has explicitly defined permissions.
- Unauthorized actions are rejected.
- Customers can access only their own authorized resources.

### FR-AUTH-004: Failed Authentication Management

**Description**

The system shall detect and restrict repeated unsuccessful authentication attempts.

**Priority:** Must Have

**Stakeholders:** ST-07, ST-09

**Architecture Concerns:** CON-01, CON-07

**Architecture Viewpoints:** VP-03, VP-06, VP-07

**Acceptance Criteria**

- Failed authentication attempts are recorded.
- Repeated failed attempts trigger configured restrictions.
- Authentication failure events are available for security monitoring.
- Error messages do not disclose sensitive account information.

### FR-AUTH-005: Password Management

**Description**

The system shall allow users to securely change and reset their passwords.

**Priority:** Should Have

**Stakeholders:** ST-01, ST-07

**Architecture Concerns:** CON-01, CON-09

**Architecture Viewpoints:** VP-03, VP-05, VP-06

**Acceptance Criteria**

- Authenticated users can change their passwords.
- Passwords comply with configured security policies.
- Password reset requires identity verification.
- Password reset credentials are time-limited and single-use.



## 6. Account Management

### FR-ACC-001: Account Creation

**Description**

The system shall allow authorized banking operations staff to create simulated bank accounts for registered customers.

**Priority:** Must Have

**Stakeholders:** ST-01, ST-03

**Architecture Concerns:** CON-01, CON-04, CON-07

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-06

**Acceptance Criteria**

- An account is associated with an existing active customer.
- A unique account identifier is generated.
- The account currency is recorded.
- The initial account balance is zero.
- Account creation is recorded in the audit trail.

### FR-ACC-002: Account Information Retrieval

**Description**

The system shall allow authenticated customers to retrieve information about their own bank accounts.

**Priority:** Must Have

**Stakeholders:** ST-01

**Architecture Concerns:** CON-01, CON-04, CON-09

**Architecture Viewpoints:** VP-03, VP-04, VP-06

**Acceptance Criteria**

- Customers can retrieve their associated accounts.
- Account identifiers, currency and status are displayed.
- Unauthorized account access is rejected.

### FR-ACC-003: Account Balance Inquiry

**Description**

The system shall allow customers to retrieve the ledger balance and available balance of their accounts.

**Priority:** Must Have

**Stakeholders:** ST-01, ST-03

**Architecture Concerns:** CON-03, CON-04, CON-09

**Architecture Viewpoints:** VP-03, VP-04, VP-06

**Acceptance Criteria**

- The ledger balance reflects posted financial entries.
- The available balance reflects applicable active fund reservations.
- Balances are displayed with their associated currency.
- Balance information is consistent with the financial ledger.

### FR-ACC-004: Account Status Management

**Description**

The system shall allow authorized operations staff to manage the status of customer accounts.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-07, ST-08

**Architecture Concerns:** CON-01, CON-04, CON-07

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-06

**Acceptance Criteria**

- Accounts support Active, Frozen and Closed statuses.
- Frozen accounts cannot initiate new debit transactions.
- Closed accounts cannot initiate new financial transactions.
- Account closure requires a zero balance and no outstanding reservations.
- All status changes are recorded in the audit trail.

### FR-ACC-005: Account Transaction History

**Description**

The system shall allow customers to retrieve the transaction history associated with their accounts.

**Priority:** Must Have

**Stakeholders:** ST-01, ST-03

**Architecture Concerns:** CON-01, CON-04, CON-09

**Architecture Viewpoints:** VP-03, VP-04, VP-06

**Acceptance Criteria**

- Customers can retrieve their own account transactions.
- Transaction amount, currency, reference, date and status are displayed.
- Transactions can be filtered by date and transaction type.
- Unauthorized transaction history access is rejected.

## 7. Digital Wallet Management

### FR-WAL-001: Wallet Creation

**Description**

The system shall allow eligible registered customers to create simulated digital wallets.

**Priority:** Must Have

**Stakeholders:** ST-01, ST-04

**Architecture Concerns:** CON-01, CON-04, CON-09

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-06

**Acceptance Criteria**

- A wallet is associated with an active customer.
- A unique wallet identifier is generated.
- The wallet currency is recorded.
- The initial wallet balance is zero.

### FR-WAL-002: Wallet Balance Inquiry

**Description**

The system shall allow authenticated customers to retrieve their digital wallet balances.

**Priority:** Must Have

**Stakeholders:** ST-01

**Architecture Concerns:** CON-03, CON-04, CON-09

**Architecture Viewpoints:** VP-03, VP-04, VP-06

**Acceptance Criteria**

- Customers can retrieve their own wallet balances.
- Ledger and available balances are displayed.
- Wallet balances are consistent with posted financial entries and active reservations.
- Unauthorized wallet access is rejected.

### FR-WAL-003: Wallet Funding

**Description**

The system shall allow customers to fund their digital wallets using eligible simulated bank accounts.

**Priority:** Must Have

**Stakeholders:** ST-01, ST-03

**Architecture Concerns:** CON-01, CON-04, CON-07

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-05, VP-06

**Acceptance Criteria**

- The funding amount must be greater than zero.
- The source account and destination wallet must belong to the authenticated customer.
- The source account must have sufficient available funds.
- The account debit and wallet credit are posted atomically.
- A unique transaction reference is generated.
- Duplicate requests do not result in duplicate financial postings.

### FR-WAL-004: Wallet Withdrawal

**Description**

The system shall allow customers to transfer funds from their digital wallets to eligible simulated bank accounts.

**Priority:** Must Have

**Stakeholders:** ST-01, ST-03

**Architecture Concerns:** CON-01, CON-04, CON-07

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-05, VP-06

**Acceptance Criteria**

- The withdrawal amount must be greater than zero.
- The source wallet and destination account must belong to the authenticated customer.
- The wallet must have sufficient available funds.
- The wallet debit and account credit are posted atomically.
- A unique transaction reference is generated.
- Duplicate requests do not result in duplicate financial postings.

### FR-WAL-005: Wallet Status Management

**Description**

The system shall allow authorized operations staff to manage digital wallet statuses.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-07, ST-08

**Architecture Concerns:** CON-01, CON-04, CON-07

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-06

**Acceptance Criteria**

- Wallets support Active, Frozen and Closed statuses.
- Frozen wallets cannot initiate new debit transactions.
- Closed wallets cannot initiate new financial transactions.
- Wallet closure requires a zero balance and no outstanding reservations.
- Status changes are recorded in the audit trail.



## 8. Fund Transfers

### FR-TRF-001: Internal Fund Transfer

**Description**

The system shall allow authenticated customers to transfer funds between eligible accounts or wallets maintained within NEXUS.

**Priority:** Must Have

**Stakeholders:** ST-01, ST-03

**Architecture Concerns:** CON-01, CON-04, CON-07

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-06

**Acceptance Criteria**

- The source funding instrument belongs to the authenticated customer.
- The source and destination are valid and eligible for the transaction.
- The transfer amount is greater than zero.
- The source has sufficient available funds.
- The debit and credit entries are posted atomically.
- A unique transaction reference is generated.

### FR-TRF-002: External Fund Transfer

**Description**

The system shall allow customers to initiate fund transfers to simulated external bank accounts through a simulated payment provider.

**Priority:** Must Have

**Stakeholders:** ST-01, ST-03, ST-10

**Architecture Concerns:** CON-04, CON-05, CON-07

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-05, VP-06

**Acceptance Criteria**

- External beneficiary information is validated.
- Sufficient available funds are confirmed.
- Funds are reserved before external processing.
- A payment request is submitted to the simulated payment provider.
- The provider transaction reference is recorded when available.
- Financial posting and reservation release are performed according to the confirmed transaction outcome.

### FR-TRF-003: Transfer Validation

**Description**

The system shall validate fund transfer requests before financial processing.

**Priority:** Must Have

**Stakeholders:** ST-01, ST-03, ST-07

**Architecture Concerns:** CON-01, CON-04

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-06

**Acceptance Criteria**

- Mandatory request fields are validated.
- Source ownership and authorization are verified.
- Source and destination statuses are validated.
- Unsupported currency combinations are rejected.
- Insufficient funds result in transaction rejection.
- Invalid requests do not generate financial postings.

### FR-TRF-004: Transaction Limit Validation

**Description**

The system shall validate fund transfers against configured transaction limits.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-04, ST-07, ST-08

**Architecture Concerns:** CON-01, CON-04, CON-07

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-06

**Acceptance Criteria**

- Per-transaction limits are configurable.
- Daily cumulative transfer limits are configurable.
- Transfers exceeding applicable limits are rejected.
- Concurrent requests cannot bypass configured limits.
- Limit validation outcomes are recorded.

### FR-TRF-005: Duplicate Transfer Prevention

**Description**

The system shall prevent duplicate financial processing of the same fund transfer request.

**Priority:** Must Have

**Stakeholders:** ST-01, ST-03, ST-05

**Architecture Concerns:** CON-04, CON-07

**Architecture Viewpoints:** VP-03, VP-04, VP-05

**Acceptance Criteria**

- Transfer initiation supports an idempotency key.
- Repeated requests with the same key and equivalent payload return the existing transaction outcome.
- Reuse of the same key with a different payload is rejected.
- Duplicate requests do not generate additional financial postings.
- Duplicate detection is safe under concurrent processing.

### FR-TRF-006: Transfer Timeout Management

**Description**

The system shall manage external fund transfers for which a definitive payment response is not received within the configured timeout period.

**Priority:** Must Have

**Stakeholders:** ST-01, ST-03, ST-09, ST-10

**Architecture Concerns:** CON-02, CON-04, CON-05, CON-10

**Architecture Viewpoints:** VP-03, VP-04, VP-05, VP-07

**Acceptance Criteria**

- External payment response timeouts are detected.
- Transactions with uncertain outcomes are marked as Pending.
- A timeout alone does not trigger a definitive failure.
- Applicable fund reservations are maintained until the outcome is resolved.
- Transaction status inquiries can be initiated.
- Unresolved transactions are available for operational investigation.

### FR-TRF-007: Transfer Reversal

**Description**

The system shall support authorized reversal of eligible completed fund transfers.

**Priority:** Must Have

**Stakeholders:** ST-01, ST-03, ST-08

**Architecture Concerns:** CON-04, CON-07

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-05, VP-06

**Acceptance Criteria**

- The original transaction reference is required.
- Transaction reversal eligibility is validated.
- External transfers require a confirmed external reversal outcome.
- Reversal entries compensate for the original financial postings.
- Original ledger entries are preserved.
- Duplicate reversals are prevented.
- Reversal actions are recorded in the audit trail.

## 9. Merchant Payments

### FR-MER-001: Merchant Registration

**Description**

The system shall allow authorized banking operations staff to register simulated merchants.

**Priority:** Must Have

**Stakeholders:** ST-02, ST-03, ST-04

**Architecture Concerns:** CON-01, CON-04, CON-07

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-06

**Acceptance Criteria**

- A unique merchant identifier is generated.
- Merchant name and category information are recorded.
- A valid merchant payment account is associated with the merchant.
- Merchant registration is recorded in the audit trail.

### FR-MER-002: Merchant Payment Initiation

**Description**

The system shall allow authenticated customers to initiate payments to registered merchants using eligible accounts or wallets.

**Priority:** Must Have

**Stakeholders:** ST-01, ST-02, ST-03

**Architecture Concerns:** CON-01, CON-04, CON-09

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-05, VP-06

**Acceptance Criteria**

- The merchant identifier is validated.
- The merchant is active and eligible to receive payments.
- The customer funding source is authorized.
- Sufficient available funds are confirmed.
- Applicable transaction limits are validated.
- A unique payment reference is generated.
- Duplicate financial processing is prevented.

### FR-MER-003: QR-Based Merchant Payment

**Description**

The system shall support simulated QR-based merchant payment initiation.

**Priority:** Should Have

**Stakeholders:** ST-01, ST-02, ST-04

**Architecture Concerns:** CON-05, CON-09

**Architecture Viewpoints:** VP-02, VP-03, VP-05, VP-06

**Acceptance Criteria**

- A registered merchant can be associated with a simulated QR payload.
- The QR payload identifies the merchant.
- Invalid QR payloads are rejected.
- Merchant details and payment amount are displayed before customer confirmation.
- QR-based payments follow standard payment validation and processing rules.

### FR-MER-004: Merchant Payment Status Inquiry

**Description**

The system shall allow authorized merchants to retrieve the status of payments associated with their merchant profiles.

**Priority:** Must Have

**Stakeholders:** ST-02, ST-03

**Architecture Concerns:** CON-01, CON-04, CON-09

**Architecture Viewpoints:** VP-03, VP-04, VP-05, VP-06

**Acceptance Criteria**

- Payments can be retrieved using a valid transaction reference.
- The current transaction status is returned.
- Merchants can retrieve only their own payment transactions.
- Payment status information is consistent with transaction records.

### FR-MER-005: Merchant Payment Refund

**Description**

The system shall allow authorized merchants or operations staff to initiate refunds against eligible completed merchant payments.

**Priority:** Should Have

**Stakeholders:** ST-01, ST-02, ST-03

**Architecture Concerns:** CON-01, CON-04, CON-07

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-05, VP-06

**Acceptance Criteria**

- The original payment reference is required.
- Refund authorization and eligibility are validated.
- The refund amount must be greater than zero.
- The cumulative refunded amount cannot exceed the original payment amount.
- Applicable funding availability is validated.
- Refunds generate separate financial entries and transaction references.
- Duplicate refund processing is prevented.

### FR-MER-006: Merchant Status Management

**Description**

The system shall allow authorized banking operations staff to manage merchant statuses.

**Priority:** Must Have

**Stakeholders:** ST-02, ST-03, ST-08

**Architecture Concerns:** CON-01, CON-04, CON-07

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-06

**Acceptance Criteria**

- Merchants support Active, Suspended and Closed statuses.
- Suspended and closed merchants cannot receive new payments.
- Existing financial obligations remain available for resolution.
- Only authorized operations staff can modify merchant statuses.
- Status changes are recorded in the audit trail.



## 10. Financial Ledger Management

### FR-LED-001: Double-Entry Financial Posting

**Description**

The system shall record financial movements using double-entry accounting principles.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-05, ST-06, ST-08

**Architecture Concerns:** CON-04, CON-07

**Architecture Viewpoints:** VP-02, VP-03, VP-04

**Acceptance Criteria**

- Each financial posting generates a uniquely identifiable journal.
- Each journal contains at least two ledger entries.
- Total debit amounts equal total credit amounts for each currency.
- Unbalanced journals are rejected.
- Ledger entries are associated with their originating transaction reference.

### FR-LED-002: Atomic Financial Posting

**Description**

The system shall ensure that all ledger entries belonging to a financial journal are posted atomically.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-05, ST-06

**Architecture Concerns:** CON-04, CON-10

**Architecture Viewpoints:** VP-03, VP-04

**Acceptance Criteria**

- All entries within a journal are committed together.
- Failure of any entry prevents the entire journal from being committed.
- Partial financial postings are prevented.
- Balance updates remain consistent with committed ledger entries.

### FR-LED-003: Ledger Immutability

**Description**

The system shall preserve posted financial ledger entries and prevent unauthorized modification or deletion.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-07, ST-08

**Architecture Concerns:** CON-01, CON-04, CON-07

**Architecture Viewpoints:** VP-03, VP-04, VP-06

**Acceptance Criteria**

- Posted ledger entries cannot be edited through application interfaces.
- Posted ledger entries cannot be deleted through application interfaces.
- Financial corrections generate separate compensating entries.
- Compensating entries reference the original financial journal.
- Unauthorized modification attempts are recorded.

### FR-LED-004: Fund Reservation Management

**Description**

The system shall support reservation and release of available funds during payment processing.

**Priority:** Must Have

**Stakeholders:** ST-01, ST-03, ST-05

**Architecture Concerns:** CON-04, CON-07

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-05

**Acceptance Criteria**

- Reservations are associated with unique transaction references.
- Active reservations reduce the available balance.
- Reservations do not independently change the posted ledger balance.
- Successful financial posting consumes the associated reservation.
- Definitively failed or cancelled transactions release applicable reservations.
- Reservations for uncertain transactions remain subject to outcome resolution.
- Concurrent reservations cannot exceed available funds.

### FR-LED-005: Balance Calculation

**Description**

The system shall maintain accurate ledger and available balances for supported financial accounts.

**Priority:** Must Have

**Stakeholders:** ST-01, ST-03, ST-06, ST-08

**Architecture Concerns:** CON-03, CON-04, CON-07

**Architecture Viewpoints:** VP-03, VP-04

**Acceptance Criteria**

- Ledger balances reflect committed financial entries.
- Available balances account for active fund reservations.
- Monetary values use appropriate fixed-precision representations.
- Unsupported currency combinations are rejected.
- Concurrent financial operations do not create inconsistent balances.
- Unauthorized overdrafts are prevented.

### FR-LED-006: Ledger Entry Retrieval

**Description**

The system shall allow authorized operations staff to retrieve financial journals and associated ledger entries.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-08

**Architecture Concerns:** CON-01, CON-04, CON-07

**Architecture Viewpoints:** VP-03, VP-04, VP-06

**Acceptance Criteria**

- Ledger entries can be retrieved using a transaction reference.
- Journals can be retrieved using a journal identifier.
- Debit amount, credit amount, currency and posting timestamp are available.
- Original and compensating entries can be traced.
- Unauthorized ledger access is rejected.

### FR-LED-007: Simulated Account Funding

**Description**

The system shall allow authorized operations staff to credit eligible simulated accounts with fictional funds for educational and testing purposes.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-04, ST-08

**Architecture Concerns:** CON-01, CON-04, CON-07

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-06

**Acceptance Criteria**

- Only authorized operations staff can initiate simulated funding.
- Funding amounts must be greater than zero.
- Funding generates balanced financial journal entries against a designated simulation ledger account.
- Duplicate funding requests do not generate duplicate postings.
- Funding actions are recorded in the audit trail.
- No real funds or external financial institutions are involved.

## 11. Transaction Management

### FR-TXN-001: Transaction Record Creation

**Description**

The system shall create identifiable transaction records for supported financial operations.

**Priority:** Must Have

**Stakeholders:** ST-01, ST-02, ST-03

**Architecture Concerns:** CON-04, CON-07

**Architecture Viewpoints:** VP-03, VP-04, VP-05

**Acceptance Criteria**

- Each accepted transaction request generates a unique transaction reference.
- Transaction type, amount, currency and initiation timestamp are recorded.
- Source and destination references are recorded where applicable.
- Transaction records can be associated with financial journals.
- External provider references are recorded where applicable.

### FR-TXN-002: Transaction Lifecycle Management

**Description**

The system shall manage transactions according to explicitly defined lifecycle states and permitted state transitions.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-05, ST-06

**Architecture Concerns:** CON-04, CON-07, CON-10

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-05

**Acceptance Criteria**

- Supported states include Initiated, Validated, Processing, Pending, Completed, Failed and Reversed.
- Permitted state transitions are explicitly defined.
- Invalid state transitions are rejected.
- Completed status requires successful financial posting where applicable.
- Uncertain external outcomes remain Pending until resolved.
- Reversed status requires successful compensating financial processing.
- State changes are recorded with timestamps.

### FR-TXN-003: Transaction Status Inquiry

**Description**

The system shall allow authorized users to retrieve the current status of eligible transactions.

**Priority:** Must Have

**Stakeholders:** ST-01, ST-02, ST-03

**Architecture Concerns:** CON-01, CON-04, CON-09

**Architecture Viewpoints:** VP-03, VP-04, VP-05, VP-06

**Acceptance Criteria**

- Transactions can be retrieved using valid transaction references.
- Current transaction status is returned.
- Customers and merchants can access only their authorized transactions.
- Transaction status reflects the latest recorded processing outcome.

### FR-TXN-004: Transaction State History

**Description**

The system shall maintain a historical record of transaction state transitions.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-05, ST-08

**Architecture Concerns:** CON-04, CON-07

**Architecture Viewpoints:** VP-03, VP-04, VP-06

**Acceptance Criteria**

- Each state transition records the previous and new states.
- State transition timestamps are recorded.
- The initiating actor or system component is identifiable.
- Transition reasons are recorded where applicable.
- Historical state records are preserved.

### FR-TXN-005: Transaction Search and Filtering

**Description**

The system shall allow authorized operations staff to search and filter transaction records.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-08

**Architecture Concerns:** CON-01, CON-03, CON-07

**Architecture Viewpoints:** VP-03, VP-04, VP-06

**Acceptance Criteria**

- Transactions can be searched using transaction references.
- Transactions can be filtered by date, type, status and amount.
- External provider references can be used for transaction searches.
- Search results support pagination.
- Access is restricted to authorized users.

### FR-TXN-006: Transaction Error Management

**Description**

The system shall record and communicate transaction processing errors.

**Priority:** Must Have

**Stakeholders:** ST-01, ST-03, ST-05, ST-09

**Architecture Concerns:** CON-01, CON-04, CON-07, CON-08

**Architecture Viewpoints:** VP-03, VP-04, VP-05, VP-06

**Acceptance Criteria**

- Processing failures are associated with standardized error codes.
- Validation failures are distinguishable from technical failures.
- Uncertain payment outcomes are distinguishable from definitive failures.
- User-facing messages do not expose sensitive technical information.
- Diagnostic information is available to authorized operations staff.
- Errors can be correlated with transaction references.

### FR-TXN-007: Transaction Recovery

**Description**

The system shall support recovery and resolution of interrupted or incomplete transaction processing.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-05, ST-09

**Architecture Concerns:** CON-02, CON-04, CON-07, CON-10

**Architecture Viewpoints:** VP-03, VP-04, VP-05, VP-07

**Acceptance Criteria**

- Incomplete transactions can be identified after service interruption.
- Recovery processing preserves existing transaction references.
- Recovery operations do not generate duplicate financial postings.
- External transaction outcomes are verified before uncertain transactions are resolved.
- Unresolved exceptions are available for operational investigation.
- Recovery actions are recorded for audit purposes.



## 12. Notification Management

### FR-NOT-001: Transaction Notification Generation

**Description**

The system shall generate notifications for supported transaction lifecycle events.

**Priority:** Must Have

**Stakeholders:** ST-01, ST-02, ST-04

**Architecture Concerns:** CON-04, CON-09

**Architecture Viewpoints:** VP-02, VP-03, VP-05

**Acceptance Criteria**

- Notifications are generated for configured transaction events.
- Supported events include completed, failed and reversed transactions.
- Notification content reflects the recorded transaction outcome.
- Notifications contain the relevant transaction reference.
- Sensitive authentication information is excluded.
- Duplicate events do not generate unintended duplicate notifications.

### FR-NOT-002: Notification Delivery

**Description**

The system shall deliver notifications through a simulated notification provider.

**Priority:** Must Have

**Stakeholders:** ST-01, ST-02, ST-09

**Architecture Concerns:** CON-02, CON-05, CON-09

**Architecture Viewpoints:** VP-03, VP-05, VP-07

**Acceptance Criteria**

- Notification requests are submitted to the simulated provider.
- Each notification has a unique notification identifier.
- Notification delivery outcomes are recorded.
- Notification processing is independent of financial transaction completion.
- Notification delivery failures do not reverse completed financial transactions.
- No real SMS or email delivery is required.

### FR-NOT-003: Notification Template Management

**Description**

The system shall support configurable notification templates for supported business events.

**Priority:** Should Have

**Stakeholders:** ST-03, ST-04

**Architecture Concerns:** CON-08, CON-09

**Architecture Viewpoints:** VP-02, VP-03, VP-04

**Acceptance Criteria**

- Templates can be associated with supported notification events.
- Templates support predefined dynamic fields.
- Transaction references, amounts and currencies can be populated dynamically.
- Only authorized users can modify templates.
- Template changes are recorded for audit purposes.

### FR-NOT-004: Notification Retry Management

**Description**

The system shall support controlled retry processing for failed notification delivery attempts.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-05, ST-09

**Architecture Concerns:** CON-02, CON-04, CON-10

**Architecture Viewpoints:** VP-03, VP-04, VP-05, VP-07

**Acceptance Criteria**

- Failed notification attempts are identifiable.
- Retry intervals and maximum retry attempts are configurable.
- Retry processing preserves the original notification identifier.
- Duplicate delivery is prevented where supported by the provider.
- Notifications exceeding retry limits are available for investigation.
- Notification retries do not generate financial postings.

### FR-NOT-005: Notification History

**Description**

The system shall maintain notification records and delivery attempt history.

**Priority:** Should Have

**Stakeholders:** ST-03, ST-08, ST-09

**Architecture Concerns:** CON-01, CON-07, CON-08

**Architecture Viewpoints:** VP-03, VP-04, VP-06

**Acceptance Criteria**

- Notification records contain the associated business event reference.
- Notification creation and delivery timestamps are recorded.
- Delivery statuses and retry attempts are available.
- Authorized operations staff can retrieve notification history.
- Sensitive notification data is protected.

## 13. Banking Operations

### FR-OPS-001: Operations Dashboard

**Description**

The system shall provide authorized banking operations staff with a dashboard for monitoring platform activities.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-04, ST-09

**Architecture Concerns:** CON-03, CON-07, CON-09

**Architecture Viewpoints:** VP-02, VP-03, VP-04

**Acceptance Criteria**

- Transaction volumes are displayed.
- Transactions can be categorized by type and status.
- Completed, failed and pending transaction counts are available.
- Unresolved operational exceptions are identifiable.
- Dashboard information is derived from recorded system data.
- Dashboard access is restricted to authorized users.

### FR-OPS-002: Maker-Checker Authorization

**Description**

The system shall support dual authorization for designated sensitive operational activities.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-07, ST-08

**Architecture Concerns:** CON-01, CON-04, CON-07

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-06

**Acceptance Criteria**

- Sensitive operational requests can be submitted by authorized makers.
- Submitted requests remain pending until reviewed.
- Authorized checkers can approve or reject requests.
- Makers cannot approve their own requests.
- Approval does not bypass applicable business validation.
- Approved requests cannot be executed more than once.
- Maker and checker identities and decisions are recorded.

### FR-OPS-003: Operational Request Management

**Description**

The system shall maintain identifiable records of operational requests requiring review or execution.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-07, ST-08

**Architecture Concerns:** CON-01, CON-04, CON-07

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-06

**Acceptance Criteria**

- Each operational request has a unique request identifier.
- Request type, initiating user and creation timestamp are recorded.
- Approval and execution statuses are distinguishable.
- Supported request types include account status changes, simulated funding and transaction reversals.
- Rejection reasons and execution outcomes are recorded.
- Unauthorized request modifications are rejected.

### FR-OPS-004: Transaction Exception Management

**Description**

The system shall allow authorized operations staff to investigate and manage transaction exceptions.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-08, ST-09

**Architecture Concerns:** CON-04, CON-07, CON-10

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-05

**Acceptance Criteria**

- Pending and interrupted transactions are identifiable.
- Exception records reference their originating transactions.
- Operations staff can record investigation notes.
- Exceptions can be assigned to authorized operations users.
- External payment outcomes can be investigated.
- Exception resolution follows applicable financial controls.
- Operations staff cannot directly overwrite posted ledger entries.

### FR-OPS-005: Business Configuration Management

**Description**

The system shall allow authorized operations staff to maintain supported business configuration parameters.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-04, ST-07

**Architecture Concerns:** CON-01, CON-04, CON-07, CON-08

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-06

**Acceptance Criteria**

- Supported configuration parameters include transaction limits and notification retry policies.
- Configuration values are validated before activation.
- Sensitive configuration changes require applicable approval.
- Configuration changes record previous and new values.
- Configuration changes record the responsible user and timestamp.
- Configuration changes do not expose application secrets.

### FR-OPS-006: Operational User Management

**Description**

The system shall allow authorized administrators to manage banking operations user accounts and assigned permissions.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-07, ST-08

**Architecture Concerns:** CON-01, CON-07

**Architecture Viewpoints:** VP-03, VP-04, VP-06

**Acceptance Criteria**

- Authorized administrators can create operational user accounts.
- Operational users can be assigned permitted roles.
- Maker and checker permissions can be configured.
- Operational user accounts can be disabled.
- Unauthorized privilege escalation is prevented.
- User and permission changes are recorded for audit purposes.

### FR-OPS-007: Operational Activity History

**Description**

The system shall maintain a history of sensitive activities performed by banking operations users.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-07, ST-08

**Architecture Concerns:** CON-01, CON-07

**Architecture Viewpoints:** VP-03, VP-04, VP-06

**Acceptance Criteria**

- Sensitive operational activities are recorded.
- Activity records identify the responsible user.
- Activity records include action type and timestamp.
- Associated business entities and transaction references are identifiable.
- Authorized users can retrieve operational activity history.
- Unauthorized modification and deletion of activity records are prevented.



## 14. Reconciliation

### FR-REC-001: External Transaction Record Import

**Description**

The system shall support the import of transaction records generated by the simulated external payment provider.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-05, ST-10

**Architecture Concerns:** CON-04, CON-05, CON-07

**Architecture Viewpoints:** VP-03, VP-04, VP-05

**Acceptance Criteria**

- External transaction records can be imported using a supported format.
- Mandatory record fields are validated.
- Provider transaction references, amounts, currencies and statuses are captured.
- Invalid records are identified and reported.
- Duplicate record imports do not create duplicate reconciliation records.
- Import outcomes are recorded for audit purposes.

### FR-REC-002: Transaction Matching

**Description**

The system shall compare internal transaction records with corresponding external payment provider records.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-08, ST-10

**Architecture Concerns:** CON-04, CON-05, CON-07

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-05

**Acceptance Criteria**

- Records are matched using supported transaction references.
- Transaction amounts, currencies and normalized statuses are compared.
- Successfully matched transactions are identifiable.
- Amount and status discrepancies are identified.
- Missing internal and external records are identified.
- Matching outcomes are recorded.

### FR-REC-003: Internal Ledger Reconciliation

**Description**

The system shall reconcile internal transaction records against their associated financial journals and ledger entries.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-06, ST-08

**Architecture Concerns:** CON-04, CON-07

**Architecture Viewpoints:** VP-03, VP-04

**Acceptance Criteria**

- Completed financial transactions are checked against expected financial postings.
- Missing or unexpected financial journals are identified.
- Debit and credit totals are validated for each currency.
- Duplicate financial postings are identified.
- Financial posting discrepancies are reported.
- Reconciliation processing does not directly modify posted ledger entries.

### FR-REC-004: Reconciliation Batch Processing

**Description**

The system shall support batch-based reconciliation processing for defined reporting periods.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-08, ST-09

**Architecture Concerns:** CON-03, CON-04, CON-07, CON-10

**Architecture Viewpoints:** VP-03, VP-04, VP-07

**Acceptance Criteria**

- Each reconciliation batch has a unique batch identifier.
- Reconciliation periods and data sources are recorded.
- Batch execution status is maintained.
- Matched and unmatched transaction counts are available.
- Reprocessing does not create unintended duplicate results.
- Failed batches can be identified and investigated.

### FR-REC-005: Reconciliation Exception Management

**Description**

The system shall allow authorized operations staff to investigate and resolve reconciliation discrepancies.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-07, ST-08

**Architecture Concerns:** CON-01, CON-04, CON-07

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-06

**Acceptance Criteria**

- Unmatched transactions generate identifiable reconciliation exceptions.
- Exceptions are categorized according to discrepancy type.
- Investigation notes and supporting references can be recorded.
- Exceptions can be assigned to authorized operations users.
- Financial corrections follow applicable approval controls.
- Original financial records remain preserved.
- Resolution actions and outcomes are recorded.

### FR-REC-006: Simulated Settlement Management

**Description**

The system shall calculate and maintain simulated settlement obligations associated with eligible external financial transactions.

**Priority:** Should Have

**Stakeholders:** ST-03, ST-08, ST-10

**Architecture Concerns:** CON-04, CON-05, CON-07

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-05

**Acceptance Criteria**

- Eligible transactions are associated with a settlement period.
- Settlement obligations are calculated separately for each currency.
- Applicable debit and credit obligations are identifiable.
- Each settlement record has a unique reference.
- Settlement status and associated transaction references are maintained.
- Reconciliation and settlement statuses are distinguishable.
- No real interbank settlement is performed.

## 15. Reporting and Audit

### FR-RPT-001: Transaction Reporting

**Description**

The system shall generate transaction reports for authorized banking operations users.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-04, ST-08

**Architecture Concerns:** CON-01, CON-03, CON-07

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-06

**Acceptance Criteria**

- Reports can be generated for selected date ranges.
- Transactions can be categorized by type, currency and status.
- Transaction counts and monetary totals are available.
- Monetary totals are calculated separately for each currency.
- Reported values are consistent with underlying transaction records.
- Report access is restricted to authorized users.

### FR-RPT-002: Financial Ledger Reporting

**Description**

The system shall generate reports based on recorded financial journals and ledger entries.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-06, ST-08

**Architecture Concerns:** CON-04, CON-07

**Architecture Viewpoints:** VP-02, VP-03, VP-04

**Acceptance Criteria**

- Debit and credit totals are available for selected reporting periods.
- Ledger account balances are reportable.
- Financial journals can be traced to originating transactions.
- Compensating financial entries are identifiable.
- Trial balance reports can be generated.
- Reports identify inconsistencies between debit and credit totals.

### FR-RPT-003: Reconciliation Reporting

**Description**

The system shall generate reports summarizing reconciliation processing outcomes.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-08, ST-09

**Architecture Concerns:** CON-04, CON-07, CON-09

**Architecture Viewpoints:** VP-02, VP-03, VP-04

**Acceptance Criteria**

- Reconciliation reports reference the associated batch identifier.
- Matched and unmatched transaction counts are available.
- Discrepancies are categorized by type.
- Monetary differences are reported separately for each currency.
- Open and resolved exception counts are available.
- Reconciliation results can be traced to underlying records.

### FR-RPT-004: Merchant Reporting

**Description**

The system shall allow authorized merchants to retrieve reports of their associated payment transactions.

**Priority:** Should Have

**Stakeholders:** ST-02, ST-03

**Architecture Concerns:** CON-01, CON-04, CON-09

**Architecture Viewpoints:** VP-02, VP-03, VP-04, VP-06

**Acceptance Criteria**

- Merchants can retrieve reports for selected date ranges.
- Payment counts and monetary totals are available.
- Refund transactions are identifiable.
- Payment and refund totals are reported separately.
- Merchants cannot access another merchant's financial reports.

### FR-RPT-005: Audit Trail Management

**Description**

The system shall maintain audit records for designated business, financial, administrative and security activities.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-07, ST-08

**Architecture Concerns:** CON-01, CON-04, CON-07

**Architecture Viewpoints:** VP-03, VP-04, VP-06

**Acceptance Criteria**

- Audit records contain a unique audit identifier.
- The responsible user or system component is identifiable.
- Action type, timestamp and affected entity are recorded.
- Previous and new values are recorded where applicable.
- Sensitive credentials and secrets are excluded from audit records.
- Audit records cannot be modified or deleted through ordinary application interfaces.
- Audit records can be correlated with relevant transaction and operational references.

### FR-RPT-006: Audit Record Retrieval

**Description**

The system shall allow authorized users to search and retrieve audit records.

**Priority:** Must Have

**Stakeholders:** ST-03, ST-07, ST-08

**Architecture Concerns:** CON-01, CON-03, CON-07

**Architecture Viewpoints:** VP-03, VP-04, VP-06

**Acceptance Criteria**

- Audit records can be filtered by date range, actor and action type.
- Records can be retrieved using relevant entity or transaction references.
- Search results support pagination.
- Access is restricted to authorized users.
- Audit record retrieval does not modify the original records.

### FR-RPT-007: Report Export

**Description**

The system shall allow authorized users to export supported reports in a structured file format.

**Priority:** Should Have

**Stakeholders:** ST-02, ST-03, ST-04, ST-08

**Architecture Concerns:** CON-01, CON-05, CON-09

**Architecture Viewpoints:** VP-03, VP-04, VP-05, VP-06

**Acceptance Criteria**

- Supported reports can be exported in CSV format.
- Exported records reflect the selected report filters.
- Exported records preserve applicable monetary precision.
- Unauthorized or sensitive information is excluded.
- Report export activities are recorded for audit purposes.

## 16. Requirements Traceability

Each functional requirement is assigned a unique identifier and associated with relevant stakeholders, architecture concerns and architecture viewpoints.

Functional requirements shall be traceable to applicable:

- Business capabilities
- Architecture views
- Application components
- Data entities
- API specifications
- Architecture decision records
- Security controls
- Test cases

Detailed implementation traceability shall be established during subsequent architecture design and development activities.

## 17. Assumptions and Constraints

- NEXUS is an independent educational reference platform.
- All financial transactions and customer records are simulated.
- External payment and notification providers are simulated.
- No real financial settlement or movement of funds is performed.
- No proprietary banking infrastructure or confidential employer information is used.
- Regulatory compliance certification is outside the current project scope.
- Functional requirements are subject to refinement during architecture design.
- Requirements shall be prioritized further when defining the minimum viable product.

## 18. Document Status

Initial functional requirements baseline drafted.

The requirements remain subject to review, validation, prioritization and refinement during subsequent architecture activities.
