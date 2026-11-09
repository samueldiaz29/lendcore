# Loan financial model: concepts, rules, and worked methods

## Purpose and precedence

This guide explains the amounts represented in a loan schedule and the relationships among rate, time, principal, payment, and balance. The detailed calculation contracts are in the linked rate, interest, amortization, payment-allocation, prepayment, default-interest, schedule, and rounding documents. All figures below are illustrative, not bank pricing, a customer quote, or a legal conclusion. Product/contract terms and applicable law govern. Open interpretation or accounting questions remain marked for validation in [governance decisions](../10-project-governance/assumptions-and-decisions.md).

## Core concepts

| Term | Meaning and distinction |
|---|---|
| Principal | Amount of credit funded to the borrower. A limit or approved amount is not principal until disbursed. |
| Outstanding principal | Funded principal still unpaid after principal allocations and effective adjustments. It excludes separately due interest and charges. |
| Compensatory interest | Contract price for using outstanding principal over time. It accrues under the rate and day-count terms. |
| Default/moratory interest | A legally/contractually permitted consequence of overdue payment. In the initial design it is simple, separately tracked, and never added to principal to earn further interest. It is not a penalty fee. |
| Installment | A dated amount due, commonly composed of principal and compensatory interest, with permitted charges/insurance shown separately. |
| Effective rate | A rate whose period yield includes compounding within its stated period. |
| Nominal rate | An annual quotation that requires a declared conversion/compounding frequency to derive period rates. |
| Prepayment | Money applied to outstanding principal before the scheduled maturity, reducing future compensatory interest. |
| Installment advance | Money held/applied toward future scheduled installments without the same immediate principal reduction. Its effect must be distinguished and disclosed. |
| Grace of principal | A period in which scheduled principal amortization is zero while current interest remains payable. It is not full-payment grace. |

## Business rules and invariants

- **FM-001 (confirmed decision):** contractual currency is PEN or USD and every amount carries its currency; never add unlike currencies without an explicit, evidenced conversion.
- **FM-002 (confirmed decision):** financial decimal arithmetic is intended to use Java `BigDecimal`; binary floating-point is not authoritative for money.
- **FM-003 (confirmed decision):** French and German amortization are supported; weekly, exactly every 15 calendar days, and monthly repayment frequencies are supported. Twice-per-month dates are a distinct calendar choice.
- **FM-004 (confirmed decision):** supported day-count choices are Actual/360, Actual/365, and 30E/360. The specific rate interpretation, boundary convention, and 30E variant must be frozen by contract/product.
- **FM-005 (confirmed decision):** fixed and variable rates are in scope by release; a fixing change affects only future accrual after its effective date.
- **FM-006 (confirmed decision):** initial grace is principal-only; current interest remains due and unpaid interest does not automatically increase principal.
- **FM-007 (confirmed decision):** unpaid interest is not automatically capitalized; initial default interest is not compounded. Exact overdue base/rate must be legally validated.
- **FM-008 (confirmed decision):** schedule recalculation preserves earlier schedule versions, paid installments, and financial movements.
- **FM-009 (proposal DP-003):** settlement scale of two decimals, at least 12 decimal places for intermediate calculations, and HALF_UP rounding are proposals, not approved accounting/legal policy.
- **FM-010 (proposal DP-004):** interest interval includes its start date and excludes its end date. The contract must choose a boundary convention before use.
- **FM-011:** calculation inputs, source, precision, dates, effective events, formula, and rounding result must be explainable and reproducible.
- **FM-012:** only confirmed money is applied. Allocation sum equals the applied part of the receipt; any excess remains separately instructed or unapplied.

## Rate types and time fractions

For nominal annual rate `j` convertible `m` times annually, the period rate is `i = j/m` and the equivalent effective annual rate is `(1+i)^m - 1`. For effective annual rate `EA`, equivalent homogeneous periodic rate is `(1+EA)^(1/m)-1`. Therefore 12% nominal convertible monthly gives a 1% monthly rate and about 12.682503% effective annual; 12% effective annual gives about 0.948879% monthly. They are not interchangeable.

Day-count selects the year fraction; it does not on its own decide whether the rate is simple or compounded. For simple annual proration, `I = B × r × d/D`. For an effective annual rate applied with fractional compounding, `I = B × ((1+EA)^(d/D)-1)`. Contract and product specify which model applies. Actual/360 uses actual elapsed days over 360. Actual/365 uses actual days over 365 even in a leap year under this fixed convention. 30E/360 transforms each month to 30 days; the chosen variant controls month-end treatment.

## Amortization systems

### French (level payment for uniform periods)

For opening principal `P`, effective periodic rate `i`, and `n` equal periods, the theoretical payment is `A = P i / (1-(1+i)^(-n))`; at zero rate, `A=P/n`. In each period, interest is opening balance times period rate, principal is payment less interest, and closing principal is opening principal less principal paid. Payments are level before rounding when rate and periods are uniform. With irregular actual dates or rate resets, period factors differ and payment must be solved from discounted cash flows rather than by blindly dividing an annual rate by payment frequency.

### German (constant principal)

Principal amortization is `P/n` before final residual adjustment. Each period's interest is calculated on opening principal. Therefore payment generally declines over time as principal falls. This differs from French amortization, which keeps the total scheduled payment level for equal periods and changes its principal/interest mix.

### Worked comparison (illustrative)

PEN 10,000, 12 monthly periods, 1% effective monthly, no fees/insurance, no intermediate rounding:

| Method | First payment | Second payment | Principal pattern | Total theoretical interest |
|---|---:|---:|---|---:|
| French | 888.4878868 | 888.4878868 | Increasing principal portion | 661.8546414 |
| German | 933.3333333 | 925.0000000 | 833.3333333 principal each period | 650.0000000 |

French payment calculation: `10,000 × 0.01 / (1 - 1.01^-12) = 888.4878868`. Period 1 interest is `10,000 × .01 = 100`; principal is `788.4878868`; closing principal is `9,211.5121132`. German period 1 principal is `10,000/12 = 833.3333333`, interest is 100, payment is 933.3333333. The theoretical totals assume unrounded exact installments; customer settlement values and final installment depend on approved rounding policy.

## Frequency, dates, and grace

Weekly means seven calendar days between anchors. Every-15-day means exactly 15 calendar days; it is not a pair of fixed dates per month. Monthly preserves a defined anchor (including an explicit month-end rule). A non-business-day adjustment changes the due date and potentially the actual accrual duration, so the convention and calendar are contractual. A disbursement date later than/before the first scheduled boundary creates a short or long first accrual segment; do not conceal it by silently changing principal.

For two periods of principal grace on PEN 10,000 at 1% monthly, and assuming due current interest: periods 1 and 2 each have principal due 0, interest due PEN 100, and closing principal remains PEN 10,000. The principal does not grow to PEN 10,100 or PEN 10,200. After grace, amortization is calculated over the remaining contractual term. If interest is unpaid, record it as due under policy; do not capitalize automatically.

## Payment allocation and prepayment distinctions

An incoming amount moves through receipt, settlement, identification, application, and reconciliation. These states are not synonyms. The allocation priority must be legally valid for the product and disclosed. The current proposal is in [payment allocation](payment-allocation.md); default-interest base and priority, fees, and expenses remain open for Legal. A short payment may partially satisfy an installment and leave an overdue amount. A duplicate with identical source/id/payload returns the recorded outcome. Same ID with different payload is blocked. Excess is not revenue and is not silently appropriated.

For a principal prepayment, first apply any due amounts according to the valid allocation rule; the net principal portion reduces balance. A borrower may select the contractually supported option of keeping maturity and lowering payment, or shortening term under the agreed payment treatment. They cannot hold both payment and maturity constant after reducing principal unless the contract defines some other economic adjustment. An installment advance is not an equivalent principal prepayment. Full settlement includes principal and accrual through its effective value date, plus only permitted due items; an expired quote must be refreshed.

Illustration: after due items are covered, a PEN 2,000 principal prepayment against PEN 10,000 leaves PEN 8,000 principal. At 1% monthly with 10 uniform remaining periods, French payment becomes `8,000 × .01/(1-1.01^-10) = 844.656...`, approximately PEN 844.66 before final-period/rounding treatment. Future compensatory interest is calculated on the reduced balance.

## Default interest, posting precision, and versions

Illustration only: permitted overdue base PEN 1,000, simple annual rate 10%, 18 days, Actual/360 gives `1,000 × .10 × 18/360 = PEN 5.00`. This formula does not establish that this base or rate is lawful for a specific LendCore loan. Do not calculate default interest on a balance that contains capitalized default interest. If principal or base changes mid-period, split the time interval and preserve each segment in calculation evidence.

Do not round each internal operation without a specified posting rule. Retain exact inputs and calculation precision; round at the contractually/accounting-approved component or settlement point. Sum of allocations must reconcile exactly to applied funds. Any residual cent is assigned by an approved eligible-component rule or remains explicitly unapplied. A schedule recalculation creates a successor version with reason, effective date, cutoff balance, parameters, and approval. Paid installments and closed accruals are not rewritten.

## Failure and validation cases

Missing rate type, basis, day-count, calendar, or payment method prevents a reproducible schedule. A zero rate uses equal principal in either method; zero principal or non-positive term is invalid. A variable index outage follows the contract's fallback clause or escalates; it is not replaced with an invented value. A payment with foreign currency is not applied absent an explicit FX instruction/quote. An overpayment cannot create negative principal. A late value date correction requires authoritative evidence and an authorized, auditable recalculation. A failed or reversed movement creates a linked compensation and successor schedule as needed; it never deletes historic calculation evidence.

## Related references

[Interest rates](interest-rates.md) · [Interest calculation](interest-calculation.md) · [Amortization methods](amortization-methods.md) · [Repayment schedules](repayment-schedules.md) · [Payment allocation](payment-allocation.md) · [Prepayment](prepayment-calculation.md) · [Default interest](late-interest.md) · [Rounding and precision](rounding-and-precision.md) · [Financial test cases](financial-examples.md).
