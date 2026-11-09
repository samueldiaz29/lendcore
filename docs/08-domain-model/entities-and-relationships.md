# Entities and relevant data

| Entity | Identity / critical data | Invariants |
|---|---|---|
| Customer / PartyRole | individual/entity type, identifiers, status, relationship, authority and validity | INV-001; no merge without audit |
| Document | class, owner, issuer, issue/expiry, version, hash, review | Do not overwrite reviewed evidence; audit access |
| ProductVersion | validity, eligibility, currency, rate, basis, method, frequency, charges, limits | Frozen after contractual use |
| Application | customer, need, amount, term, version, consent, stage | Evaluation references exact snapshot |
| Evaluation / Decision | data, source, date, policy/model, reasons, decision-maker, authority | Reproducible; score is not decision |
| Contract | frozen terms, documents, acceptance, effectiveness | Material changes require new acceptance |
| Loan | principal/currency, value date, contract, state, separate delinquency attribute | Balances derived from movements |
| ScheduleVersion/Installment | method, rate, basis, dates, components, due state | History retains versions |
| Payment/Allocation | external references, amount, currency, dates, components | Idempotent; allocations sum to applied amount |
| Movement | type, signed amount, currency, value date, state, origin, correlation | Confirmed movement immutable; linked compensations |
| Guarantee | type, asset/guarantor, value, valuation, lien, perfection, release | Only perfected collateral counts for coverage |
| CollectionCase | delinquency, stage, owner, contact, promise, dispute | Does not change contract/balance by itself |
| RateFixing | index, source, observation date, value, margin, effective date | No retroactivity |
| FXQuote | pair, rate, provider, timestamp, purpose, amount | Conversion is reconstructible |

## INV — Domain invariants

- **INV-001:** every confirmed movement is retained and immutable.
- **INV-002:** an idempotency key identifies one effective operation per source.
- **INV-003:** confirmed payment allocations cannot exceed receipt; excess is separate.
- **INV-004:** balances and interest are grouped by contractual currency; no conversion without explicit FX.
- **INV-005:** reconstructible balance = disbursement events + authorized adjustments − principal applied + compensating reversals, separated by currency/effective date.
- **INV-006:** default interest is not added to principal to generate further interest in the initial scope.
