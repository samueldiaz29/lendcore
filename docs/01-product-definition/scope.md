# Scope and releases

## MVP — coherent end-to-end credit flow

Includes individual and legal-entity customers; a document file as an evidence repository (without making a final regulatory-sufficiency determination); limited-complexity personal and business loans; application; simulated or adapter-based bureau/income data; hybrid credit assessment; configurable approval bands with maker-checker controls; contract/summary sheet as documents; single-tranche disbursement; fixed rates; PEN/USD; French and German amortization; manual/imported simulated payments; allocation; prepayment; simple delinquency; basic collections; recorded personal and real collateral; operational ledger; audit trail; and essential reports.

## Version 1

Adds vehicle and mortgage lending with specialized milestones and collateral; variable rates with index and review windows; business disbursements in tranches; weekly/15-day schedules, principal-only grace, controlled rescheduling/refinancing, automated reconciliation, collection strategies, customer portal, and additional live integrations.

## Future

Full-payment grace with capitalized interest only after product-specific legal and financial analysis; syndicated, leasing and revolving facilities; reverse mortgages; securitization; production ML scoring; insolvency restructuring; integrated court enforcement; and automated write-off/prudential reporting.

## Explicit exclusions

LendCore is not a core banking system, general ledger, interbank payment rail, official SBS reporting repository, complete AML/CFT system, digital signature certification authority, bureau, appraiser, or court case-management system. Connectors exchange information with those systems and must be reconciled with the system of record.

## Product-family distinctions

| Family | Initial release | Distinction that must remain explicit |
|---|---|---|
| Personal | MVP | Disposable income, indebtedness, disclosed insurance/charges, and possible BCRP rate cap according to category. |
| Business | Limited MVP; tranches in V1 | Financial statements, cash flow, economic group, legal representatives, collateral, covenants, and use of proceeds. |
| Vehicle | V1 | Vehicle identification, invoice, payment to seller, lien/security interest, and insurance where required by product. |
| Mortgage | V1 | Valuation/appraiser, property and registry records/encumbrances, legal review, registration milestones, insurance/charges, and formal release. |

The MVP must not treat a secured loan as approved solely because of LTV, or use the same income evidence for an individual and a business.
