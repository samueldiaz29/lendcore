# Financial test cases

TC-001..008 are described in `06-financial-model/financial-examples.md`. Freeze fixtures after rounding policy approval. Add these edge cases:

| ID | Setup and action | Expected result |
|---|---|---|
| TC-009 | Disbursement Jan 31, first due Feb 28, ACT/365, EA 12%, principal 1,000 | 28-day period under include-start/exclude-end; compound fractional interest uses `t=28/365` = approximately 8.73; retain factor/date. |
| TC-010 | 30E/360 from Jan 31 to Feb 28 | 28 days when 31→30 at start and 28 at end; confirm implemented contractual variant. |
| TC-011 | Payment 500 applied to overdue items concurrently with partial prepayment | One operation locks/revalidates balance; the other requotes; principal is not overpaid. |
| TC-012 | USD payment to PEN loan with no conversion | Reject/do not apply; do not infer FX. |
| TC-013 | FX USD/PEN 3.75 converts USD 100 | Store USD 100 source, PEN 375.00 destination, rate/provider/time. |
| TC-014 | Rate changes after 10 days in a 30-day period | Split interval; past segment uses old rate, future segment uses new rate only after effective date. |
| TC-015 | Payment after close with bank-proven earlier value date | Create date reconciliation/review; adjust only with authorization and audit; recalculate from value date without deleting movements. |
| TC-016 | Partial payment with interest 10.005 | Under proposed HALF_UP policy, round to 10.01 and explicitly assign residual; validate with Accounting/Legal. |
| TC-017 | Reversal of already compensated payment | Reject excess reversal and retain original/first reversal. |
| TC-018 | Full prepayment quoted while two debits are concurrent | First confirmed settles; second cannot create negative balance and remains excess/unapplied pending instruction. |

**Precision note:** TC-009 exact value is recalculated as `1000*((1.12)^(28/365)-1)`; displayed value is approximate. Exact fixture must use high-precision decimal arithmetic. 30E/360 cases depend on the contractual variant configured on the product.
