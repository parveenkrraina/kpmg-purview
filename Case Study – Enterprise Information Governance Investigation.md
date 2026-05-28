## Quick Navigation

- [Task 1 – Data Discovery & Classification](#task-1-data-discovery-classification)
- [Task 2 – Encryption & Protection](#task-2-encryption-protection)
- [Task 3 – DLP Investigation](#task-3-dlp-investigation)
- [Task 4 – Endpoint Governance](#task-4-endpoint-governance)
- [Task 5 – Insider Risk Investigation](#task-5-insider-risk-investigation)
- [Task 6 – Adaptive Protection](#task-6-adaptive-protection)
- [Task 7 – Audit Investigation](#task-7-audit-investigation)
- [Task 8 – Content Search & eDiscovery](#task-8-content-search-ediscovery)
- [Task 9 – AI Governance](#task-9-ai-governance)

# Case Study – Enterprise Information Governance Investigation
## Microsoft Purview Integrated Governance Scenario
#### Background
A global consulting organization is advising a multinational financial and healthcare client during a confidential acquisition initiative called:
Project Falcon
The engagement involves:
- financial due diligence
- regulatory analysis
- legal review
- audit evidence collection
- AI-assisted reporting
- executive collaboration
The organization uses:
- Microsoft Teams
- Microsoft SharePoint
- Microsoft OneDrive
- Microsoft Outlook
- Microsoft Purview
The organization recently implemented:
- Sensitive Information Types (SIT)
- Exact Data Match (EDM)
- Sensitivity Labels
- Microsoft Purview Encryption
- Data Loss Prevention (DLP)
- Endpoint DLP
- Insider Risk Management
- Adaptive Protection

- Audit Premium
- Content Search
- eDiscovery
#### Business Scenario
A senior consultant working on Project Falcon submits resignation notice.
Within the next several days, the following activities are detected:
- Large SharePoint downloads
- Multiple after-hours access attempts
- Browser uploads from unmanaged browsers
- USB copy activity from corporate endpoint
- Local copies of financial spreadsheets
- External email forwarding attempts
- Teams file sharing outside approved channels
- AI prompt submissions into unmanaged AI tools
- Deletion of several local files after activity
The organization receives:
- DLP alerts
- Endpoint DLP alerts
- Elevated Insider Risk alerts
- Audit activity anomalies
Adaptive Protection automatically increases enforcement controls for the user.
Legal and compliance teams now require:
- investigation evidence
- activity timelines
- impacted data analysis
- defensible reporting
- governance improvement recommendations

#### Your Role
You are part of the:
Enterprise Governance & Investigation Team
Your responsibility is to:
- investigate the incident
- identify governance gaps
- determine data exposure
- evaluate Microsoft Purview controls
- recommend remediation actions

#### Investigation Objectives
Your team must determine:
WHAT HAPPENED?
WHAT DATA WAS INVOLVED?
WHO ACCESSED THE DATA?
WAS DATA EXFILTRATED?
WHICH CONTROLS WORKED?
WHAT GOVERNANCE IMPROVEMENTS ARE REQUIRED?

### Task 1 – Data Discovery & Classification
#### Objective
Identify how Microsoft Purview detects and classifies sensitive information.
#### Questions
1. Which Microsoft Purview technology would detect:
  - credit card numbers
  - bank account numbers
  - government IDs?
2. Which technology would help identify:

  - exact customer financial records
  - payroll IDs
  - internal account numbers?
3. Which technology would identify:
  - merger documents
  - audit reports
  - legal agreements
  - confidential strategy documents?
4. Which sensitivity labels would you recommend for:
  - executive reports
  - merger plans
  - financial statements
  - audit evidence?
5. Explain the difference between:
  - SIT
  - EDM
  - Trainable Classifiers
  - Sensitivity Labels

### Task 2 – Encryption & Protection
#### Objective
Evaluate how information protection should be applied.
#### Questions
1. Which documents should be encrypted?
2. Which users should have access?
3. Should external sharing be allowed?
4. When would “Do Not Forward” be appropriate?
5. How does encryption differ from DLP?

6. How does protection remain persistent after files leave the organization?

### Task 3 – DLP Investigation
#### Objective
Investigate sensitive data movement.
#### Questions
1. Which DLP policies should trigger in this scenario?
2. Which activities represent high-risk behavior?
3. Which actions should:
  - warn users
  - block activity
  - allow override with justification?
4. Which activities should generate alerts?
5. Which workloads should be monitored?
6. How does DLP differ from Endpoint DLP?

### Task 4 – Endpoint Governance
#### Objective
Investigate endpoint-level risks.
#### Questions
1. Which endpoint activities are risky?
2. Should USB transfers be:
  - blocked
  - audited
  - allowed with justification?
3. Which browser activities create governance risk?
4. How can Endpoint DLP help detect:
  - clipboard usage

  - local file copies
  - browser uploads
  - AI prompt submissions?
5. Why is endpoint governance critical in remote work environments?

### Task 5 – Insider Risk Investigation
#### Objective
Analyze risky user behavior.
#### Questions
1. Why did the user risk score increase?
2. Which behavioral indicators contributed?
3. How did resignation status affect risk analysis?
4. Which activities indicate:
  - accidental risk
  - malicious intent?
5. How does Insider Risk Management differ from DLP?
6. Which additional telemetry would improve the investigation?

### Task 6 – Adaptive Protection
#### Objective
Apply risk-based governance.
#### Questions
1. What should happen when a user becomes:
  - low risk
  - medium risk
  - elevated risk?
2. Which controls should Adaptive Protection strengthen?
3. Should elevated-risk users receive:

  - stricter DLP
  - stronger access restrictions
  - longer retention
  - reduced sharing permissions?
4. How does Adaptive Protection improve traditional DLP?

### Task 7 – Audit Investigation
#### Objective
Reconstruct the activity timeline.
#### Questions
1. Which audit logs should investigators review first?
2. Which activities indicate potential exfiltration?
3. Which filters are most useful during audit searches?
4. Why is Audit Premium valuable?
5. Which logs should be exported for investigation evidence?
6. How does audit retention affect investigations?

### Task 8 – Content Search & eDiscovery
#### Objective
Locate and preserve investigation evidence.
#### Questions
1. Which content locations should be searched?
2. Which keywords would help identify impacted content?
3. When should the investigation escalate into eDiscovery?
4. Which exported evidence formats may be required?
5. How should legal evidence be preserved?
6. Explain the difference between:
  - Content Search

  - eDiscovery

### Task 9 – AI Governance
#### Objective
Investigate AI-related governance risks.
#### Scenario Update
Investigation reveals that confidential merger summaries were pasted into unmanaged
AI tools.
#### Questions
1. Which controls should have detected this activity?
2. How can Endpoint DLP help govern AI prompts?
3. How does Insider Risk Management support AI investigations?
4. Why is AI governance becoming critical for enterprises?
5. What governance policies would you recommend for AI usage?

#### Final Deliverables
Your team must prepare:
1. Incident Summary
Explain:
- what occurred
- timeline of events
- impacted systems

2. Impact Assessment
Identify:
- exposed data
- business impact
- regulatory concerns

3. Governance Analysis
Evaluate:
- which Microsoft Purview controls worked
- which controls failed
- where visibility gaps existed

4. Investigation Findings
Provide:
- evidence summary
- risky behaviors identified
- exfiltration indicators
- policy violations

5. Governance Recommendations
Recommend improvements for:
- DLP
- Endpoint DLP
- Insider Risk
- Adaptive Protection
