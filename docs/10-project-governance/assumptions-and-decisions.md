# Decisions, assumptions, and open items

## User-approved decisions

- **DP-010:** Peru; simulated commercial bank; individuals/legal entities; PEN/USD; personal/business segments.
- **DP-011:** personal, business, vehicle, and mortgage families; differentiated and released in phases.
- **DP-012:** hybrid risk engine; recommendation does not replace human authority where required.
- **DP-013:** French/German amortization; fixed/variable, effective/nominal, compensatory/default rates; ACT/360, ACT/365, 30E/360; weekly, every 15 days, and monthly frequencies.
- **DP-014:** initial grace is principal-only; interest remains payable and is not automatically capitalized.
- **DP-015:** prepayment and installment advance are distinct; partial principal prepayment may reduce payment or term under contract; simple default interest without capitalization in initial design.
- **DP-016:** decimal precision, traceable ledger, no deletion, compensating movements, idempotency, and contractual currency.

## Proposed product-design decisions

- **DP-001:** specialized platform; does not replace core banking/general ledger.
- **DP-002:** MVP with one disbursement, fixed rates, limited personal/business loans; collateral workflow included; variable rates, tranches, and secured product families in V1.
- **DP-003:** 2-decimal settlement scale, at least 12-decimal internal precision, HALF_UP proposed, subject to accounting/legal review.
- **DP-004:** semi-open accrual period (include start/exclude end); final payment adjusts residual.
- **DP-005:** maker-checker for high-impact actions; delegated amounts are policy-configured, not fixed here.

## Open items that cannot responsibly be resolved from public sources alone

1. Legal counsel validates BCRP caps by customer, credit, and currency; adds the BCRP notice for the period beginning 1 Nov 2026 and confirms subsequent amendments.
2. Legal defines exact default-interest base, payment-allocation priority, charge/expense treatment, complaint deadlines, and product-specific contract exceptions.
3. Simulated bank defines risk appetite, capacity thresholds, score, approval bands, offer validity, document requirements, and delegation limits.
4. Finance/Accounting defines rounding point/mode by component, currencies, FX, entries, and general-ledger reconciliation.
5. Legal/Product decides whether “installment advance” interaction meets required distinction/disclosure and its contractual effects.
6. Compliance determines SBS rules by authorization/institutional scope, retention by document class, classification/provisions/reporting, and preservation duties.
7. Privacy defines legal bases, notices, databases, retention periods, providers, cross-border flows, and impact assessment criteria.
8. Legal/Valuation defines collateral-specific valuation, registry, and perfection requirements by asset and product.

These open items do not prevent conceptual technical analysis; they do prevent declaring a real regulated operation production-ready.
