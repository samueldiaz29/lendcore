# Non-functional requirements

The following targets are **proposed design objectives** to validate during architecture and operations; they are legal obligations only where explicitly stated.

| ID | Verifiable requirement / evidence |
|---|---|
| RNF-001 | Individual authentication and session control; MFA for privileged staff and sensitive actions is a target aligned with applicable SBS channel controls. Evidence: authentication test matrix. |
| RNF-002 | Authorization by action, scope, amount, product, state, and validity; deny by default and segregate duties. Every sensitive denial produces an auditable event. |
| RNF-003 | Personal data has a purpose, applicable legal basis/consent, least-privilege access, correction/blocking, and retention controls; privacy impact assessment for credit profiling is a proposed control. |
| RNF-004 | Encrypt data in transit and at rest under institutional policy; segregate secrets; do not place authentication or sensitive financial data in logs. |
| RNF-005 | Business users cannot alter audit records: actor, synchronized timestamp, correlation, entity, action, before/after values or reference, rationale, and outcome. Evidence is exportable for audit. |
| RNF-006 | Confirmed movements are retained; balances are reconstructible by sequence, value date, currency, and reversals; reconciliation is automated or investigable. |
| RNF-007 | Idempotency uses source + unique key + operation; two concurrent requests for the same payment produce at most one application. Isolation/locking is a later technical decision. |
| RNF-008 | Proposed availability target: 99.5% monthly for internal functions, 24x7, excluding announced maintenance and third parties; measure with probes. This is a target, not a regulatory commitment. |
| RNF-009 | Proposed p95 target: ≤2 s for standard queries and ≤5 s for a simulation of up to 360 installments under an agreed load profile; excludes third-party outages. |
| RNF-010 | Proposed initial scale: 1 million loans and 10 million movements without loss of consistency; architecture confirms sizing. |
| RNF-011 | Integrations use timeouts, correlation, bounded backoff, status queries, and discrepancy queues; retries do not duplicate effects. |
| RNF-012 | Observability includes metrics, correlated logs, and alerts for calculation errors, duplicates, pending payments, reconciliation, and latency; avoid unnecessary PII in logs. |
| RNF-013 | Proposed RPO ≤15 minutes and RTO ≤4 hours; restoration exercise at least twice a year, subject to risk appetite. |
| RNF-014 | Interfaces document schema, versions, currency/scale, dates, error catalog, idempotency, and examples; incompatible changes require a version/plan. |
| RNF-015 | Monetary calculations use Java `BigDecimal` as the intended exact-decimal representation, with defined scale/rounding rules and regression cases. Binary float/double must not be the source of financial values. Evidence: reproduce approved financial fixtures, including residual and reversal cases. |
| RNF-016 | Store timestamps in UTC and display in America/Lima; contractual dates use local dates and a versioned calendar. Do not mix receipt timestamp with value date. |
| RNF-017 | Each financial release demonstrates regression for rates, schedules, allocation, default interest, prepayment, reversal, concurrency, and reconciliation. Coverage is evidence, not a universal percentage. |
| RNF-018 | Documents retain version, checksum, type, origin, permissions, and retention policy; access is audited. |
| RNF-019 | Retention/destruction/blocking policy reconciles prudential, contractual, AML, and personal-data obligations; Legal validates the exact term per category. |
| RNF-020 | Customer-facing terms, summary sheet, and calculations are understandable and deliverable by channel; comply with format and timing rules applicable to each current version. |

## Interpretation and verification

These requirements describe observable service qualities and controls, not a choice of infrastructure. RNF-008 through RNF-010 and RNF-013 contain proposed targets (availability, response time, initial volume, recovery point/objective); they are not approved service-level commitments. Product, Operations, Risk, and Finance must approve the measurement window, exclusions, load profile, and recovery scenario before they become release gates. Do not treat a target as satisfied because a design document repeats it: verify through measured evidence under a documented workload or exercise.

Security, privacy, audit, integrity, and calculation requirements apply to failure paths as well as successful paths. For example, a timeout after external bank confirmation must remain discoverable by correlation and must not trigger a duplicate monetary effect. A correction request may require blocking or correction of personal data while retention obligations may require preserving a restricted evidence record; Legal determines the case-specific retention treatment.

| Requirement group | Business reason | Suitable evidence |
|---|---|---|
| RNF-001..004, RNF-018..020 | Prevent unauthorized use, protect customer evidence, and support understandable service | Access-denial and privilege tests, data-flow/privacy review, document-access audit, channel disclosure review |
| RNF-005..007, RNF-011..012, RNF-015..017 | Protect monetary integrity and recoverability | Replay/concurrency tests, movement reconstruction, reconciliation cases, calculation fixtures, recovery exercise |
| RNF-008..010, RNF-013..014 | Set measurable service and interoperability expectations | Approved workload profile, probes, capacity test, restoration evidence, interface compatibility review |

Statutory requirements are catalogued separately in `07-compliance/`; applicability depends on institution, channel, customer, product, and current rule. Proposed controls such as encryption at rest, 99.5% availability, or MFA in a particular flow must not be labelled as a specific legal mandate unless the source and scope are established.
