# Partial and full prepayment

Quote `Q(t)=outstanding principal(t)+compensatory interest accrued through value date t+enforceable due obligations+permitted contractual costs`. Do not include future unaccrued interest. Receiving/confirming funds is a precondition to application.

For partial prepayment `X`, first apply prior obligations under the allocation rule; `X_net` reduces principal. New balance `P'=P-X_net`. Option A: retain maturity and recalculate payment using the method and remaining periods. Option B: retain target payment and solve for term or reduce the last payment; contract must define cents and date treatment. Do not promise to hold both payment and term constant.

For uniform French installments: `A'=P'i/[1-(1+i)^(-n)]`. For German method: recalculate target amortization as `P'/n`; interest-bearing installments decline. For irregular future dates, use the contractual periods and convention.

Full prepayment settles principal + accrual through effective date + due/permitted charges. The quote expires by date and new events. If the receipt is insufficient, apply partially only with instruction and disclose remaining balance; do not issue settlement. Once confirmed, principal is zero and future accrual stops; a bank discrepancy goes to reconciliation. Release collateral in a separate process.

Verifiable example: principal 10,000; 2,000 prepayment applied entirely to principal after accrued items are paid; effective monthly rate 1%; 10 months remaining. New French payment = `8,000*0.01/(1-1.01^-10) ≈ 844.66`. Expected value is approximate to cents; use high-precision decimal calculation and final-period adjustment.
