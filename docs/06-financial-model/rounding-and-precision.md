# Precision and rounding

## Proposal DP-003

The intended Java monetary representation is `BigDecimal`, so decimal values are not converted through binary floating-point. Settlement scale for PEN/USD is proposed at 2 decimal places, with at least 12 decimal places in intermediate calculations; these scale and rounding details remain proposals. Retain rates at least to source precision and enough precision for reproducible calculations. Implementation must explicitly define decimal context, scale transitions, and approved rounding mode; never use `double`/`float` as the source of financial values.

- Period interest: sum segments at high precision and round when posted under contract.
- Installments: display/settle at 2 decimals; allocate principal/interest under an explicit consistent rule; final installment adjusts documented residual.
- Payment: total allocation must equal confirmed receipt exactly; assign residual cents using a known eligible-priority rule, never lose them.
- FX: round destination amount to 2 decimals in destination currency; retain rate and rounding.
- Default interest: proposed rounding at liquidation/payment date, not daily, unless contract/law requires otherwise.

Suggested mode for ordinary amounts: HALF_UP for symmetry with decimal presentation; Legal/Accounting must validate contracts and accounting practice. Regulation may require specific treatment. Tests cover 0.005, 0.0049, negative values only for reversals, high magnitudes, and installment sums.
