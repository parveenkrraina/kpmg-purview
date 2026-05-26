# KPMG Purview Demo with Sample Data Files for Handling Tax Document for Employees, Internals and Clients

This repository contains the sample content for the KPMG Tax Data DLP workshop guide. The guide is a self-paced Microsoft Purview implementation exercise focused on separating employee personal tax data from KPMG and client tax data.

The workshop uses classification, sensitivity labels, EDM, contextual DLP, approved-domain exceptions, and monitoring to validate outcomes for allowed, warn, and blocked scenarios.

## Repository Contents

| File | Purpose |
| --- | --- |
| KPMG Tax Data DLP Implementation.pdf | End-to-end workshop guide with setup, policy design, validation, troubleshooting, and rollout stages. |
| `Approved_Secure_Domains.csv` | Sample approved domains that can be treated as trusted or exception-based destinations. |
| `Personal_Email_Domains.csv` | Common personal webmail domains used to test blocking, warning, or justification flows. |
| `EDM_Client_Tax_Records.csv` | Exact Data Match sample records for client tax identifiers and related metadata. |
| `Purview_Label_Taxonomy.csv` | Example sensitivity label taxonomy for employee tax, internal tax, and client tax data. |
| `DLP_Test_Matrix.csv` | Test cases describing expected DLP outcomes for personal, client, and generic tax scenarios. |
| `Email_Body_Client_Tax_Blocked.txt` | Sample email body containing client tax data that should trigger blocking. |
| `Email_Body_Employee_Personal_Tax_Allowed.txt` | Sample email body for personal tax data that should be allowed with audit or justification. |
| `Email_Body_Generic_Tax_Warn.txt` | Sample email body with generic tax language that should trigger a warning flow. |

## Purpose

The files in this repository are designed to support Purview demonstrations and policy testing around:

- Sensitivity labels for employee, internal, and client tax data.
- DLP behavior for personal email destinations versus approved domains.
- Exact Data Match scenarios using client tax identifiers.
- Email-based test cases that validate block, warn, and allow outcomes.

## Workshop Flow

The PDF guide walks through these major phases:

- Create demo users, groups, and alerting targets.
- Build SharePoint demo locations for employee, internal, and client tax files.
- Create and publish the three sensitivity labels.
- Define a custom sensitive information type for KPMG business tax identifiers.
- Configure an EDM classifier for exact client tax records.
- Create an auto-labeling policy for client tax data.
- Build Exchange DLP rules to block client tax data to personal email, warn on generic tax content, and allow safe personal tax scenarios.
- Add tightly scoped exceptions for approved domains or approved senders.
- Optionally extend the policy to endpoint DLP controls.
- Test, monitor, troubleshoot, and plan staged rollout from audit to enforcement.

## Suggested Usage

Use the CSV and text samples together when building or validating Purview policies. The test matrix maps the content types to the expected result so you can quickly confirm whether a policy configuration behaves as intended.

The sample email bodies and document names correspond to the test cases in the PDF, including personal tax allowed, generic tax warning, EDM client tax block, labeled client tax block, and approved-domain exception checks.