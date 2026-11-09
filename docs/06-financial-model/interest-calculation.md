# Interest accrual

For period `[start date, end date)` and principal balance `B`:

1. Determine value dates and effective events in chronological order.
2. Split the interval at each balance or rate change.
3. Calculate days `d` under the contractual convention.
4. Apply the rate/convention for each segment and aggregate without premature rounding.
5. Round to currency unit at the configured accounting point and retain the unrounded value for explanation/reconciliation.

Example: `B=10,000`, 12% annual simple interest under ACT/360, 30 days: `10,000*0.12*30/360=100.00`. With 12% EA compounded over fraction `t=30/360`, interest is `10,000*((1.12)^(30/360)-1)≈94.89`. These are different contracts, not interchangeable results.

Conventions: Actual/360 counts actual calendar days and divides by 360; Actual/365 counts actual days and uses a fixed divisor of 365; 30E/360 transforms months/year under the convention. Define whether the initial/final day is included (proposal: include start, exclude end). Weekends and holidays do not stop accrual.

Calculation and posting evidence must include currency, base balance, dates, days, divisor/factor, exact rate, source, version, and result. Intraday changes are ordered by effective date and sequence; same-date events need a precedence rule (for example, whether a settled payment occurs before or after contractual cut-off). Keep accounting date, receipt date, and value date separate.
