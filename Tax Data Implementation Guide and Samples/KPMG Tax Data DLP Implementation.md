## Quick Navigation

- [1. Demo Architecture Summary](#1-demo-architecture-summary)
- [2. What You Need Before Starting](#2-what-you-need-before-starting)
- [3. Sample Files Included](#3-sample-files-included)
- [4. Phase A - Create Demo Users and Groups](#4-phase-a---create-demo-users-and-groups)
- [5. Phase B - Create SharePoint Demo Locations](#5-phase-b---create-sharepoint-demo-locations)
- [6. Phase C - Create Sensitivity Labels](#6-phase-c---create-sensitivity-labels)
- [7. Phase D - Publish Labels with a Label Policy](#7-phase-d---publish-labels-with-a-label-policy)
- [8. Phase E - Create Custom Sensitive Information Type](#8-phase-e---create-custom-sensitive-information-type)
- [9. Phase F - Create EDM Classifier for Exact Client Tax Records](#9-phase-f---create-edm-classifier-for-exact-client-tax-records)
- [10. Phase G - Create Auto-labeling Policy for Client Tax Data](#10-phase-g---create-auto-labeling-policy-for-client-tax-data)
- [11. Phase H - Create Exchange DLP Policy](#11-phase-h---create-exchange-dlp-policy)
- [12. Phase I - Configure Exceptions Safely](#12-phase-i---configure-exceptions-safely)
- [13. Phase J - Optional Endpoint DLP Extension](#13-phase-j---optional-endpoint-dlp-extension)
- [14. Phase K - Test Execution](#14-phase-k---test-execution)
- [15. Phase L - Monitoring and Investigation](#15-phase-l---monitoring-and-investigation)

# KPMG Tax Data DLP Workshop Guide
## Self -paced Microsoft Purview implementation workshop for participants
Created by Parveen KR
Use this guide to complete the configuration, validation, and testing activities independently in a demo or lab environment.
KPMG Tax Data DLP Implementation Guide
A self-paced implementation guide created by Parveen KR for participants to complete the Microsoft Purview activities on their own using the included sample files

Purpose: This demo is designed to let employees email their own personal tax documents to a personal account, while ensuring that
KPMG, client, or business tax data is not sent to a personal mailbox or any other unmanaged destination.

Important: A single broad rule to "block tax data" will not work for this scenario. This demo intentionally combines classification, sensitivity labels, EDM, contextual DLP, destination checks, exceptions, and monitoring, because each control plays a different role and no one control solves the problem on its own.

#### How to Use This Guide
This guide is intended for individual participants to complete the setup, configuration, testing, and validation activities independently.
Author: Parveen KR
How to proceed: Follow each phase in sequence, complete the validation checks before moving to the next section, and use the sample files exactly as listed in the guide.
Important: Use only a demo, lab, or pilot environment for these activities. Do not apply these steps directly in a production environment without proper review and approval.
### 1. Demo Architecture Summary
| Layer | Purpose | Demo Object |
|---|---|---|
| Classification | Detect tax/business/client signals | Custom SIT + EDM |
| Labeling | Separate personal/internal/client data | Personal - Employee Tax; Confidential - KPMG Internal Tax; Highly Confidential - Client Tax Data |
| DLP | Control movement to personal email | Exchange DLP rule set |
| Exceptions | Allow legitimate personal/approved cases | Personal tax label, approved domains, approved users |
| Monitoring | Validate policy outcome | DLP Alerts, Activity Explorer, Audit |

Participant checkpoint: Confirm that you understand the role of each layer in the demo architecture before proceeding.

### 2. What You Need Before Starting
| Requirement | Minimum for Demo | How to Check |
|---|---|---|
| Microsoft 365 tenant | Training/lab tenant with Microsoft Purview access | Open https://purview.microsoft.com |
| Admin roles | Compliance Administrator, Security Administrator, Exchange Administrator or equivalent lab admin | Microsoft 365 admin center > Roles |
| Test internal user | A mailbox-enabled user such as joni@tenant.onmicrosoft.com | Microsoft 365 admin center > Users |
| External personal email | One real external address, such as a trainer Gmail/Outlook account | Use for test sends only |
| Purview DLP availability | DLP solution accessible in Purview | Purview portal > Solutions > Data Loss Prevention |
| Information Protection availability | Sensitivity labels and classifiers accessible | Purview portal > Solutions > Information Protection |
| Optional endpoint DLP | Windows test machine onboarded if endpoint scenario is demonstrated | Purview > Settings > Device onboarding |

No assumptions: If anything in this list — such as a role, label, SIT, EDM classifier, policy, group, site, or test file — is not already available, set it up first using the steps below. Do not try to test around missing pieces.

Participant checkpoint: Verify that your tenant, roles, test accounts, and Purview prerequisites are ready before starting the setup
phases.
### 3. Sample Files Included
| File | Purpose | Expected Result |
|---|---|---|
| EDM_Client_Tax_Records.csv | Raw client/business tax records for EDM setup | Used to create precise client tax detection |
| Employee_Personal_Tax_Allowed.docx | Employee-owned personal tax scenario | Allowed or audit-only |
| Client_Tax_Data_Blocked_EDM.docx | Exact client tax ID and engagement ID | Blocked to personal email |
| Generic_Tax_Warn.docx | Generic tax keywords without client identifiers | Warn with justification |
| Client_Tax_Data_Labeled_Blocked.docx | Manually label as Client Tax Data | Blocked to personal email |
| KPMG_Internal_Tax_Data.docx | Internal KPMG business tax content | Warn or restrict based on policy |
| Email_Body_*.txt | Copy/paste message bodies for Exchange DLP tests | Used for email tests |
| Personal_Email_Domains.csv | Personal domains for policy design | High-risk personal destinations |
| Approved_Secure_Domains.csv | Approved exception domains | Allowed only by exception |
| DLP_Test_Matrix.csv | Validation plan | Run after policy creation |

Participant checkpoint: Make sure all sample files are available and that you understand the expected result for each file.
### 4. Phase A - Create Demo Users and Groups
1. Open Microsoft 365 admin center: https://admin.microsoft.com.
2. Create or identify one internal test user. Example: Joni Sherman or TaxDemo User.
3. Ensure the test user has an Exchange Online mailbox and can send mail.
4. Create a mail-enabled security group named KPMG Tax Practice Demo Users.
5. Add the test user to KPMG Tax Practice Demo Users.
6. Create a security group named KPMG Client Tax Data Approved Senders for exception testing.
7. Create or identify a compliance/security mailbox for DLP alerts, such as compliance.alerts@tenant.

Participant guidance: Keep production groups completely out of this setup. For your first run-through, use only demo, lab, or pilot
groups.

Participant checkpoint: Confirm that your demo user, groups, and alert mailbox are created and ready for use.
### 5. Phase B - Create SharePoint Demo Locations
1. Open SharePoint admin center.
2. Create a site named KPMG Tax Data Demo or use an existing training site.
3. Create three document libraries or folders: Employee Personal Tax, KPMG Internal Tax, Client Tax Data.
4. Upload Employee_Personal_Tax_Allowed.docx to Employee Personal Tax.
5. Upload KPMG_Internal_Tax_Data.docx to KPMG Internal Tax.
6. Upload Client_Tax_Data_Blocked_EDM.docx and Client_Tax_Data_Labeled_Blocked.docx to Client Tax Data.
7. Confirm the test user has access to all three areas for demo purposes.
Participant checkpoint: Verify that the SharePoint site, libraries or folders, and file permissions are set correctly.
### 6. Phase C - Create Sensitivity Labels
| Label | Scope | Configuration |
|---|---|---|
| Personal - Employee Tax | Files and emails | No encryption for demo; footer: Personal Tax Information; use for employee-owned tax data |
| Confidential - KPMG Internal Tax | Files and emails | Encryption optional; header/footer: KPMG Internal Tax; restrict to internal users if available |
| Highly Confidential - Client Tax Data | Files and emails | Encrypt; restrict to KPMG Tax Practice Demo Users; watermark: Client Tax Data |

1. Open https://purview.microsoft.com.
2. Go to Solutions > Information Protection > Sensitivity labels.
3. Select Create a label.
4. Create the first label: Personal - Employee Tax. Add description for users: Use only for your own personal tax records, not client or
KPMG business data.
5. Set scope to Files and emails. Add footer marking if desired. Do not enable encryption for the first demo iteration.
6. Repeat for Confidential - KPMG Internal Tax. Use a description that makes it clear this is for internal KPMG business tax data.
7. Repeat for Highly Confidential - Client Tax Data. Enable encryption if your demo tenant supports it. Restrict access to KPMG Tax
Practice Demo Users or a pilot group.
8. Review and create each label.
Participant checkpoint: Confirm that all three sensitivity labels have been created with the intended scope and settings.

### 7. Phase D - Publish Labels with a Label Policy
1. In Purview, go to Information Protection > Publishing policies.
2. Select Publish label.
3. Choose the three labels created in Phase C.
4. Publish to KPMG Tax Practice Demo Users or your test user.
5. Set default label to General/Internal if available. If no default label exists, leave default unconfigured for first run.
6. Enable users to provide justification when removing or downgrading labels from Confidential or Highly Confidential labels.
7. Name the policy KPMG Tax Data Label Publishing Policy.
8. Create the policy and wait for propagation. In many tenants, label availability can take time in Office apps.
Validation: Sign in as the test user in Word or Outlook and confirm that the labels are visible. If they do not appear right away, allow
some time for propagation, restart Office, and then recheck the label policy target group along with the user's licensing and roles.

Participant checkpoint: Check that the labels are visible to the test user in Word or Outlook before moving on.
### 8. Phase E - Create Custom Sensitive Information Type
Objective: The goal here is to detect KPMG and client tax business identifiers together with the surrounding context. Treat this SIT as a medium-confidence signal — useful on its own, but especially valuable until EDM is fully in place.

| Component | Value |
|---|---|
| Name | KPMG Business Tax Identifier |
| Primary pattern | KPMG-TAX-\d{6} OR ENG-TAX-\d{6} |
| Supporting keywords | client, tax advisory, client tax return, engagement, corporate tax, financial report, VAT, GST |
| Medium confidence | Primary pattern + one supporting keyword within proximity |
| High confidence | Primary pattern + two supporting keywords or both ClientTaxID and EngagementID patterns |

1. Go to Information Protection > Classifiers > Sensitive info types.
2. Select Create sensitive info type.
3. Name: KPMG Business Tax Identifier.
4. Create a pattern with a regular expression primary element. Use sample regex KPMG-TAX-\d{6}.
5. Add a second primary pattern or additional regex for ENG-TAX-\d{6}.
6. Add supporting elements/keywords: client, tax advisory, client tax return, engagement, corporate tax, financial report, VAT, GST.
7. Set proximity so supporting words must appear near the primary pattern. Use a practical value such as 300 characters for demo.
8. Create low, medium, and high confidence patterns if your tenant wizard allows multiple confidence levels.
9. Save the SIT.
10. Use Test and upload Client_Tax_Data_Blocked_EDM.docx. Confirm a match is detected.

11. Upload Employee_Personal_Tax_Allowed.docx. Confirm it does not match this business/client SIT.
Participant checkpoint: Test the custom sensitive information type and confirm that only the expected business and client content
is detected.
### 9. Phase F - Create EDM Classifier for Exact Client Tax Records
Objective: The aim is to match only the known client and business tax records from the EDM sample dataset, so that an employee’s own tax document is not incorrectly caught by the block rule.

1. Open the included EDM_Client_Tax_Records.csv and review the sample rows.
2. Confirm the file contains only fictional client/business tax records. Do not include employee personal tax data.
3. In Purview, go to Information Protection > Classifiers > EDM classifiers.
4. If available, keep the New EDM experience enabled for easier setup.
5. Create a new EDM classifier or EDM SIT based on your tenant experience.
6. Upload or define the schema using columns: ClientID, ClientName, ClientTaxID, EngagementID, ClientCountry, DataOwner,
Sensitivity.
7. Choose ClientTaxID as the primary sensitive field. Add EngagementID and ClientName as supporting fields if the wizard supports
mapping.
8. Hash and upload the source data following the Purview wizard or EDM upload tool instructions for your tenant.
9. Name the EDM classifier KPMG Client Tax EDM.
10. After publication/indexing, test the EDM classifier using Client_Tax_Data_Blocked_EDM.docx.
11. Test Employee_Personal_Tax_Allowed.docx and confirm it does not match EDM.
What you should see: Client_Tax_Data_Blocked_EDM.docx should match because it contains KPMG-TAX-458921 and ENG-TAX-100001, both of which exist in the EDM dataset. Employee_Personal_Tax_Allowed.docx should not return an EDM match.

Participant checkpoint: Confirm that the EDM classifier is published and returns a match only for the intended client tax records.
### 10. Phase G - Create Auto-labeling Policy for Client Tax Data
1. Go to Information Protection > Auto-labeling policies.
2. Select Create auto-labeling policy.
3. Choose custom policy or sensitive info type-based policy depending on wizard options.
4. Name: Auto-label Client Tax Data.
5. Locations: Exchange, SharePoint, and OneDrive for demo. Avoid broad production targeting initially.
6. Condition: content contains KPMG Client Tax EDM OR KPMG Business Tax Identifier at medium/high confidence.
7. Apply label: Highly Confidential - Client Tax Data.

8. Run in simulation mode first. Do not turn on automatic enforcement immediately.
9. Review simulated matches. Confirm only client/business tax documents are matched.
10. After tuning, enable the policy only for the demo location/pilot group.
Participant checkpoint: Review the simulation results and make sure the auto-labeling policy targets only the intended content.
### 11. Phase H - Create Exchange DLP Policy
Objective: The goal is to stop client and business tax data from being sent to personal email, while still allowing employees to send their own tax documents, with audit and justification built into the process.

1. Go to Solutions > Data Loss Prevention > Policies.
2. Select Create policy > Custom policy.
3. Name: KPMG - Block Client Tax Data to Personal Email.
4. Locations: Exchange email. Add Devices later only after endpoint prerequisites are ready.
5. Scope: start with KPMG Tax Practice Demo Users or the test user.
6. Create Rule 1: Block labeled client tax data to personal email.
7. Condition: content contains sensitivity label Highly Confidential - Client Tax Data.
8. Additional condition: recipient is outside the organization or recipient domain is one of the personal email domains from
Personal_Email_Domains.csv.
9. Action: block the email, notify user, send incident report to compliance/security mailbox, and create alert.
10. Create Rule 2: Block EDM client tax records to personal email.
11. Condition: content contains KPMG Client Tax EDM.
12. Additional condition: recipient is outside organization or personal email domain.
13. Action: block, notify user, create high severity alert.
14. Create Rule 3: Warn for generic tax information.
15. Condition: content contains generic tax keywords or built-in tax-related SITs if available, but does not contain KPMG Client Tax EDM
and is not labeled Highly Confidential - Client Tax Data.
16. Action: allow override with business justification, show policy tip, audit event.
17. Set policy mode to Test first. Then move to Test with notifications. Then enforce only high-confidence Rule 1 and Rule 2.
Participant checkpoint: Confirm that the Exchange DLP rules are created in the correct order and are running in the intended policy
mode.
### 12. Phase I - Configure Exceptions Safely
| Exception | Recommended Configuration | Risk Warning |
|---|---|---|
| Employee personal tax | Allow if label = Personal - Employee Tax AND no EDM/client SIT match identifier is present | Do not allow if EDM/client tax |
| Approved secure domains | Allow for domains in Approved_Secure_Domains.csv | Require encryption and audit |
| Approved senders | Allow only KPMG Client Tax Data Approved Senders | Avoid broad group exceptions |

1. In the DLP rule editor, add exceptions only after core block rules work.
2. For personal tax: exception should require Personal - Employee Tax label AND no match for KPMG Client Tax EDM.
3. For approved domains: exception should require recipient domain is approved AND message is encrypted if your policy supports it.
4. For approved senders: exception should be limited to a small pilot group and audited.
5. Never create an exception such as all tax users can send externally.
Participant checkpoint: Review each exception carefully and confirm that no broad or unsafe bypass has been introduced.
### 13. Phase J - Optional Endpoint DLP Extension
1. Confirm endpoint DLP prerequisites and device onboarding are complete before demonstrating endpoint controls.
2. Go to Purview > Settings > Device onboarding and confirm the test device is listed.
3. Edit or create a DLP policy that includes Devices location.
4. Conditions: file has label Highly Confidential - Client Tax Data OR contains KPMG Client Tax EDM.
5. Actions: block upload to personal webmail, block copy to USB, block copy to clipboard, audit file copy/rename/print activities as
needed.
6. Test from the onboarded Windows device only. Do not assume endpoint DLP is active until the device appears in Purview.
Participant checkpoint: If you are testing endpoint DLP, verify that the device is onboarded and visible in Purview before continuing.
### 14. Phase K - Test Execution
| Test | Steps | Expected Result |
|---|---|---|
| TC01 Allowed Personal Tax | Attach Employee_Personal_Tax_Allowed.docx to an email to personal Gmail. Use Personal - Employee Tax label if available. | Allow or allow with audit/justification. No EDM block. |
| TC02 Block EDM Client Tax | Attach Client_Tax_Data_Blocked_EDM.docx to personal Gmail. | Blocked by EDM DLP rule. Alert created. |
| TC03 Warn Generic Tax | Attach Generic_Tax_Warn.docx to personal Gmail. | Warn with justification; do not hard block unless policy is stricter. |
| TC04 Block Labeled Client Tax | Apply Highly Confidential - Client Tax Data to Client_Tax_Data_Labeled_Blocked.docx, then email to personal Outlook.com. | Blocked by label-based DLP rule. |
| TC05 Approved Domain Exception | Send Client_Tax_Data_Blocked_EDM.docx to approved secure domain sample if configured. | Allow only if exception configured and audited; otherwise block. |

Participant checkpoint: Complete the test matrix and confirm that the allowed, warning, and block outcomes match the guide.
### 15. Phase L - Monitoring and Investigation
1. Open Purview portal > Data Loss Prevention > Alerts.

2. Review alert details: matched rule, sender, recipient, sensitive information type, confidence, and action taken.
3. Open Activity Explorer.
4. Filter by user, activity type, DLP rule match, label, location, or time range.
5. Confirm test events appear for blocked and warned cases.
6. Review Audit if enabled: label changes, message send attempts, policy overrides, file access, and downloads.
7. Capture screenshots for class discussion: allowed, warned, blocked, and investigated outcomes.
Participant checkpoint: Review alerts, Activity Explorer, and audit details to confirm that your test actions were recorded correctly.
16. Troubleshooting
| Issue | Likely Cause | Fix |
|---|---|---|
| Labels do not appear in Office | Policy not propagated or user not in label policy scope | Wait, restart Office, verify target group and licensing |
| SIT does not match | Regex/supporting evidence/proximity issue | Test with exact sample text; simplify pattern first |
| EDM does not match | Data not uploaded, hashing/indexing pending, wrong field selected | Verify EDM source values, wait for indexing, retest from EDM classifier |
| DLP does not trigger | Policy in wrong mode, wrong location, user out of scope | Check policy mode, Exchange location, user scope, recipient condition |
| Personal tax document is blocked | Generic rule too aggressive | Add exception requiring no EDM match and Personal - Employee Tax label |
| Client tax document allowed | Missing EDM/label condition or recipient condition | Test SIT/EDM independently and verify personal domain condition |

Participant checkpoint: If any result does not match the guide, use the troubleshooting table to isolate the issue before moving on.
17. Rollout Strategy for Production-Like Environments
| Stage | Mode | Goal |
|---|---|---|
| Stage 1 | Audit only | Understand matches and false positives |
| Stage 2 | Warn with justification | Educate users and collect business context |
| Stage 3 | Block high-confidence EDM and Client Tax label | Protect exact client/business tax data |
| Stage 4 | Extend to endpoint and SaaS | Control browser, USB, clipboard, and cloud exfiltration |
| Stage 5 | Operationalize monitoring | Integrate with SOC, Insider Risk, and governance reviews |

Participant checkpoint: Review the rollout stages and confirm that you understand how to move from audit to enforcement safely.
18. Participant Notes and Guidance
This scenario cannot be handled well with one broad DLP rule. If everything related to tax is blocked, employees may not be able to send their own personal returns. If everything related to tax is allowed, client data can leave the organization too easily. The purpose of this guide is to help you understand how Microsoft Purview uses context to make that distinction.
As you work through the steps, focus on the difference between employee-owned personal tax data and client or business tax data.
Personal tax documents may be allowed with proper auditing, while client or KPMG business tax content should be restricted from being sent to personal destinations.

This is why the design in this guide combines sensitivity labels, EDM, DLP, controlled exceptions, and monitoring. Each part has a specific role: labels identify and protect content, EDM detects exact client tax records, DLP controls movement to risky destinations, and Activity Explorer together with DLP alerts helps you validate and investigate outcomes.
Keep this principle in mind throughout the exercise: allow personal tax data when appropriate, prevent client and business tax data from leaving, and use context to tell the difference.
Final participant checkpoint: Confirm that you can explain the difference between personal tax data and protected client or business tax data, and how Purview uses labels, EDM, DLP, exceptions, and monitoring together.
