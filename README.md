# AD Login Detection + Auto-Containment (Splunk + Shuffle)

**One-liner:** Built a Splunk + Shuffle workflow to detect anomalous **4624** logons (external IP/RDP) and trigger approved **AD account disablement**, reducing containment to **<1 minute**.

**Stack:** Splunk (SIEM) • Shuffle (SOAR) • Active Directory (AD DS) • Windows Server 2022 • Universal Forwarder • Vultr (VPC) • Slack/Email  
**Use case:** Suspicious RDP login → detect in Splunk → notify analyst → approve → disable user in AD

## What I Built (Flow)
1. Deployed a cloud **Active Directory** lab in **Vultr VPC** (Windows Server 2022 DC + Windows client).
2. Shipped **Windows Security logs** to **Splunk** using **Universal Forwarders**.
3. Wrote **Splunk SPL** to detect anomalous **Event ID 4624** logons from **external IPs** (RDP).
4. Triggered **Shuffle** via webhook to send **Slack/email** alerting.
5. Implemented **human approval** before running automated containment (**Disable-AD-User**), then posted confirmation.

## Outcomes (Measurable)
- **Containment:** **<1 minute** from alert → approved account disablement  
- **Reduced manual effort:** replaced “log in + disable user” with a controlled one-click workflow  
- **Improved visibility:** clear audit trail via ticket/notifications + confirmation message

## Screenshots / Evidence

### Workflow Diagram
![Active Directory Project Diagram](key-screenshots/Active-Directory-Project-Digram-V2.drawio.png)

### Detection (Splunk SPL / 4624)
![Splunk Detection Dashboard](key-screenshots/1-The-Detection-Splunk-Query.png)

### SOAR Orchestration (Shuffle)
![Shuffle Workflow Logic](key-screenshots/2-The-Orchestration-Shuffle-Workflow.png)

### Analyst Triage (Slack + Approval)
![Slack Triage Notification](key-screenshots/3.1-The-Triage-Slack-Alert-and-Email-Approval.png)
![Email Approval Prompt](key-screenshots/3.2-The-Triage-Slack-Alert-and-Email-Approval.png)

### Response Confirmation (AD Disable + Slack Closeout)
![Active Directory Disabled Account](key-screenshots/4.1-The-Response-Final-Confirmation-and-Disabled-Account.png)
![Final Slack Confirmation](key-screenshots/4.2-The-Response-Final-Confirmation-and-Disabled-Account.png)

## Skills Demonstrated
- **Detection Engineering (Splunk SPL / Windows Security Logs)**
- **SOAR Automation (Shuffle)**
- **Identity & Access Management (Active Directory)**
- **Incident Response (containment + comms)**
- **Webhook / API Integration**

## Next Improvements
- Add enrichment (GeoIP, allowlisted ranges, known admin sources) to reduce false positives.
- Expand detections to AD attack paths (Kerberoasting / lateral movement) with additional event correlations.
- Add case management integration to track approvals and remediation steps end-to-end.

## Resources
- **Complete Process Screenshots:** [Full Screenshot Process](./full-screenshot-process)
