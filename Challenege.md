### 💡 Challenge 01: Custom SIT & Pattern Testing

**Objectives:**
- Create a second regex-based SIT for a different pattern (e.g., `CUS\d{5}` for customer IDs)
- Modify the keyword dictionary to include additional terms (e.g., "migraine", "fever")
- Test how the changes affect match behavior

**Learning Outcome:** This gives faster learners something meaningful to do while others finish, and helps reinforce pattern tuning and testing workflows.

### 💡 Challenge 02: Marketing Sublabel & Auto-Labeling

**Objectives:**
- Create a sublabel for Marketing content that allows unrestricted access but adds headers/footers for tracking.
- Modify the Financial Data label's auto-labeling policy to include a custom SIT created in a previous lab.
- Explore the audit log to verify whether the auto-labeling policy has applied the label to any content (if audit is enabled and time allows).

**Learning Outcome:** Reinforces label hierarchy and auto-labeling policy configuration.

### 💡 Challenge 03:
**Objectives:**
- Create an additional custom OME template for another department (e.g., Legal or Executive), using a different expiration period or intro text
- Modify the mail flow rule to apply encryption only when the subject line contains specific keywords (e.g., “Confidential” or “Secure”)
- Test how emails behave when sent from Outlook desktop vs. Outlook on the web

**Learning Outcome:** This reinforces PowerShell-based customization and expands awareness of mail flow rule flexibility.

### 💡 Challenge 04:
**Objectives:**
- Create a second DLP policy in PowerShell that targets the “Contoso Diseases List” SIT and restricts external sharing in Exchange or OneDrive
- Modify an existing DLP policy to include more granular conditions, such as matching a specific domain (e.g., externalpartner.com) or requiring exact data match (EDM) info types
- Create a Defender file policy that uses a different sensitive info type (e.g., SWIFT Code) and assigns a different governance action like notifying admins
- Adjust policy tip text to include custom guidance for users (e.g., “Sharing financial data externally requires business justification. Please remove sensitive content or provide a reason.”)

**Learning Outcome:** These tasks reinforce configuration fluency, policy refinement, and broader understanding of both automation and user experience in DLP enforcement.

### 💡 Challenge 05:
**Objectives:**
- Modify the USB transfer policy to log instead of block, then change it back after exploring the policy tip behavior
- Add additional device actions like “Print” or “Copy to network share” to the same rule
- Block access to generative AI domains by adding bard.google.com or chat.openai.com under Service domains in the DLP settings
- Explore the Advanced classifications tab to see how Content Explorer could be used to validate whether endpoint activities are being flagged or captured
- Bonus task (for those with time and permissions): Simulate activity by copying a text snippet that matches a sensitive info type into Notepad and saving to USB. Observe alerts in Activity explorer if integration is enabled.

**Learning Outcome:** These challenges reinforce advanced endpoint protection techniques and give learners a chance to see how DLP can be fine-tuned and tested in real-world deployments.

### 💡 Challenge 06:
**Objectives:**
- Create a second retention label that uses event-based retention, such as retaining a contract for X years after expiration.
- Configure a disposition review for a label to understand how content reviewers are notified and complete actions in the Purview portal.
- Use PowerShell to list published labels or active retention policies and explore how these can be managed at scale.
- Review and interpret retention policy overlap using the Microsoft Purview Policy Lookup tool, and explore which policy would apply when multiple exist.

**Learning Outcome:** These challenges help reinforce deeper functionality of Microsoft Purview retention and allow learners to explore the more advanced or edge-case retention scenarios they may encounter in enterprise environments.

### 💡 Challenge 07:
**Objectives:**
- Create a custom policy for general data exfiltration that uses adaptive thresholds and applies to all users except the finance department
- Modify the notice template to include links to organizational data handling policies or internal reporting portals
- Adjust the data leak policy thresholds or indicator weights to increase sensitivity to specific actions (e.g., printing or file sharing)

### 💡 Challenge 08:
**Objectives:**
- Add a second DLP rule to the Credit Card policy that uses Moderate risk as the condition and sets it to Audit only, contrasting it with the Elevated risk rule
- Discuss how Adaptive Protection could reduce alert fatigue by narrowing enforcement to high-risk users only

### 💡 Challenge 09:
**Objectives:**
- Modify the search scope to target specific users or rule names, simulating a targeted investigation.
- Create a second audit retention policy with a different priority or record type to simulate layered retention logic.
- Discuss how audit retention intersects with incident response workflows, especially for insider risk or privileged access reviews.

**Learning Outcome:** These tasks reinforce how audit logging and retention serve as foundational tools for incident detection, compliance auditing, and long-term forensic readiness.

### 💡 Challenge 10:
**Objectives:**
- Use advanced search syntax (KeyQL) or natural language Copilot (if preview enabled) to create a broader or more complex search query
- Expand the data source to include multiple teams or specific user mailboxes
- Investigate differences between Core and Premium eDiscovery experiences
- Create a second case to simulate parallel investigations with different scopes

**Learning Outcome:** These challenges help learners understand the depth of Microsoft Purview’s investigation capabilities, from simple keyword detection to managing full legal or compliance review workflows.

### 💡 Challenge 11:
**Objectives:**
- Modify the insider risk policy to include additional indicators or change the triggering event to simulate different use cases (e.g., privilege escalation).
- Add a second DLP rule for moderate-risk users to allow auditing instead of blocking, illustrating graduated enforcement.
- Discuss how data assessments might feed into auto-labeling policies or adaptive retention based on the findings.

