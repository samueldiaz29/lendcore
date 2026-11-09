# LendCore Development Roadmap

This roadmap is the single source of truth for implementation progress. A task is completed only after implementation, acceptance-criteria review, and test evidence have been reviewed. Status reflects the latest user-reported or reviewed development state.

## Status summary

| Status | Count |
|---|---:|
| PENDING | 14 |
| IN PROGRESS | 0 |
| BLOCKED | 0 |
| COMPLETED | 0 |
| **Total** | **14** |

## Phase progress

| Phase | Scope | Completed / Total | Progress |
|---|---|---:|---:|
| 1. Customer and evidence | Customer identity, parties, documents, consent | 0 / 2 | 0% |
| 2. Product and origination | Versioned product and credit application | 0 / 2 | 0% |
| 3. Assessment and decision | Capacity assessment and delegated decision | 0 / 2 | 0% |
| 4. Contract and disbursement | Accepted terms and confirmed single disbursement | 0 / 2 | 0% |
| 5. Loan administration | Reproducible fixed-rate schedules and balances | 0 / 1 | 0% |
| 6. Payments and ledger | Payment allocation, prepayment, reversal, reconciliation | 0 / 3 | 0% |
| 7. Delinquency, controls, and reporting | Collections, authorization, audit and reports | 0 / 2 | 0% |

## Phase 1 — Customer and evidence

### Customer and documents module

#### LEND-001 — Register individual and legal-entity customers

| Field | Details |
|---|---|
| Task ID | LEND-001 |
| Task name | Register individual and legal-entity customers |
| Phase | 1 — Customer and evidence |
| Module | Customer and documents |
| Priority | Critical |
| Status | [ ] PENDING — Not started |
| Dependencies | None |
| Objective | Register individuals and legal entities with validated identity, duplicate detection, entity representatives/authority evidence, customer status, and consent/basis records needed by downstream origination. |
| Business rules | RN-001–RN-004; RF-001; PR-001; INV-001; CA-001. See `docs/03-business-rules/business-rules.md`, `docs/02-requirements/functional-requirements.md`, and `docs/09-acceptance-criteria/acceptance-criteria.md`. |
| Acceptance criteria | Valid unique identity creates one customer; exact duplicate is blocked without mutation or merge; potential match is flagged for review; entity registration captures tax identifier and representatives and does not claim authority without current evidence; status and reason remain visible with history; consent/basis and revocation are retained; missing/malformed required fields cannot produce a ready-for-origination file. Include safe concurrent duplicate handling and focused automated tests. |
| Completion date | — |
| Review notes | Assigned as the first implementation task. Do not query external identity or bureau sources in this task. |

#### LEND-002 — Capture and review customer documents

| Field | Details |
|---|---|
| Task ID | LEND-002 |
| Task name | Capture and review customer documents |
| Phase | 1 — Customer and evidence |
| Module | Customer and documents |
| Priority | Critical |
| Status | [ ] PENDING — Not started |
| Dependencies | LEND-001 |
| Objective | Store versioned customer evidence with owner, type, issuer, dates, review outcome, and access history; expose mandatory evidence gaps to dependent flows. |
| Business rules | RN-005; RF-002; PR-001; CA-002. |
| Acceptance criteria | Evidence is associated with the correct customer/party, version and review history are retained, expired/illegible/inconsistent evidence is flagged, reviewed evidence is not overwritten, and missing mandatory evidence blocks only the dependent state. |
| Completion date | — |
| Review notes | Pending task assignment after LEND-001 approval. |

## Phase 2 — Product and origination

### Product and origination module

#### LEND-003 — Configure and publish a versioned credit product

| Field | Details |
|---|---|
| Task ID | LEND-003 |
| Task name | Configure and publish a versioned credit product |
| Phase | 2 — Product and origination |
| Module | Product and origination |
| Priority | Critical |
| Status | [ ] PENDING — Not started |
| Dependencies | LEND-001, LEND-002 |
| Objective | Maintain an eligible personal or limited-business credit product version with complete fixed-rate, currency, repayment, calendar, charge, limit, and validity terms. |
| Business rules | RN-006–RN-010; RF-003; US-002; CA-003. |
| Acceptance criteria | Incomplete/invalid product cannot be published; effective terms are versioned and frozen when used contractually; prior versions remain available; currency, rate type/basis, method, frequency, calendar, charges, eligibility, and limits are explicit. |
| Completion date | — |
| Review notes | Product policy values remain configurable; do not invent bank risk appetite or legal pricing decisions. |

#### LEND-004 — Register a credit application

| Field | Details |
|---|---|
| Task ID | LEND-004 |
| Task name | Register a credit application |
| Phase | 2 — Product and origination |
| Module | Product and origination |
| Priority | Critical |
| Status | [ ] PENDING — Not started |
| Dependencies | LEND-001, LEND-002, LEND-003 |
| Objective | Capture a personal or limited-business request linked to a customer and exact product version, preserving the submitted application snapshot. |
| Business rules | RN-011–RN-014; RF-004; PR-002; US-003; CA-004. |
| Acceptance criteria | Drafts can be saved incomplete; submission requires identity/authority, consent/basis, purpose, amount, currency, term, income/cash flow, obligations, and required evidence or an authorized exception; no source query occurs without applicable consent/basis; duplicate requests are linked or held; material changes make affected assessment stale. |
| Completion date | — |
| Review notes | — |

## Phase 3 — Assessment and decision

### Risk and decision module

#### LEND-005 — Assess repayment capacity and exposure

| Field | Details |
|---|---|
| Task ID | LEND-005 |
| Task name | Assess repayment capacity and exposure |
| Phase | 3 — Assessment and decision |
| Module | Risk and decision |
| Priority | Critical |
| Status | [ ] PENDING — Not started |
| Dependencies | LEND-004 |
| Objective | Produce a dated, reproducible assessment snapshot with income/cash flow, obligations, exposure, missing data, explainable indicators, and a recommendation. |
| Business rules | RN-015–RN-022; RF-005; PR-003; US-004; CA-005. |
| Acceptance criteria | Assessment uses versioned data/policy and authorized sources; income and debt currency treatment is explicit; missing/unavailable source data stays pending, incomplete, or error and never implies approval; material data changes stale the result; human override rationale is retained. |
| Completion date | — |
| Review notes | No numeric risk appetite or capacity threshold is specified by current documentation; use governed configuration, not hard-coded invented policy. |

#### LEND-006 — Record an authorized credit decision

| Field | Details |
|---|---|
| Task ID | LEND-006 |
| Task name | Record an authorized credit decision |
| Phase | 3 — Assessment and decision |
| Module | Risk and decision |
| Priority | Critical |
| Status | [ ] PENDING — Not started |
| Dependencies | LEND-005 |
| Objective | Allow a properly delegated decision-maker to approve, condition, return, or reject an application with rationale and validity. |
| Business rules | RN-023–RN-027; RF-006; PR-004; US-005; CA-006; authorization rules in `docs/02-requirements/actors-and-permissions.md`. |
| Acceptance criteria | Decision records actor, authority, policy version, rationale, conditions, and expiry; out-of-band authority, conflict, stale evidence, or missing required second approval blocks/escalates; analyst recommendation is distinct from approval; rejected case cannot proceed to disbursement. |
| Completion date | — |
| Review notes | Delegation bands and risk policy are configurable simulated-bank parameters. |

## Phase 4 — Contract and disbursement

### Contract and loan module

#### LEND-007 — Formalize and record accepted terms

| Field | Details |
|---|---|
| Task ID | LEND-007 |
| Task name | Formalize and record accepted terms |
| Phase | 4 — Contract and disbursement |
| Module | Contract and loan |
| Priority | Critical |
| Status | [ ] PENDING — Not started |
| Dependencies | LEND-006, LEND-003 |
| Objective | Freeze approved terms, schedule inputs, beneficiary, disclosures, conditions, and customer acceptance evidence for contract preparation. |
| Business rules | RN-028–RN-031; RF-007; PR-005; US-006; CA-007. |
| Acceptance criteria | Contract snapshot exactly matches approved offer; required conditions and acceptance exist before disbursement; material amount/rate/beneficiary change requires renewed review and acceptance; issued terms can expire or be declined without financial effect; history is retained. |
| Completion date | — |
| Review notes | This records evidence; it does not claim legal sufficiency of a signature. |

#### LEND-008 — Order and confirm single-tranche disbursement

| Field | Details |
|---|---|
| Task ID | LEND-008 |
| Task name | Order and confirm single-tranche disbursement |
| Phase | 4 — Contract and disbursement |
| Module | Contract and loan |
| Priority | Critical |
| Status | [ ] PENDING — Not started |
| Dependencies | LEND-007 |
| Objective | Create an idempotent disbursement request for the approved beneficiary and make the loan effective only on confirmed or authorized reconciled execution. |
| Business rules | RN-032–RN-035; RF-008; PR-006; US-007; CA-008a/b. |
| Acceptance criteria | Conditions and authorization are revalidated; request has stable external/correlation identity; duplicate callback creates one movement; timeout remains unknown and status is queried before retry; rejection creates no movement; confirmed value date and evidence activate one loan. |
| Completion date | — |
| Review notes | MVP supports one disbursement; external settlement remains authoritative. A simulator may stand in for the provider. |

## Phase 5 — Loan administration

### Contract and loan module

#### LEND-009 — Generate and preserve contractual repayment schedules

| Field | Details |
|---|---|
| Task ID | LEND-009 |
| Task name | Generate and preserve contractual repayment schedules |
| Phase | 5 — Loan administration |
| Module | Contract and loan |
| Priority | Critical |
| Status | [ ] PENDING — Not started |
| Dependencies | LEND-008, LEND-003 |
| Objective | Generate monthly fixed-rate French or German schedules from confirmed contract terms and value date, retaining reproducible inputs and schedule versions. |
| Business rules | RN-036–RN-044; RF-009; PR-006; US-008; CA-009a/b/d; `docs/06-financial-model/`. |
| Acceptance criteria | Validate positive principal and term; calculate correct method and zero-rate case; principal totals to funded amount; interest, dates, currency, rounding, grace, and irregular first period follow contract/configuration; final adjustment avoids negative balance; schedule changes create successor versions and preserve paid/overdue history. |
| Completion date | — |
| Review notes | MVP is fixed-rate, monthly, French/German, and principal-only grace. Detailed posting-rounding policy remains an open Finance/Accounting decision and must not be silently represented as approved. |

## Phase 6 — Payments and ledger

### Payments and operational ledger module

#### LEND-010 — Receive, identify, and allocate ordinary payments

| Field | Details |
|---|---|
| Task ID | LEND-010 |
| Task name | Receive, identify, and allocate ordinary payments |
| Phase | 6 — Payments and ledger |
| Module | Payments and operational ledger |
| Priority | Critical |
| Status | [ ] PENDING — Not started |
| Dependencies | LEND-009 |
| Objective | Record simulated/manual/imported receipts, confirm/identify funds, allocate them to obligations, and update the operational balance exactly once. |
| Business rules | RN-045–RN-054; RF-010; PR-007; US-009; CA-010a–f; INV-002–005. |
| Acceptance criteria | Validate loan, currency, amount, reference, dates and settlement; identical replay returns original outcome; conflicting same-key payload is investigated; concurrent duplicates apply once; partial payment remains partial; excess is unapplied or separately instructed; component totals reconcile with receipt and no cent is lost; failure after external confirmation is recoverable. |
| Completion date | — |
| Review notes | Allocation priority is a proposed baseline in `docs/06-financial-model/payment-allocation.md`; exact legal/contractual hierarchy remains an open Legal decision. Keep it explicitly configurable and do not claim legal approval. |

#### LEND-011 — Quote and apply prepayment or settlement

| Field | Details |
|---|---|
| Task ID | LEND-011 |
| Task name | Quote and apply prepayment or settlement |
| Phase | 6 — Payments and ledger |
| Module | Payments and operational ledger |
| Priority | High |
| Status | [ ] PENDING — Not started |
| Dependencies | LEND-010 |
| Objective | Quote an amount at a date and, after confirmed funds and customer instruction, apply partial principal prepayment or full settlement under the selected contractual option. |
| Business rules | RN-055–RN-062; RF-011; PR-008/014; US-010; CA-011a–d. |
| Acceptance criteria | Quote identifies accrued/due components and validity; expired quote recalculates; partial prepayment reduces principal and creates successor schedule under selected option; installment advance is distinct; insufficient settlement does not close; excess is controlled; reversal compensates and restores reconstructible balance; close only at reconciled zero. |
| Completion date | — |
| Review notes | Do not implement penalties or assume legal charge treatment absent approved policy. |

#### LEND-012 — Reverse and reconcile financial movements

| Field | Details |
|---|---|
| Task ID | LEND-012 |
| Task name | Reverse and reconcile financial movements |
| Phase | 6 — Payments and ledger |
| Module | Payments and operational ledger |
| Priority | Critical |
| Status | [ ] PENDING — Not started |
| Dependencies | LEND-008, LEND-010, LEND-011 |
| Objective | Investigate confirmed external events, reconcile them to one local movement, and correct errors through authorized compensating entries. |
| Business rules | RN-083–RN-087; RF-017; PR-015; US-015; CA-017; INV-001/002/005. |
| Acceptance criteria | Original confirmed movement remains immutable; reversal references original, reason, actor, date, and required independent approval; duplicate/excess reversal is denied; uncertain external state is investigated before action; derived balance/schedule is reproducible and reconciled. |
| Completion date | — |
| Review notes | — |

## Phase 7 — Delinquency, controls, and reporting

### Collections module

#### LEND-013 — Detect delinquency and manage collection cases

| Field | Details |
|---|---|
| Task ID | LEND-013 |
| Task name | Detect delinquency and manage collection cases |
| Phase | 7 — Delinquency, controls, and reporting |
| Module | Collections |
| Priority | High |
| Status | [ ] PENDING — Not started |
| Dependencies | LEND-010, LEND-012 |
| Objective | Identify unpaid due amounts at cut-off and support manual, traceable collection activity without changing contractual balances through promises or notes. |
| Business rules | RN-071–RN-076; RF-014; PR-010/011; US-013; CA-014. |
| Acceptance criteria | Delinquency remains separate from loan state; age and overdue amounts derive from effective allocations; simple default interest uses only approved configured base/rate; payment in transit/dispute is investigable and adverse escalation follows policy; promises do not amend schedule or debt. |
| Completion date | — |
| Review notes | Exact default-interest and collection policy are legal/bank open items in the documentation. |

### Authorization and audit module

#### LEND-014 — Enforce authorization and provide essential audit/reporting

| Field | Details |
|---|---|
| Task ID | LEND-014 |
| Task name | Enforce authorization and provide essential audit/reporting |
| Phase | 7 — Delinquency, controls, and reporting |
| Module | Authorization, audit, and reporting |
| Priority | Critical |
| Status | [ ] PENDING — Not started |
| Dependencies | LEND-001–LEND-013 (as applicable to each protected action and report) |
| Objective | Apply action/scope/amount/state/validity permissions and preserve audit evidence; produce essential customer, loan, movement, decision, and balance views with reproducible cut-offs. |
| Business rules | RN-088–RN-096; RF-018/019; CA-018/019; `docs/02-requirements/actors-and-permissions.md`. |
| Acceptance criteria | Unauthorized/revoked action is denied and audited; maker-checker conflicts and configured limits are enforced; sensitive data access is controlled; history records actor/time/change/rationale; reports preserve parameters, cut-off, time zone, and source evidence; reports do not mutate business records. |
| Completion date | — |
| Review notes | Some controls are required earlier at each financial operation; this task consolidates and verifies them rather than deferring basic authorization until the end. |

## Blocked tasks

None currently recorded. An unresolved policy question blocks only the affected behavior that cannot safely be configured; it does not automatically block unrelated development.

## Change log

| Date | Change |
|---|---|
| 2026-11-09 | Created roadmap from the existing MVP scope and requirement traceability. Added LEND-001 as the first assigned task, initially PENDING; no implementation has been submitted for review. |
