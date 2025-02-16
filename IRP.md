# Incident Response Plan Structure for Catnip Games International

## 1. Introduction

### Purpose
As Catnip Games expands its multiplayer gaming infrastructure, ensuring security is critical to protect player data, maintain game availability, and prevent security breaches. This Incident Response Plan (IRP) provides a structured approach to identifying, managing, and mitigating security incidents, ensuring a quick and coordinated response while maintaining player trust.

### Objectives
- Detect and respond to security incidents with minimal impact on game services.
- Automate response workflows using **Cortex** and **MISP**.
- Centralize incident tracking and coordination with **TheHive**.
- Improve collaboration between **SOC, development, and infrastructure teams**.
- Ensure compliance with **data protection regulations (GDPR)**.

## 2. Scope and Applicability
This plan applies to **all Catnip Games systems, networks, and services**, including:

- **300+ Linux servers** across two data centers.
- **Sensitive services**: player data, matchmaking, game hosting, and APIs.
- **Integration points** with third-party services or platforms.

### Types of Incidents Covered
- **DoS attacks**
- **Bot exploits** of game mechanics
- **Unauthorized data access**
- **Account compromises**
- **Social engineering attacks**

## 3. Incident Response Team (Roles and Responsibilities)

| **Team/Role**            | **Responsibilities**  |
|-------------------------|----------------------------------|
| **SOC Analysts**         | Monitor alerts, perform initial triage, categorize incidents, initiate investigations. |
| **Incident Handler**     | Lead response, coordinate between teams, document incident details in TheHive. |
| **Threat Intelligence Team** | Enrich alerts with MISP, analyze IOCs, update threat feeds. |
| **Development Team**     | Assist in application-related vulnerabilities, patching, and game logic fixes. |
| **Infrastructure Team**  | Handle Linux server security, network defense, and system recovery. |
| **Management**          | Approve escalations, handle external communication, and make major decisions. |

## 4. Incident Response Lifecycle

### 4.1. Preparation
- Deploy **TheHive** for centralized case management.
- Configure **MISP** for real-time threat intelligence sharing.
- Set up **Cortex playbooks** for automated mitigation (e.g., blocking malicious IPs).
- Harden **Linux servers** (disable password SSH access, enable MFA for privileged accounts).
- Establish **logging and monitoring** via **Elasticsearch**.
- Conduct **SOC training and incident response drills**.

### 4.2. Detection and Analysis
#### Automated Threat Detection
- **Elasticsearch logs** monitor **network traffic, API activity, and authentication attempts**.
- **Anomalous behavior** (e.g., high login failures, data exfiltration attempts) triggers alerts in **TheHive**.

#### Incident Categorization (MISP Integration)
- Query **MISP** for known **IP addresses, malware hashes, phishing domains**.
- Assign a severity level based on predefined classification criteria.

#### Initial Investigation & Impact Analysis
- Review logs, affected systems, and attack vector.
- Determine **business impact** (e.g., downtime, data exposure, player complaints).

### 4.3. Containment, Eradication, and Recovery
#### Containment (Automated & Manual)
- **Account Compromise:**
  - Lock compromised accounts **automatically via Cortex**.
  - Enforce **password resets** and notify users.
- **DoS or Bot Attack:**
  - Apply **rate-limiting on affected APIs**.
  - **Blacklist attacker IPs** using Cortex & firewall rules.
- **Malware or Unauthorized Access:**
  - Isolate affected **server or user accounts**.
  - Conduct **forensic analysis** to assess damage.

#### Eradication & Recovery
- **Apply patches, revoke access, remove malware**.
- **Restore affected systems from backups (if necessary)**.
- **Gradually reintroduce blocked traffic to prevent recurrence**.

### 4.4. Post-Incident Activity
1. **Root Cause Analysis**
   - Determine how the attack happened and how to prevent it.
2. **Threat Intelligence Updates**
   - Add **new IOCs to MISP** (e.g., attacker domains, IPs).
3. **Incident Documentation in TheHive**
   - Capture all steps taken, lessons learned.
4. **Playbook Improvement**
   - Refine **Cortex automation rules** for faster response next time.

## 5. Incident Classification and Prioritization

| **Severity Level** | **Description** | **Response Time** | **Escalation Path** |
|-------------------|------------------------------------------------|-------------------|----------------------------------|
| **Critical**       | Data breach, large-scale account compromises | Immediate        | SOC → Management → Development |
| **High**           | Targeted attacks on matchmaking, authentication APIs | 1 hour            | SOC → Infrastructure |
| **Medium**         | Minor bot exploits, small-scale DoS attacks | 4 hours           | SOC → Threat Intelligence |
| **Low**            | Failed login attempts, minor reconnaissance | 24 hours          | SOC only |

## 6. Response Playbooks
### 6.1. Account Compromise Playbook
#### Trigger: Multiple failed login attempts, suspicious activity.
- **Lock affected accounts using Cortex.**
- **Force password reset and 2FA enforcement.**
- **Notify affected users and monitor for further compromise.**

### 6.2. Malware Detection Playbook
#### Trigger: Malware hash detected in logs.
- **Isolate affected server.**
- **Scan for persistence mechanisms.**
- **Remove malware and apply patches.**

## 7. Communication and Escalation Procedures
### Internal Communication
- SOC team updates **Teams incident channels**.
- Major incidents require **management briefing within 1 hour**.

### External Communication
- If **player accounts are compromised**, notify affected users.
- If a major security breach occurs, **PR team issues a statement**.

## 8. Reporting and Continuous Improvement
- **Automated reports from TheHive** summarize incident trends.
- **Key Metrics:**
  - Mean Time to Detect (**MTTD**).
  - Mean Time to Respond (**MTTR**).
  - % of incidents mitigated automatically by Cortex.
- **Quarterly tabletop exercises** to test new attack scenarios.

## 9. Prototype Implementation Steps
1. **Deploy TheHive** for case tracking.
2. **Set up MISP** to ingest threat intelligence.
3. **Develop Cortex playbooks** for automated mitigation.
4. **Configure Elasticsearch** for real-time monitoring.
5. **Simulate real-world attacks to test response workflows.**

## 10. Training and Awareness
- **Quarterly Red Team exercises** simulating bot attacks and phishing.
- **SOC analysts trained on threat hunting and incident handling.**

## 11. Legal and Compliance Considerations
- Ensure compliance with **GDPR** and **local data protection laws**.
- Maintain **audit logs** of all security incidents.

