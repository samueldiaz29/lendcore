# State machines

A transition requires an authorized actor, satisfied condition, event, and auditable log. Loan contractual state and delinquency are separate dimensions.

| Entity | States / permitted transitions | Restrictions / effects |
|---|---|---|
| Customer | DRAFT→PENDING_VERIFICATION→ACTIVE/OBSERVED; ACTIVE→RESTRICTED/INACTIVE; correction→ACTIVE after validation | Restriction does not delete loans; Operations/Compliance act by cause. |
| Application | DRAFT→SUBMITTED→INCOMPLETE or UNDER_ASSESSMENT→UNDER_REVIEW→CONDITIONALLY_APPROVED/APPROVED/REJECTED; approved→EXPIRED; conditional→FORMALIZATION; withdrawal→WITHDRAWN | Rejected application is not edited; a new application links to it. |
| Assessment | PENDING→IN_PROGRESS→COMPLETE/INCOMPLETE/ERROR; COMPLETE→STALE on material data change | Retry creates a versioned attempt; does not overwrite results. |
| Decision | PENDING→APPROVED/CONDITIONAL/REJECTED/RETURNED; approval→EXPIRED/REVOKED before contract | Decision-maker must be within delegated band; revocation has rationale. |
| Contract | PREPARATION→ISSUED→ACCEPTED→EFFECTIVE; issued→EXPIRED/DECLINED; accepted→VOIDED only under authorized pre-disbursement condition | Material amendment creates new version and acceptance. |
| Disbursement | REQUESTED→PENDING_EXTERNAL→CONFIRMED/REJECTED/UNKNOWN; unknown→confirmed/rejected by query/reconciliation | Confirmation creates movement; unknown blocks duplicate order. |
| Contractual loan | PROPOSED→ACTIVE on disbursement; ACTIVE→SETTLED/REFINANCED/WRITTEN_OFF on approved event; closure→CLOSED | Written-off loan may still be collected; SETTLED requires confirmed zero balance. |
| Delinquency | CURRENT↔OVERDUE; OVERDUE→IN_COLLECTION/IN_DISPUTE; can coexist with ACTIVE loan; cures after overdue obligations satisfied | Not a contractual state; calculate days and overdue balance. |
| Installment | SCHEDULED→OVERDUE; SCHEDULED/OVERDUE→PARTIAL→PAID; authorized change→RESCHEDULED; reversal may reopen via new history | Paid installment is not deleted; reversal creates traceable open balance. |
| Payment | RECEIVED→UNIDENTIFIED/SETTLING→CONFIRMED→APPLIED→RECONCILED; rejected; applied→REVERSED | External transition carries correlated event; applied payment is not deleted. |
| Guarantee | PROPOSED→UNDER_VALIDATION→PERFECTED→ACTIVE→ENFORCEMENT→RELEASE_PENDING→RELEASED; rejected/expired | Release needs covered debt resolution/approval; enforcement is external. |
| Collection | OPEN→ASSIGNED→CONTACTED→PROMISE/DISPUTE/ESCALATED→RESOLVED/CLOSED | Promise does not alter balance. |

Prohibited transitions: rejected application→disbursement; pending payment→applied; active loan→closed without reconciled zero; proposed collateral→counted as perfected; confirmed movement→deleted/modified.
