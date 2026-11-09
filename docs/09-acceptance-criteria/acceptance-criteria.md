# Acceptance criteria

## Customer and product
- **CA-001:** Given a registered identifier, when a matching customer is created, then automatic creation is blocked and a potential duplicate is shown without merging records.
- **CA-002:** Given an expired/illegible document, when the file is reviewed, then it is flagged and the application cannot proceed to assessment if the document is mandatory.
- **CA-003:** Given a product without day-count convention or typed rate, when publication is attempted, then publication fails with missing fields; changing product version does not alter a signed loan.

## Origination and approval
- **CA-004:** Given missing consent or an incomplete file, when an application is submitted, then it remains draft/incomplete and no external source is queried.
- **CA-005:** Given an unavailable bureau provider, when assessment runs, then the result is visibly pending/error; missing data never causes automatic approval.
- **CA-006:** Given a decision amount above the user's authority, when the approver tries to confirm, then the system escalates and retains the draft; an out-of-band approver cannot force it.

## Formalization and disbursement
- **CA-007:** Given the beneficiary changes after approval, when the contract is prepared, then new review/approval and acceptance are required.
- **CA-008a:** Given a confirmed disbursement order, when the same callback arrives twice, then only one movement exists.
- **CA-008b:** Given an order timeout, when the operator retries, then prior status is queried and no second order is issued until resolved.

## Schedule
- **CA-009a:** Given principal PEN 10,000, 12 periods, and 1% effective monthly rate, when French amortization is generated without interim rounding, then theoretical payment is PEN 888.4878867834 and total principal amortization is PEN 10,000. If each of the first 11 cash installments is rounded to PEN 888.49 and interest is posted on the cent-rounded balance, the last installment is approximately PEN 888.46; production expected cents depend on the approved posting-rounding rule and must be fixed with Finance/Accounting.
- **CA-009b:** Given the same terms under German amortization, then theoretical principal amortization is constant at 833.333333 and interest-bearing payments decline with balance.
- **CA-009c:** Given a 15-day frequency, when dates are generated, then each due date is 15 calendar days apart, not the 15th/month-end.
- **CA-009d:** Given two periods of principal grace, then principal paid in both is zero, interest is charged, and principal does not grow through automatic capitalization.

## Payments and prepayment
- **CA-010a exact amount:** Given an obligation of 100.00 and confirmed receipt of 100.00, then 100.00 is allocated once and the installment is paid.
- **CA-010b insufficient:** Given an obligation of 100.00 and receipt of 40.00, then installment is partial with 60.00 remaining.
- **CA-010c duplicate:** Given same source/ID and identical payload, then return the original result with no second movement; different payload under same ID creates a dispute.
- **CA-010d concurrency:** Given two simultaneous requests with the same ID, then only one effective application occurs; if different IDs exceed debt, excess is separated.
- **CA-010e external failure:** Given bank confirmation but local response failure, when callback is retried, then event is recovered idempotently and reconciled.
- **CA-010f rounding:** Given allocations totaling 99.99 against a 100.00 payment, then the cent is explicitly assigned by rule or remains unapplied; it is never lost.
- **CA-011a partial prepayment:** Given net prepayment 2,000 against principal 10,000, then new principal is 8,000 and the new schedule follows the selected option.
- **CA-011b insufficient full settlement:** Given a quote of 1,000 and confirmed payment of 999.99, then loan is not closed and remainder is shown.
- **CA-011c reversal:** Given an applied prepayment is later reversed with authorization, then a compensating movement reopens balance; prior schedule is not overwritten.
- **CA-011d expired quote:** Given yesterday's quote, when applying today, then accrual is recalculated and the difference must be confirmed.

## Operations, collateral, control
- **CA-012:** Given a new fixing effective in the future, then only future periods are recalculated; past accrual remains unchanged.
- **CA-013:** Given unperfected collateral, then it is shown as pending and is not counted for approval coverage.
- **CA-014:** Given an overdue installment and payment under reconciliation, then delinquency remains investigable and adverse automated actions are suspended under policy.
- **CA-015:** Given refinancing is in progress, then the old obligation remains until the new one is confirmed and effective.
- **CA-016:** Given a written-off loan, then debt/history remain available and recovery is recorded separately.
- **CA-017:** Given a confirmed movement, then an operator cannot edit/delete it; reversal requires reference, reason, and dual approval.
- **CA-018:** Given a report at a cut-off date, then report parameters/date/time zone are recorded and movement figures can be reproduced.
- **CA-019:** Given a role is revoked, then an unconfirmed operation loses authorization and the event is audited.
- **CA-020:** Given a repeated external message, then correlation/idempotency prevents duplicate effect and invalid schema is rejected with reason.
- **CA-021:** Given a payment complaint, then it links to receipt/allocation, preserves movement, and records deadline/status without exposing another customer's data.
