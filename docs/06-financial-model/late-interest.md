# Simple default interest

Design formula: `M = V * r_m * d / D` per segment, where V is the permitted unpaid overdue base, `r_m` the annual default rate, d elapsed days, and D the day-count divisor. When a payment reduces V, split intervals and calculate on updated balance. Do not capitalize M or overdue compensatory interest; do not charge interest on interest (INV-006). Validate cap/base under applicable regulation and contract by category.

Example: permitted default base PEN 1,000; 10% simple annual rate; 18 days; ACT/360: `1,000*.10*18/360=5.00`. If 400 is paid on day 10: first segment 10 days `2.777777...`, then 600 for 8 days `1.333333...`, total `4.111111...` → 4.11 if rounding is defined at liquidation. Rounding each segment to cents first may differ; policy sets the liquidation rounding point unless contract/law requires periodic posting.

Compensatory and default interest may accrue concurrently only on legally permitted bases and within limits; exact base remains subject to legal validation. Do not add default interest to principal for the next period.
