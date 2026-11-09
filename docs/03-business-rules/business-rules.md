# Master business rules catalog

Each rule is a verifiable product decision. Normative sources are identified where a legal obligation is stated; the remaining rules are proposed under DP-002/DP-003 and subject to bank policy. Each group references related RF and AC.

## How to apply the catalog

An RN describes a business outcome, not an implementation design. Product configuration may specialize a rule only where the rule allows it and the configuration has an owner, version, effective date, and evidence. Where the catalog says “subject to Legal,” no default configuration should be treated as an approved legal interpretation. The functional requirement owns the user-visible trigger and outcome; the process catalog describes sequence and recovery; the financial model supplies calculation detail. These references form one traceable decision and should be changed together when meaning changes.

The important distinction is between **evidence**, **decision**, and **execution**. A bureau response or valuation is evidence, not an approval. An approval authorizes an action but is not proof that funds moved. A payment receipt is not yet a loan allocation. A collection promise is not a schedule amendment. A write-off is not debt forgiveness. The system must retain these as separate facts and state transitions.


## Customer, product, and origination

- **RN-001 Unique identity:** block automatic creation when type and document number match; a fuzzy match creates an alert and review, not a merge. Exception: documented correction with history. RF-001; CA-001.
- **RN-002 Parties and representation:** a legal entity requires a tax identifier, representatives, and current authority evidence; an application/signature beyond that authority is blocked. RF-001.
- **RN-003 Customer status:** observed, inactive, deceased, or blocked status prevents new origination according to the reason; existing debt is not deleted. RF-001.
- **RN-004 Consent and purpose:** source inquiries require an applicable legal basis/consent, purpose, date, text, and origin; revocation stops future use where applicable without destroying contractual evidence that must be retained. RF-001, RF-021.
- **RN-005 Documents:** each document type has product/segment-specific requirements, validity, owner, and validation rule; missing, expired, or inconsistent evidence blocks advancement to a state requiring it. RF-002.
- **RN-006 Versioned product:** a product cannot be published without currency, method, rate, day-count, frequency, calendar, charges, or limits; the version effective at contracting is frozen. RF-003.
- **RN-007 Product eligibility:** age, segment, purpose, currency, term, amount, and collateral are product criteria; failure results in ineligibility or an escalated exception, never concealment. RF-003..004.
- **RN-008 Disclosable terms:** quote the rate and its type, periodicity, basis, applicable charges/insurance, calendar, total amount, and disclosed cost for the relevant category. Do not present TCEA as the contractual interest rate. RF-003, RF-007.
- **RN-009 Currencies:** product/loan retains its contractual currency. Conversion requires source amount/currency, destination currency, FX rate and source, timestamp/value date, user/purpose, and resulting amount. RF-003, RF-010.
- **RN-010 Calendars:** monthly frequency preserves the anchor day with a contractual adjustment rule; weekly adds 7 days; 15-day frequency adds exactly 15 calendar days; “twice monthly” is allowed only when explicitly defined by the product. RF-003, RF-009.
- **RN-011 Complete application:** assessment starts only with identity/authority, consent, purpose, amount, currency, term, income/cash flow, declared obligations, and required evidence or an authorized exception. RF-004.
- **RN-012 Duplicate application:** same customer/product/purpose within a configurable window is linked or held for review; it must not duplicate reported debt/exposure. RF-004.
- **RN-013 File integrity:** a change after assessment invalidates affected indicators and requires recalculation; preserve prior values and who changed them. RF-004..005.
- **RN-014 Capacity currency:** calculate income, installments, and debt by currency; convert exposure using approved FX and a policy-consistent date, and show FX sensitivity when income and debt currencies differ. RF-005.


## Risk and authorization

- **RN-015 Repayment capacity:** calculate net income less essential expenses, verifiable current obligations, and proposed installment; methodology, sources, haircuts, and thresholds are configurable by segment/product and explainable. There is no universal threshold. RF-005.
- **RN-016 Verifiable income:** distinguish declared, observed, and verified income; if inconsistent, use the lower supported value or stop assessment under policy; never silently impute zero income. RF-005.
- **RN-017 Exposure:** consolidate known direct/indirect debt and commitments by customer/group under policy; avoid double counting a source reference. RF-005.
- **RN-018 Sensitivity:** stress higher variable rates, FX, lower income/sales, and delayed receipts where relevant; stress conditions and acceptance are versioned. RF-005.
- **RN-019 Versioned scoring:** save model/policy version, inputs, date, result, bands, and principal reasons; a score is not an approval. RF-005.
- **RN-020 Missing data/source outage:** set incomplete/pending state; human reassessment is allowed only with equivalent evidence and authority; outage cannot become a favorable result. RF-005.
- **RN-021 Capacity primacy:** credit decision is primarily based on repayment capacity; collateral mitigates loss and does not replace capacity under General Law 26702, art. 222, and applicable SBS rules. RF-005..006.
- **RN-022 Risk classification:** prudential/regulatory category and provisions follow SBS rules by debtor type; LendCore may support/store data but must not assume commercial score equals regulatory classification. RF-005.
- **RN-023 Human review:** authorized staff review recommendation, exceptions, documents, and contradictions before a decision required by policy; override requires rationale and escalation. RF-006.
- **RN-024 Delegation:** amount, risk, product, currency, exception, and exposure determine authority under a versioned matrix; an out-of-limit request escalates and cannot be artificially split. RF-006, RF-019.
- **RN-025 Segregation and conflicts:** applicant/analyst/preparer cannot be the sole approver and executor of the resulting disbursement, reversal, or adjustment. A person with a conflict does not participate in the decision. Related-party financing follows the applicable governance and approval authority; SBS Resolution 02235-2026 amended Credit Risk Regulation article 21(e), with a distinct CMAC rule. RF-006, RF-008, RF-017; C-02.
- **RN-026 Rejection/conditions:** decision stores coded and written reason, authority, policy, validity, and conditions; do not disclose third-party or confidential data. RF-006.
- **RN-027 Reopening:** material data change, expired approval, or unmet conditions return the case to assessment/authority; approval is not indefinite. RF-006.


## Contract, disbursement, and loan administration

- **RN-028 Contract freeze:** accepted terms, rates, basis, calendar, method, charges, and product version form an immutable snapshot. RF-007.
- **RN-029 Acceptance:** amount, beneficiary, or material terms different from approval invalidate formalization and require updated approval/acceptance. RF-007.
- **RN-030 Conditions precedent:** disbursement requires effective contract, required collateral/insurance/documents, and validated account; authorized exceptions retain evidence. RF-007..008.
- **RN-031 Deliverables:** record version and evidence of delivery of contract, summary sheet, and schedule to customer, including channel/date. RF-007.
- **RN-032 Unique order:** idempotency key is unique by loan+tranche; amount/currency must match approval and authorized beneficiary. RF-008.
- **RN-033 External confirmation:** sent/timeout remains pending/unknown; only confirmation or authorized reconciliation makes disbursement effective. RF-008.
- **RN-034 Partial disbursement:** supported only for a tranche-based product; each tranche has a value date and accrues under contract. MVP limits to one disbursement. RF-008.
- **RN-035 Rejection/retry:** query prior operation status before retry; ambiguous result cannot create another order. RF-008.
- **RN-036 Dated parameters:** applied rate depends on validity and accrual date; a change is never retroactive for accrued interest. RF-009, RF-012.
- **RN-037 Accrual:** ordinary interest is calculated on outstanding principal under contractual basis, interval, and rate; charges are not added to principal unless a specific legal/contractual basis has been reviewed. RF-009.
- **RN-038 Schedule:** installments separate principal, compensatory interest, default interest, charges, and insurance; scheduled principal reconciles to funded principal under contract. RF-009.
- **RN-039 French method:** level installment before rounding for uniform rate/periods; irregular actual periods use period factors and a consistent resolution, not an unjustified annual-rate-divided-by-installment-count shortcut. RF-009.
- **RN-040 German method:** constant principal amortization (except final adjustment); interest varies with balance and days. RF-009.
- **RN-041 Principal grace:** during N periods, principal amortization is zero and current interest is paid under the calendar; unpaid interest does not automatically increase principal. Unpaid interest is recorded as due, not capitalized. RF-009.
- **RN-042 Schedule changes:** new schedule is versioned with reason; satisfied installments and closed accruals are not recalculated retroactively. RF-009, RF-015.
- **RN-043 Non-business day:** calendar and rule (preceding/following/modified following) are fixed in contract/product; date adjustment affects actual accrual. A product cannot be published without a rule. RF-009.
- **RN-044 Final period:** final installment adjusts cents and balance without negative principal or unexplained amounts. RF-009.


## Payments, prepayment, and integrity

- **RN-045 Payment validation:** amount must be positive, currency compatible with contract, loan open, source reference present, and value date valid; failure creates no applied movement. RF-010.
- **RN-046 Idempotency:** external source+identifier is unique; identical replay returns existing outcome; same ID with different payload is blocked and investigated. RF-010.
- **RN-047 Atomic application:** movement, allocations, balance, and installment status commit as one logical unit or remain pending; no partial application without an explicit state. RF-010.
- **RN-048 Allocation order:** allocate overdue enforceable items and legally due default interest, then compensatory interest, principal, and charges only as permitted by contract/law and configured policy. Exact order is disclosed and versioned. For consumers, do not invent a priority that conflicts with rights; legal review is required by product. RF-010.
- **RN-049 Insufficient amount:** allocate by the applicable priority and leave the installment partially satisfied; do not mark paid until no due amount remains, except a documented rounding tolerance. RF-010.
- **RN-050 Excess amount:** do not appropriate silently; identify instruction among prepayment, future installments, or unapplied balance and obtain confirmation where required. RF-010..011.
- **RN-051 Unidentified payment:** hold in an operational suspense account (not the loan balance) until matched; daily reconciliation is a target. RF-010, RF-017.
- **RN-052 Value date:** retain receipt, settlement, and value dates; adjust interest only under contractual terms and confirmed evidence. RF-010.
- **RN-053 Concurrency:** simultaneous payments recalculate against a serialized balance; no excess allocation or duplicate assignment. Handle excess separately. RF-010.
- **RN-054 Transaction failure:** failure before external confirmation is not applied; failure after external confirmation creates a recoverable discrepancy and does not retry execution without a status query. RF-010, RF-017.
- **RN-055 Right to prepay:** allow total/partial prepayment and reduce compensatory interest accrued through payment date; no penalty or equivalent charge under Consumer Code Law 29571, art. 86, subject to applicability by customer/product. RF-011; source C-03.
- **RN-056 Quote:** as of a specified date/time calculate outstanding principal, compensatory interest accrued through value date, due obligations, and permitted/contractual costs; expire and recalculate after date/event change. RF-011.
- **RN-057 Partial prepayment:** after prior obligations/accrual under disclosed policy, apply net amount to principal; generate a new table under the contractual option: same term with recalculated installment or reduced term with recalculated installment. RF-011.
- **RN-058 Full prepayment:** exact settlement comprises principal + interest through effective date + permitted due obligations; future accrual stops from effective cancellation date, subject to reconciliation. RF-011.
- **RN-059 Installment advance:** payment for future installments remains an advance if not applied to principal; it does not create an equivalent reduction in principal/future interest. Distinguish and explain the option under applicable SBS/consumer rules. RF-010..011.
- **RN-060 Pending prepayment:** instruction is not applied until funds are confirmed; a quote is not settlement. RF-011.
- **RN-061 New schedule:** retain original snapshot, movements, and prepayment allocation; do not duplicate or remove paid installments. RF-011.
- **RN-062 Closure:** contractual balance is zero and reconciliation has no discrepancy; issue a certificate and initiate separate collateral-release workflow. RF-011.


## Rates, collateral, delinquency, and credit changes

### Financial operation distinctions

The following terms are deliberately not interchangeable. Their separation affects customer rights, balance reconstruction, reporting, and acceptance testing.

| Operation | What changes | What does not happen automatically | Related rules |
|---|---|---|---|
| Scheduled installment payment | Settles some or all amounts already due | Does not reduce future principal beyond the principal component allocated to this installment | RN-045..054 |
| Principal prepayment | Reduces outstanding principal before scheduled maturity and therefore future compensatory-interest base | Does not mean that future installments are paid; does not close the loan unless full settlement is confirmed | RN-055..062 |
| Installment advance | Reserves/applies funds to a future scheduled obligation according to the contract | Is not an equivalent immediate principal reduction; do not show the same savings as a prepayment | RN-050, RN-059 |
| Rescheduling | Replaces the future due-date/amount plan for an existing obligation after approval and acceptance | Does not necessarily replace the debt or erase delinquency/history | RN-077, RN-079..081 |
| Refinancing | Creates a new credit transaction whose proceeds or agreed accounting settle/replace an old obligation | Does not take effect merely because new terms were simulated or approved | RN-078..081 |
| Reversal | Adds a linked compensating event to correct a confirmed movement | Does not delete the original movement or imply a second external transfer | RN-083..087 |
| Write-off | Records an approved accounting/prudential treatment | Does not automatically forgive the legal claim or end permitted recovery activity | RN-082 |

### Failure handling contract

| Failure or exception | Required business outcome | Evidence retained / recovery path |
|---|---|---|
| Mandatory application evidence missing | Keep draft/incomplete; do not assess as complete | Missing item, owner, reason, and resubmission history |
| Customer changes a material term after assessment | Mark affected assessment stale and return for reassessment | Before/after data, actor, impacted indicators, prior assessment version |
| Approval rejected or expired | No formalization/disbursement; preserve reasons and decision | New application or authorized reassessment creates a linked version |
| External source unavailable | Explicit pending/error; no favorable default | Provider, request/correlation, timestamp, retry/manual alternative authority |
| Disbursement timeout | Unknown pending status; query/reconcile before retry | Unique order ID and all external responses; no duplicate execution |
| Duplicate payment message | Identical replay returns original result; altered replay is disputed | Source ID and payload fingerprint; one effective allocation at most |
| Payment confirmed externally but local application failed | Create investigable discrepancy; recover from confirmation | Keep funds in settlement/suspense state pending safe recovery; no blind payment retry |
| Confirmed movement is wrong | Apply authorized linked compensation after external-state check | Original, reversal reason/approvals, corrected derived balance, reconciliation |
| Delinquency is under payment dispute | Keep obligation and dispute visible; pause adverse action only as approved policy/law requires | Complaint link, receipt evidence, investigation and outcome |
| Early payment is received after quote expiry | Recalculate using actual confirmed value date and current obligations | Prior quote, new calculation, customer instruction and confirmation |
| Process is interrupted | Resume from last durable business state; do not repeat external monetary effect | Correlation key, state, pending work, reconciliation checkpoint |

These outcomes are design requirements. Legal, accounting, and operational policies determine exact suspense treatment, collection pauses, and value-date corrections.

- **RN-063 Variable rate:** contract identifies observable index, source, margin, review frequency/date, applicable limits, notice, and discontinuation rule; new rate applies only from its effective date and never changes prior accrual. RF-012.
- **RN-064 Collateral record:** identify asset/right, owner, value/currency/date/source, rank/priority, encumbrances, link, and document. RF-013.
- **RN-065 Valuation:** real collateral has value, date, method, appraiser, and validity defined by policy; where SBS rules require, use an appraiser meeting applicable registry requirements. RF-013.
- **RN-066 Perfection:** collateral not legally evidenced as perfected is marked pending and does not count as effective collateral. RF-013.
- **RN-067 Revaluation:** alert on expiry, deterioration, insufficient coverage, ownership/encumbrance change; do not replace a valuation without evidence. RF-013.
- **RN-068 Personal guarantees:** record guarantor, covered obligation, amount/scope, assessed capacity, and consent; do not assume unlimited coverage. RF-013.
- **RN-069 Release:** only after extinction of covered obligation or approved partial release with authority and legal review; record process and certificate. RF-013.
- **RN-070 Enforcement:** record decision, notices, file, and recovery; enforcement does not occur automatically because a loan is delinquent. RF-013.
- **RN-071 Delinquency:** installment becomes overdue after contractual due date if unpaid; operational grace does not change due date or obligation without agreement/law. RF-014.
- **RN-072 Default interest:** simple interest on permitted overdue base and elapsed days, at contractual rate and within limits; do not capitalize interest or charge default interest on default interest in the initial design. Do not configure a late-payment penalty or equivalent charge prohibited under Law 31143. Legal review determines permitted default interest and applicable cap. RF-014.
- **RN-073 Default-interest base:** separate overdue principal and overdue charges/interest; which items bear default interest requires contractual and legal validation and product configuration. RF-014.
- **RN-074 Dispute/pending payment:** pause automated adverse actions when payment evidence is under reconciliation, as appropriate; retain delinquency history. RF-014.
- **RN-075 Contact:** record channel, date, outcome, consent/preferences, and owner; content and hours must follow consumer protection and current rules. RF-014.
- **RN-076 Promise to pay:** a promise does not change due date, interest, or classification; confirmed payment updates collection status. RF-014.
- **RN-077 Rescheduling:** changes dates/installments by approved modification; calculates interest through effective date and preserves debt/history. RF-015.
- **RN-078 Refinancing:** new operation extinguishes/refinances old debt only when conditions and effective disbursement/compensation occur; distinguish prudential SBS treatment from commercial status. RF-015.
- **RN-079 Capitalized interest in restructuring:** do not capitalize unless specifically legally/contractually permitted, transparently disclosed, and approved; not automatic in MVP. RF-015.
- **RN-080 New assessment:** analyze current capacity, delinquency, collateral, source of funds, and authority; independent review for exceptions. RF-015.
- **RN-081 History:** preserve old schedule and cut-off balances; link new version to reason, approvals, and acceptance. RF-015.
- **RN-082 Write-off:** approved portfolio/accounting event under applicable policy; does not extinguish claim, evidence, or movements. RF-016.


## Reversal, audit, and currency

- **RN-083 No deletion:** a confirmed movement is never physically modified or deleted. RF-017.
- **RN-084 Compensation:** reversal references original, reason, amount/currency, date, and approver; total reversed cannot exceed original. RF-017.
- **RN-085 Payment reversal:** reopens principal/installments and recalculates derived balances from effective event; does not overwrite schedule. RF-017.
- **RN-086 Uncertain disbursement:** reconcile with source system before compensation/reissue; late response links to original order. RF-017.
- **RN-087 Reconstruction:** balance equals ordered sum of effective movements by conceptual account, currency, and value date; snapshots are verifiable accelerators, not sole authority. RF-017.
- **RN-088 Audit:** decision/financial change retains actor, time, old/new data, rationale, authorization, and correlation. RF-018.
- **RN-089 Reproducible reports:** execution stores parameters, cut-off, time zone, source version, and filters. RF-018.
- **RN-090 Auditor access:** segregated read access; sensitive export is justified and logged. RF-018.
- **RN-091 Complaint:** link response and evidence to original record; resolution does not silently alter movements. RF-018, RF-021.
- **RN-092 Least privilege:** grant only the permissions needed by product, portfolio, and action. RF-019.
- **RN-093 Dual control:** exceptions, reversals, overrides, collateral release, and beneficiary change require an independent second approver. RF-019.
- **RN-094 Approval limit:** include relevant exposure and requested amount under the matrix; splitting to evade authority is prohibited. RF-019.
- **RN-095 Temporary access:** elevated privilege expires and has a reason and post-review. RF-019.
- **RN-096 Administrator/business separation:** administrator has no financial-operation access by default; emergency access is logged and reviewed. RF-019.
- **RN-097 Versioned integration:** every message identifies origin, destination, schema, correlation, date, currency, and idempotency key. RF-020.
- **RN-098 External error:** classify as retryable, final, or unknown; retry only when semantically safe. RF-020.
- **RN-099 FX:** define rate source/type by contractual or regulatory purpose; never use today's spot rate to rewrite history. RF-020.
- **RN-100 External data:** preserve source, timestamp, purpose, and quality; surface conflicts for review. RF-020.
- **RN-101 Degradation:** an integration outage blocks only operations dependent on its confirmation/required data; status and queue are visible. RF-020.
- **RN-102 Complaints:** record received date, channel, subject, priority, and configured legal deadline using a versioned legal calendar; do not assume business/calendar days without the applicable rule. RF-021.
