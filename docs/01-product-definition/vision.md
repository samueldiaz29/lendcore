# Product vision

**DP-001 — Specialized lending platform.** LendCore is a platform for originating and managing the full credit lifecycle for a Peruvian commercial bank. It supports PEN and USD, individuals and legal entities, and treats an external core banking system as the authority for accounts and settlement where integrated.

## Problem and value

Fragmented applications, analyses, contracts, schedules, disbursements, payments, and collections increase the risk of inconsistent decisions and make it difficult to reconstruct why a balance changed. LendCore provides a single customer file, traceable human decisions, reproducible contractual calculations, an immutable record of operations, and end-to-end follow-up.

## Principles

1. Repayment capacity comes first; collateral mitigates loss and does not replace capacity (RN-021).
2. Every financial term is versioned and linked to a contract/loan.
3. The engine recommends; authorized staff decide whenever policy requires human review.
4. Every amount retains its currency, precision, source, and valuation date; currencies are never implicitly added.
5. A confirmed financial operation is corrected through a compensating entry, never deleted.
6. Compliance requires configuration, organizational controls, and legal review; this document does not certify compliance.

## Product success (proposed objectives)

A complete file is available before a decision; a schedule can be reproduced from frozen parameters; a confirmed event is never applied twice; every balance can be traced to the operational ledger; and alerts are visible for due dates, delinquency, collateral, and rate changes. Quantitative service objectives are in the NFR catalog.
