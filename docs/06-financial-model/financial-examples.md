# Calculated financial examples

These are mathematical examples under explicit assumptions, not contractual quotes. Values are calculated without intermediate rounding and then displayed to 2 decimals.

| TC | Input | Rule | Expected |
|---|---|---|---|
| TC-001 | PEN 10,000; 12 installments; 1% effective monthly | French | Theoretical payment 888.4878867834. If installments 1–11 are each collected at 888.49 and interest is computed on the cent-rounded cash balance, installment 12 is approximately 888.46 to close principal at zero. Exact booked component amounts depend on the approved rounding rule. |
| TC-002 | PEN 10,000; 12 installments; 1% effective monthly | German | Principal 833.333333 per installment; first payment 933.333333; second 925.00; final principal adjusted to residual. |
| TC-003 | 12% nominal annual, monthly | Conversion | Monthly rate 1%; EA 12.6825030132%. |
| TC-004 | 12% EA; ACT/360; 30 days; balance 10,000 | Compound factor | Interest ≈94.89. |
| TC-005 | 12% simple annual; ACT/360; same values | Simple proration | Interest 100.00; differs from TC-004. |
| TC-006 | Balance 1,000; 10% simple annual default; 18 days; D=360 | Default interest | 5.00, no capitalization. |
| TC-007 | Due interest 20, due principal 100, payment 70 | Proposed interest-first order | 20 to interest, 50 to principal; 50 remains overdue. |
| TC-008 | Principal 10,000; 2,000 principal prepayment; 10 months; 1% effective | French, same term | New theoretical payment ≈844.66; no future interest on repaid principal. |

## Reproducible verification

For TC-001 the unrounded French payment is `10000*0.01/(1-1.01^-12) = 888.4878867834`. As a separate cash-rounding illustration, iterating the loan balance from PEN 10,000 using 1% interest on the cent-rounded opening balance and eleven payments of PEN 888.49 leaves about PEN 879.690977 before the final month's interest, so the closing installment is about PEN 888.46. Exact results can differ by a cent depending on whether component or payment amounts are rounded at each posting; the final fixture cannot be frozen until DP-003 is approved. TC-001/002 theoretical values are unrounded.
