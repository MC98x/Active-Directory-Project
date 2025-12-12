# Active Directory

## Objective
The primary objective of this project was to build a comprehensive Active Directory environment in the cloud to simulate a corporate network, acting as both the Administrator and the SOC Analyst. The goal was to establish a detection and response pipeline that identifies unauthorized access (RDP Brute Force/Success) and utilizes a SOAR platform to automatically contain the threat by disabling the compromised user account in Active Directory.

---

## Skills Learned

**I. Infrastructure & Identity Management (IAM):**
* **Cloud Network Architecture:** Deployed a Virtual Private Cloud (VPC) in Vultr to host a Windows Server 2022 Domain Controller and a **Windows 11 Pro** Client, configuring internal networking to simulate a corporate LAN.
* **Active Directory Administration:** Promoted a server to a Domain Controller (DC), configured DNS, managed Organizational Units (OUs), and created User Accounts to mimic a realistic organizational structure.
* **Endpoint Configuration:** Successfully joined client workstations (using **Windows 11 Pro**'s domain join capability) to the domain and enabled Remote Desktop Protocol (RDP) to facilitate remote management and attack simulation.

**II. Detection Engineering (SIEM):**
* **Log Ingestion Pipeline:** Installed and configured Splunk Enterprise on a Linux server and deployed Universal Forwarders on Windows endpoints to ship Windows Event Logs and Sysmon telemetry.
* **SPL (Search Processing Language):** Developed custom Splunk queries to filter out noise and specifically identify Event ID 4624 (Successful Logins) and 4625 (Failed Logins) originating from unauthorized IP addresses.
* **Alert Configuration:** Tuned Splunk alerts to trigger near real-time notifications based on specific threshold logic (e.g., multiple failed attempts followed by a success).

**III. Security Orchestration, Automation, and Response (SOAR):**
* **Webhook Integration:** Established a listener in Shuffle to receive alerts directly from Splunk, converting raw log data into actionable JSON objects.
* **Active Directory Integration:** Authenticated Shuffle with the Active Directory environment, allowing the SOAR platform to perform administrative actions (resetting passwords, disabling accounts) remotely.
* **Human-in-the-Loop Logic:** Designed a decision tree in Shuffle that sends an approval request to the SOC Analyst (via Email/Slack) before taking remediation actions, preventing accidental lockouts.

**IV. Threat Simulation:**
* **Attack Generation:** Performed a Brute Force attack against the cloud-exposed RDP services to generate authentic "Failed Login" and "Successful Login" telemetry.
* **Telemetry Verification:** Validated that the attack patterns were correctly captured by Sysmon and indexed by Splunk, ensuring the visibility required for detection.

---

## Tools Used

**Security Operations Stack:**
* **Splunk Enterprise:** SIEM for log aggregation and searching.
* **Shuffle:** SOAR platform for workflow automation.
* **Splunk Universal Forwarder:** Endpoint log collection agent.
* **Sysmon:** Advanced background telemetry generation.

**Infrastructure & Environment:**
* **Vultr:** Cloud Service Provider (Hosting the Lab).
* **Windows Server 2022:** Domain Controller (Target).
* **Windows 11 Pro:** Client Workstation (Endpoint).
* **Ubuntu:** Hosting the Splunk Server.

**Utilities & Communication:**
* **PowerShell:** Used for AD setup and connectivity testing.
* **Slack:** Used for instant incident notification.
* **RDP (Remote Desktop):** Protocol used for administration and attack vector.
* **Draw.io:** Used for network diagramming.

---

## Network Diagram
to add..

---

## Key Results

**1. Automated Containment of Compromised Users**
By integrating Shuffle with Active Directory, I created a mechanism where a confirmed threat triggers a direct response. If an account shows signs of compromise (e.g., RDP login from a non-corporate IP), the system can automatically disable that user account in the Domain Controller.

**2. Telemetry Visibility & Ingestion**
Successfully established a complete data pipeline where Windows Security Logs and Sysmon data are generated on the endpoint, forwarded to the Indexer, and visualized in the Splunk Dashboard. This eliminated "blind spots" regarding user authentication activity.

**3. Drastic Reduction in Response Time (MTTR)**
The workflow transformed the account lockout process from a manual administrative task to a one-click operation.

* **Without Automation:** Analyst receives alert -> RDPs into Domain Controller -> Opens Active Directory Users & Computers -> Finds User -> Right Click "Disable". **(~10-15 Minutes)**
* **With Automation:** Analyst receives Slack Notification on phone -> Clicks "Approve" -> Shuffle API disables the account instantly. **(< 1 Minute)**

---

## Screenshots
*(Placeholder: Splunk Dashboard showing the brute force logs)*
*(Placeholder: Shuffle workflow showing the decision tree)*
*(Placeholder: Active Directory showing the "Account is Disabled" status)*
*(Placeholder: Slack notification asking for approval)*

---

## Future Improvements

To further evolve this Active Directory project, the following enhancements are planned:

* **Geo-Location Blocking:** Enhance the detection rules to automatically flag or block IPs based on geographic location using a plugin in Splunk.
* **Kerberoasting Simulation:** Expand the attack scope to include internal AD attacks like Kerberoasting to test detection capabilities against credential theft inside the perimeter.
* **Vulnerability Scanning:** Introduce Nessus to scan the Domain Controller for misconfigurations or unpatched vulnerabilities.
* **Report Generation:** Configure Splunk to email a weekly PDF report summarizing all RDP attempts and locked-out accounts to management.

---

## Conclusion

This Active Directory project demonstrates the ability to secure the most critical component of an enterprise network: the Identity Provider. By simulating a real-world attack scenario and building a response mechanism that bridges the gap between the **SIEM** (Detection) and **Active Directory** (Remediation), I have proven that I can not only monitor a network but actively defend it.

This project proves my ability to:
* Deploy and manage Windows Server and Active Directory infrastructure in the cloud.
* Write custom SPL to extract meaningful security insights from raw logs.
* Architect automated workflows that reduce the workload on SOC teams and minimize the dwell time of attackers.

These skills are essential for a modern SOC Analyst, enabling me to contribute immediately to threat detection and incident response operations.

---

## Resources and Documentation
to add..

