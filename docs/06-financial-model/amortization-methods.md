# Amortization methods

## French method (level payment, uniform periods)

Initial principal `P`, effective rate per period `i`, number of payments `n`. Payment before rounding: `A=P*i/[1-(1+i)^(-n)]`; if `i=0`, `A=P/n`. For each period: interest `I_k=B_(k-1)*i`; principal `C_k=A-I_k`; balance `B_k=B_(k-1)-C_k`. The final installment is adjusted to exact remaining balance plus period accrual to account for accumulated rounding.

Example: `P=10,000`, `i=1%`, `n=12`: theoretical A = 888.4878867834. If installments 1–11 are collected at 888.49 and the balance is updated from rounded cash postings, installment 12 is approximately 888.46; the exact booked amount depends on component-rounding rules. Retain calculation precision, allocate residual under the approved policy, and show the final adjustment.

## German method (constant principal)

`C=P/n` before adjustment; `I_k=B_(k-1)*i`; `A_k=C+I_k`; `B_k=B_(k-1)-C`. For the same example, amortization is 833.3333; first payment 933.3333, second 925.0000, final approximately 841.6667 before closing-rounding adjustment.

## Unequal periods / actual days

Do not use a uniform payment with `EA/m` when periods differ. Period factor `q_k=(1+EA)^(d_k/D)` if the contract defines an effective annual rate compounded by fraction; then interest is `B_(k-1)*(q_k-1)`. If the contract defines simple daily interest, use `I=B*r*d/D`. Freeze the selected method in the contract. For a constant payment with variable factors, solve `P=Σ A / Π_(j=1..k)(1+i_j)` for A; this is generalized French amortization. Independently verify cash flows.

## Principal grace

For `g` periods, principal amortization is zero (`C=0`) and current interest is paid. After grace, principal remains P and payment is recalculated for remaining term under contract. Unpaid interest is not capitalized in MVP.

## Edge cases

P=0 does not create a loan; i=0 uses equal principal; n must be an integer >0; payment above balance is separated as excess/prepayment; disbursement date different from first due date creates an irregular first period; rate change creates a prospective schedule and reset date; holiday adjustment follows the contractual rule. Verify total principal = funded principal and no negative balance.
