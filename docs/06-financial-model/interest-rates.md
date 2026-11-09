# Rates and conversions

## Contractual definitions required

Every rate defines numeric value, type (nominal/effective), reference annual period, compounding frequency, currency, day-count basis, effective date, index/margin if variable, caps, conversion method, and rounding. “12% annual” is insufficient.

## Conversions

- Effective annual `EA` to effective rate per homogeneous period of `m` periods/year: `i_p=(1+EA)^(1/m)-1`.
- Effective periodic rate to effective annual: `EA=(1+i_p)^m-1`.
- Nominal annual convertible `m` times: `i_p=j_nom/m`; `EA=(1+j_nom/m)^m-1`. This is valid only when the contract defines a nominal rate with that compounding frequency.
- Effective annual rate to effective factor for fraction `t`: `i_t=(1+EA)^t-1`, if contract/day-count convention uses compounding for fractional periods.
- Simple daily proration for balance `B`, annual effective rate `r`: `I=B*r*d/D`; Actual/360 uses `D=360`; Actual/365 uses `D=365`; leap years still use D=365 under fixed Actual/365. This must be explicitly defined in contract/product.

Day-count convention defines fraction `t`; it does not automatically convert a nominal rate to an effective rate or authorize compounding. ACT/ACT is unsupported. 30E/360 uses a 360-day year and 30-day months: `360(Y2-Y1)+30(M2-M1)+(min(D2,30)-min(D1,30))`; end-of-February and start/end date cases must be fixed in the contract using a documented 30E/360 variant.

## Nominal vs effective example

12% nominal annual convertible monthly: period rate `0.12/12=1%`; EA `(1.01)^12-1=12.6825030132%`. A 12% EA corresponds to a period rate `(1.12)^(1/12)-1≈0.948879%`, not 1%.

## Variable rates

Record index value, observation date, source, margin, limits, period, notice, rounding rule, and effective date. Review creates a new snapshot. Closed accruals retain the prior rate; new rate applies prospectively from a future effective date. If the index is unavailable/discontinued, apply the agreed clause and escalate to Legal; do not freeze or replace it arbitrarily.

## Caps

BCRP maximum interest rates depend on currency and semester for categories subject to Law 31143/Circular 0008-2021-BCRP. Resolve the limit by effective date and category; do not hard-code a semester's rate as a constant. Confirm scope (consumer/small-business credit or other legal cases) before validation; a bank may be treated differently for transactions outside that scope. Default interest follows its specific rules. Sources and effective periods belong in compliance configuration.
