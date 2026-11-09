# User stories and acceptance references

## Epic: Customer and product

### US-001 — Maintain customer file
As an adviser, I want to register an individual or legal entity and its authorized parties so I can start an application with verifiable identity.

- Context: RF-001, RF-002; RN-001..005; PR-001.
- Preconditions: authenticated user assigned to the portfolio.
- Main flow: capture identity/authority → search for matches → attach evidence → validate required fields → leave file as draft or ready.
- Alternatives: potential duplicate goes to review; expired document is flagged; legal entity without current authority cannot sign.
- Exceptions: source outage leaves verification pending.
- Acceptance: CA-001, CA-002.

### US-002 — Publish versioned product
As a product owner, I want to publish financial terms with an effective period so offers and contracts can be reproduced.
- RF-003; RN-006..010; PR-002; CA-003. Publication requires rate/type/basis, method, currency, calendar, charges, eligibility, and limits; a new version does not change a signed loan.

## Epic: Origination and risk

### US-003 — Apply for credit
As a customer/adviser, I want to submit an amount, purpose, and evidence to request financing.
- RF-004; RN-011..014; PR-002; CA-004. The flow saves a draft, validates information, and requires consent before source queries; resubmission does not create a duplicate application.

### US-004 — Assess repayment capacity
As a credit analyst, I want to review capacity, debt, sensitivity, sources, and an explainable recommendation to decide with context.
- RF-005; RN-015..022; PR-003; CA-005. Missing data or unavailable bureau does not equal approval; a reasoned override remains visible.

### US-005 — Resolve an application
As an approver, I want to approve, condition, return, or reject within my delegation to authorize credit responsibly.
- RF-006; RN-023..027; PR-004; CA-006. The system validates validity, limits, segregation, and exceptions; decision records policy, rationale, and authority.

## Epic: Formalization and loan

### US-006 — Formalize approved terms
As operations staff, I want to issue documents and freeze accepted terms so disbursement follows the approval.
- RF-007; RN-028..031; PR-005; CA-007. A change to amount/rate/beneficiary returns for approval and acceptance.

### US-007 — Disburse a loan
As a disbursement operator, I want to send a unique order and obtain its confirmation so funds are not sent twice.
- RF-008; RN-030..035; PR-006; CA-008. Timeout remains unknown; query before retry; only confirmation creates an effective movement.

### US-008 — Administer the schedule
As operations staff, I want to generate a schedule under the selected method, rate, day-count, and calendar so correct obligations can be collected.
- RF-009; RN-036..044; PR-006; CA-009. Test French/German methods, grace, holidays, irregular periods, and final adjustment.

## Epic: Loan servicing

### US-009 — Apply a payment
As operations staff, I want to identify, settle, and allocate a payment without duplication so debt and installments update correctly.
- RF-010; RN-045..054; PR-007; CA-010. Include exact, insufficient, partial, duplicate, concurrent, rounding difference, reversal, and external-error scenarios.

### US-010 — Make a prepayment
As a customer, I want to choose a lower installment or shorter term and know the balance as of a date so I can reduce future interest.
- RF-011; RN-055..062; PR-008; CA-011. Partial/full prepayment requires instruction, confirmed funds, and a new schedule; installment advance is a distinct option.

### US-011 — Review variable rate
As operations staff, I want to record a new rate with an effective date so future accrual follows the contract.
- RF-012; RN-063; PR-009; CA-012. No retroactive change; missing index is escalated.

### US-012 — Manage collateral
As an analyst, I want to link evidence of value and perfection so actual coverage and follow-up obligations are known.
- RF-013; RN-064..070; PR-005; CA-013. Pending collateral is not treated as perfected; release requires approval.

### US-013 — Manage delinquency and collections
As a collections agent, I want to prioritize overdue installments and record contact/promises so recovery is managed within policy.
- RF-014; RN-071..076; PR-010/011; CA-014. Simple default interest; disputes/pending payments remain visible; a promise does not change debt.

### US-014 — Reschedule or refinance
As an analyst, I want to propose new terms and reassess current capacity so an approved, traceable modification can be formalized.
- RF-015; RN-077..081; PR-012/013; CA-015. Old obligation is preserved until the new arrangement takes effect.

### US-015 — Reverse an operation
As an authorized operator, I want to compensate an erroneous operation while preserving the original so balances can be reconstructed and explained.
- RF-017; RN-083..087; PR-015; CA-017. Second control required; reversed amount cannot exceed original; replay is idempotent.

### US-016 — Review audit and reports
As an auditor/manager, I want to reconstruct a decision, balance, and movements as of a cut-off date to control the portfolio.
- RF-018/019; RN-088..096; CA-018/019.

### US-017 — Integrate external sources and complaints
As operations staff, I want to reconcile external references and route complaints so discrepancies can be resolved without losing evidence.
- RF-020/021; RN-097..102; CA-020/021.
