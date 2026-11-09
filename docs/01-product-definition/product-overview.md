# Product overview

LendCore maintains customer and credit files; configures versioned products; receives applications; obtains consented data; calculates capacity, exposure, and scenarios; records recommendations and decisions; prepares terms and formalization; orders disbursements; administers balances and due dates; receives payment instructions; allocates funds under policy/contract; manages delinquency, prepayment, and changes; records each financial effect in the operational ledger; and provides auditable reports.

## Boundaries and interactions

The operational ledger is LendCore's record of credit movements, not the bank's general ledger. An external system may own account balances, monetary execution, FX rates, or identity data. Each external message retains its identifier, correlation ID, date, amount, currency, status, and evidence. LendCore does not treat a disbursement as effective merely because an order was sent.

## Module boundaries

| Module | Responsibility | Does not decide |
|---|---|---|
| Customer/documents | Identity, related parties, file, consent, and validity | Final prudential classification without required data/configuration |
| Product/origination | Offer, application, frozen parameters | Final automated approval |
| Risk/decision | Indicators, signals, recommendation, file, and approvals | Override policy or delegated authority |
| Contract/loan | Accepted terms, schedule, balance, events | Execute an external transfer |
| Payments/ledger | Instruction, idempotency, allocation, and compensation | Assert unconfirmed external settlement |
| Collateral/collections | Evidence/perfection and case management | Autonomously take legal action |
| Reporting/audit | Reproducible views and evidence | Change source data |

## Information ownership and hand-offs

The customer/file function owns the reviewed identity, party authority, consent evidence, and document status held by LendCore; an authoritative identity provider may own the source identity result. Origination owns the requested purpose and terms and the exact product version used. Risk/decision owns the assessment snapshot, model/policy version, recommendation, delegated authority, conditions, and decision rationale. Contract/loan administration owns the accepted contractual snapshot, schedule versions, and current contractual servicing state derived from confirmed events. Payment operations owns receipt references, idempotency, allocation intent/result, and reconciliation status. The core/account provider owns whether an account transfer settled; the general ledger owns accounting entries. LendCore stores external references and evidence so that a discrepancy can be explained without claiming ownership of an external fact.

Every hand-off should state source and destination, customer/loan reference, currency and amount where relevant, effective/value date, request/result status, correlation identifier, and evidence/source version. An unavailable provider leaves the operation in a named pending/error state. Manual continuation is possible only under approved policy and records who authorized the exception and what equivalent evidence was used. A late or repeated message is compared with the existing identifier and payload before any financial effect is applied.

## Explicit non-responsibilities

LendCore does not establish the bank's risk appetite, approve a real credit policy, calculate official prudential classification merely from a commercial score, originate external settlement by itself, determine whether a signature is legally sufficient, perfect or enforce collateral, decide legal complaint outcomes, or file official regulatory returns in the MVP. It can record evidence, controls, and workflow outcomes that support those institutional processes. See [scope and exclusions](scope.md) and [regulatory interpretation limits](../07-compliance/regulatory-framework.md).
