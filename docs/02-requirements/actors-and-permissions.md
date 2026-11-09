# Actors, permissions, and segregation

Permissions are granted through attributes (action, product, amount band, portfolio, state, and validity), not by role name alone. Monetary bands and delegations are approved governance parameters, not universal values defined here.

| Actor | May | Restrictions / controls |
|---|---|---|
| Customer/representative | View own application/loan, provide documents, accept terms, pay/prepay, complain. | Cannot see another party's file or change rates, balances, or internal decisions. Validate current corporate authority. |
| Adviser | Create file/application, attach documents, request assessment. | Cannot assess/approve own origination, disburse, or alter a confirmed movement. |
| Analyst | Review evidence, request data, assess/recommend, propose terms. | Cannot authorize outside delegation or self-approve exceptions. |
| Supervisor/manager | Approve/reject/condition within limit; escalate exceptions. | Cannot exceed authority, omit rationale, or serve as second approver on own operation. |
| Operations | Formalize, generate schedule, record receipt and reconciliation. | Cannot change accepted terms without amendment or create and approve own financial adjustment. |
| Disbursement staff | Send/confirm an already authorized order. | Cannot change beneficiary, amount, or account without review; cannot approve the loan. |
| Collections staff | Contact, record promises/disputes, take authorized actions. | Cannot forgive debt, vary rate, or enforce collateral without approval/legal process. |
| Auditor | Read files, logs, decisions, movements, and reports; export when authorized. | Cannot modify records or disclose data outside purpose. |
| Administrator | Manage identities, technical catalogs, and delegated parameters with controls. | No unrestricted functional access; administration does not grant financial authority. |

## Authorization rules

- **INV-001:** the person preparing a disbursement, manual prepayment, reversal, write-off, or terms change is not its sole approver/executor.
- Dual approval is required for exceptions, manual payment/disbursement above configured bands, beneficiary changes after approval, reversal of confirmed movements, forgiveness/adjustments, refinancing, release of real collateral, and policy overrides.
- The second approver independently reviews the data and rationale; approval is not a ceremonial signature.
- A conflict involving a related customer, application author, or personal interest blocks the decision until reassignment.
- Access to financial data and documents is limited to need-to-know. Auditor, support, or administrator status does not automatically grant content access.
- Role revocation invalidates pending operations before confirmation; delegation changes have an effective date and owner.
