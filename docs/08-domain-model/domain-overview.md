# Conceptual domain model

## Aggregates and relationships

- **Customer** has 1:N **PartyRole** (borrower, representative, guarantor), 1:N **Consent**, and 1:N **Document**.
- **CreditApplication** belongs to a customer/group and references ProductVersion, TermsQuote, EvidenceSnapshot, Evaluation, and approval decisions.
- **CreditEvaluation** freezes sources/data, model, and outcome. **ApprovalDecision** stores authority, limits, conditions, and validity.
- **Contract** contains acceptance and financial snapshot; it originates one **Loan** and optionally several **DisbursementTranches**.
- **Loan** links to **ScheduleVersion**, **Installment**, **GuaranteeLink**, **RateVersion**, and financial events.
- **PaymentInstruction** may result in **PaymentReceipt**, **Allocation**, and **FinancialMovement**; an external receipt is not an applied movement until confirmed.
- **FinancialMovement** is immutable and tied to a logical event; **ReversalMovement** compensates it without replacing it.
- **CollectionCase** is associated with a loan/obligation and stores contacts, promises, and disputes.
- **Guarantee** links to one or more obligations with coverage/currency/priority and perfection/release workflow.
- **RateFixing** stores index, source, observation date, value, margin, and effective date.
- **FXQuote** stores currency pair, rate, provider, timestamp, purpose, and amount.

Entity IDs are stable; do not unnecessarily replicate personal data into reports. Monetary attributes are `(amount, currency)`; never store an amount without currency. Keep contract date, value date, accounting date, and receipt timestamp distinct.
