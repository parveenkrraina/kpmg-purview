# KPMG Purview Tax Data DLP Demo Repository

This repository contains a complete sample pack for demonstrating Microsoft Purview Information Protection and Data Loss Prevention for tax data scenarios.

The core objective is to allow employee personal tax sharing where appropriate, while preventing client and KPMG business tax data from being sent to unmanaged destinations.

## Repository Layout

- [README.md](README.md): Main documentation and usage guide.
- [DLP import Export.md](DLP%20import%20Export.md): PowerShell-oriented notes for DLP policy import/export and operations.
- [Tax Data Implementation Guide and Samples](Tax%20Data%20Implementation%20Guide%20and%20Samples): Full workshop content, test files, and implementation guide.

## Implementation Guide

- [KPMG Tax Data DLP Implementation.pdf](Tax%20Data%20Implementation%20Guide%20and%20Samples/KPMG%20Tax%20Data%20DLP%20Implementation.pdf)

The PDF is the end-to-end workshop playbook that covers prerequisites, label design, custom SIT and EDM creation, Exchange DLP policy setup, exception handling, validation, monitoring, troubleshooting, and staged rollout.

## Sample Pack Inventory

### Policy and Reference Data

| File | What it Contains | Usage |
| --- | --- | --- |
| [Purview_Label_Taxonomy.csv](Tax%20Data%20Implementation%20Guide%20and%20Samples/Purview_Label_Taxonomy.csv) | Label names, scope, protection guidance, and demo purpose for Personal, Internal, and Client tax data | Define or validate sensitivity label taxonomy |
| [EDM_Client_Tax_Records.csv](Tax%20Data%20Implementation%20Guide%20and%20Samples/EDM_Client_Tax_Records.csv) | Sample client records with ClientTaxID and EngagementID | Build and test EDM classifier matching |
| [Personal_Email_Domains.csv](Tax%20Data%20Implementation%20Guide%20and%20Samples/Personal_Email_Domains.csv) | Personal webmail domains (gmail, outlook, yahoo, etc.) | Destination conditions for DLP block/warn controls |
| [Approved_Secure_Domains.csv](Tax%20Data%20Implementation%20Guide%20and%20Samples/Approved_Secure_Domains.csv) | Approved exception domains | Controlled exception rules with encryption/audit |
| [DLP_Test_Matrix.csv](Tax%20Data%20Implementation%20Guide%20and%20Samples/DLP_Test_Matrix.csv) | TC01-TC05 test plan with expected outcomes and logic | Validate policy behavior after deployment |

### Email Body Test Content

| File | Scenario Simulated | Expected Behavior |
| --- | --- | --- |
| [Email_Body_Employee_Personal_Tax_Allowed.txt](Tax%20Data%20Implementation%20Guide%20and%20Samples/Email_Body_Employee_Personal_Tax_Allowed.txt) | Employee personal tax context | Allow or allow with audit/justification |
| [Email_Body_Client_Tax_Blocked.txt](Tax%20Data%20Implementation%20Guide%20and%20Samples/Email_Body_Client_Tax_Blocked.txt) | Client identifiers and engagement data | Block when sent to personal domains |
| [Email_Body_Generic_Tax_Warn.txt](Tax%20Data%20Implementation%20Guide%20and%20Samples/Email_Body_Generic_Tax_Warn.txt) | Generic tax terms without explicit client match | Warn with justification flow |

### Document Attachment Test Content

| File | Scenario Simulated | Typical Test Outcome |
| --- | --- | --- |
| [Employee_Personal_Tax_Allowed.docx](Tax%20Data%20Implementation%20Guide%20and%20Samples/Employee_Personal_Tax_Allowed.docx) | Employee personal tax document | Allowed (with policy logging/justification as configured) |
| [KPMG_Internal_Tax_Data.docx](Tax%20Data%20Implementation%20Guide%20and%20Samples/KPMG_Internal_Tax_Data.docx) | Internal KPMG tax/business content | Warn or restrict based on policy design |
| [Client_Tax_Data_Blocked_EDM.docx](Tax%20Data%20Implementation%20Guide%20and%20Samples/Client_Tax_Data_Blocked_EDM.docx) | EDM-match client tax identifiers | Block to personal destinations |
| [Client_Tax_Data_Labeled_Blocked.docx](Tax%20Data%20Implementation%20Guide%20and%20Samples/Client_Tax_Data_Labeled_Blocked.docx) | Highly Confidential - Client Tax Data labeled content | Block by label-based DLP rule |
| [Generic_Tax_Warn.docx](Tax%20Data%20Implementation%20Guide%20and%20Samples/Generic_Tax_Warn.docx) | Generic tax wording without client EDM signals | Warn/justify based on policy threshold |

## End-to-End Workshop Flow

1. Prepare demo tenant prerequisites and role access.
2. Create demo users, groups, and optional SharePoint locations.
3. Create and publish sensitivity labels.
4. Create custom SIT for KPMG tax identifiers.
5. Configure EDM classifier from the client records dataset.
6. Apply auto-labeling for client tax content.
7. Build Exchange DLP rules for block, warn, and exception handling.
8. Execute the test matrix and verify results in alerts/activity/audit.
9. Move from audit mode to staged enforcement.

## Suggested Usage Sequence

1. Start with [KPMG Tax Data DLP Implementation.pdf](Tax%20Data%20Implementation%20Guide%20and%20Samples/KPMG%20Tax%20Data%20DLP%20Implementation.pdf).
2. Use [Purview_Label_Taxonomy.csv](Tax%20Data%20Implementation%20Guide%20and%20Samples/Purview_Label_Taxonomy.csv) and [EDM_Client_Tax_Records.csv](Tax%20Data%20Implementation%20Guide%20and%20Samples/EDM_Client_Tax_Records.csv) to configure classifiers and labels.
3. Apply recipient controls using [Personal_Email_Domains.csv](Tax%20Data%20Implementation%20Guide%20and%20Samples/Personal_Email_Domains.csv) and [Approved_Secure_Domains.csv](Tax%20Data%20Implementation%20Guide%20and%20Samples/Approved_Secure_Domains.csv).
4. Validate with [DLP_Test_Matrix.csv](Tax%20Data%20Implementation%20Guide%20and%20Samples/DLP_Test_Matrix.csv) plus the DOCX/TXT sample payloads.
5. Use [DLP import Export.md](DLP%20import%20Export.md) for PowerShell-based policy operations.

## Important Notes

- All sample records are for demo/training use.
- Run these steps in a lab or pilot tenant before production rollout.
- Keep exception rules narrow and auditable.