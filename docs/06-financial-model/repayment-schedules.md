# Repayment schedules

Generate dates from disbursement and contractual frequency: weekly = +7 days; every 15 days = +15 days; monthly = same calendar day with an explicit rule for nonexistent dates (preserve month-end if contracted). If “twice monthly,” configure explicit dates (for example, the 15th and month-end); do not label this as a 15-day interval.

Each installment stores sequence, due date, opening balance, principal, compensatory interest, default interest, permitted fee/expense, insurance, total, closing balance, and schedule version. Third-party charges are distinct and disclose their basis. Never generate negative principal.

### Irregular installment

Calculate initial period from disbursement value date to first due date using the published convention. The general cash-flow method discounts payments using each interval's rate; the product defines whether the first payment is irregular, interest-only, or full. Do not hide a short/long period's interest in principal.

### Schedule changes

A date/rate/prepayment change creates a new snapshot linked to its predecessor with reason, approver, effective date, and cut-off balance. Settled installments and movements remain immutable. Explain any difference from projection in the new plan and notify the customer where required.
