# Red-Blue-Purple Team Cybersecurity Analysis Project

## Project Overview

This project demonstrates the roles and collaboration of Red, Blue, and Purple Teams in cybersecurity.

The objective is to understand how security threats can be investigated, how suspicious activities can be detected, and how defensive capabilities can be improved through collaboration.

The project includes network traffic investigation, detection-rule review, security findings, and recommendations for improving an organisation's security monitoring.

## Project Objectives

- Understand Red Team, Blue Team, and Purple Team operations.
- Investigate suspicious network communication.
- Identify unusual DNS activity and executable-associated HTTP responses.
- Review security detection-rule configurations.
- Identify gaps in existing detection coverage.
- Recommend improvements to security monitoring and incident response.
- Understand how offensive and defensive security teams work together.

## Project Components

### 1. Red Team

The Red Team focuses on identifying security weaknesses and understanding potential attack techniques in an authorised environment.

**Project focus:**
- Review potential attack activity.
- Identify suspicious behaviour.
- Document security findings.
- Provide information that can help improve defensive security.

**Report:** [Red Team Report](Red-Team-Report.md)

### 2. Blue Team

The Blue Team focuses on monitoring, investigating, and responding to suspicious activity.

**Project focus:**
- Analyse network traffic using Wireshark.
- Investigate suspicious external IP communication.
- Examine DNS requests and domain resolutions.
- Identify executable-associated HTTP responses.
- Review Elastic Security detection-rule configurations.

**Detection rules reviewed:**
- Windows Credential Stuffing Detection
- Sysmon DNS Query Monitoring
- PowerShell Script Block Monitoring

**Report:** [Blue Team Report](Blue-Team-Report.md)

### 3. Purple Team

The Purple Team brings Red Team and Blue Team activities together to improve overall security.

**Project focus:**
- Review Red Team findings.
- Evaluate Blue Team detection coverage.
- Identify monitoring gaps.
- Recommend detection improvements.
- Improve collaboration between offensive and defensive security teams.

**Report:** [Purple Team Report](Purple-Team-Report.md)

## Tools and Technologies

| Tool | Purpose |
|---|---|
| Wireshark | Network traffic analysis |
| Elastic Security | Detection-rule configuration review |
| Sysmon | Windows system monitoring and event collection |
| GitHub | Project documentation and version control |

## Key Investigation Findings

The network investigation identified:

- Repeated communication between an internal computer and an external IP address.
- DNS requests involving several external domains.
- An HTTP response with the content type `application/x-msdownload`.
- Potential monitoring gaps involving executable-associated downloads and repeated outbound connections.

These findings were treated as investigation leads. The packet evidence alone does not confirm malware execution or compromise.

## Detection Rules

Three Elastic Security detection-rule configurations were reviewed:

| Detection Rule | Windows Event ID | Purpose |
|---|---:|---|
| Sysmon DNS Query Monitoring | 22 | Monitor DNS queries |
| Windows Credential Stuffing Detection | 4625 | Identify repeated failed login attempts |
| PowerShell Script Block Monitoring | 4104 | Monitor PowerShell script activity |

All three exported configurations were marked as enabled.

**Validation limitation:** The Elastic/Kibana dashboard was unavailable during the final validation stage. Therefore, actual rule execution and alert generation were not verified.

## Project Results

The project successfully documented:

- Red Team findings.
- Blue Team network investigation.
- Three exported detection-rule configurations.
- Suspicious network and DNS activity.
- Detection coverage gaps.
- Purple Team recommendations.
- Opportunities to
