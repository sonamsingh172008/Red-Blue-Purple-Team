# Purple Team Assessment and Collaboration Report

## 1. Introduction

The purpose of this Purple Team assessment is to bring Red Team and Blue Team activities together to evaluate an organisation's security.

The Red Team focuses on identifying weaknesses and demonstrating potential attack activity. The Blue Team focuses on monitoring, detecting, investigating, and responding to suspicious activity.

The Purple Team connects both teams by using the findings from security investigations to improve detection capabilities and strengthen defensive measures.

This assessment uses findings from the Red Team investigation, Wireshark analysis, and the review of Elastic Security detection-rule configurations.

## 2. Objectives

The main objectives of this assessment were:

- Review the suspicious activities identified during the Red Team investigation.
- Evaluate how the Blue Team investigated the available evidence.
- Review existing detection rules.
- Identify gaps in security monitoring.
- Recommend improvements to detection and incident response.
- Improve communication and collaboration between offensive and defensive security activities.

## 3. Assessment Environment and Tools

| Tool or Evidence | Purpose |
|---|---|
| Wireshark | Analyse captured network traffic |
| `stealer.pcap` | Investigate suspicious network activity |
| Elastic Security | Detection-rule configuration review |
| GitHub | Store reports and detection-rule files |

Elastic/Kibana was not accessible during the final validation stage. Therefore, live detection and alert generation could not be confirmed.

## 4. Red Team Findings Reviewed

The Purple Team reviewed the suspicious activity identified during the investigation.

### 4.1 Suspicious External Communication

Repeated HTTP communication was observed between the internal computer `10.4.10.132` and external IP `66.171.248.178`.

The traffic included repeated HTTP GET requests and HTTP `200 OK` responses.

**Purple Team observation:** Repeated external communication should be investigated to determine whether it is expected or suspicious.

### 4.2 Executable-Associated HTTP Response

An HTTP response was identified from `217.182.138.150` to `10.4.10.132`.

The response contained:

- HTTP status: `200 OK`
- Content type: `application/x-msdownload`
- Packet number: `3155`

**Purple Team observation:** An executable-associated response should trigger further investigation. The actual file contents and execution status were not confirmed.

### 4.3 DNS Activity

The following domain-to-IP mappings were observed:

| Domain | Resolved IP |
|---|---|
| `proforma-invoices.com` | `217.182.138.150` |
| `bot.whatismyipaddress.com` | `66.171.248.178` |
| `macwinlogistics.in` | `23.229.162.69` |

**Purple Team observation:** DNS activity should be correlated with network connections and other endpoint records to identify potentially suspicious behaviour.

These domains are investigation leads, not confirmed malicious domains.

## 5. Blue Team Detection Capabilities Reviewed

The Blue Team had three exported Elastic Security detection-rule configurations.

### Rule 1: Sysmon DNS Query Monitoring

- Event ID: 22
- Severity: Medium
- Risk score: 47
- Execution interval: 5 minutes
- Look-back period: 10 minutes

This rule monitors DNS queries recorded through Sysmon.

### Rule 2: Windows Credential Stuffing Detection

- Event ID: 4625
- Severity: Medium
- Risk score: 47
- Execution interval: 5 minutes
- Look-back period: 10 minutes
- Threshold: 2 failed events grouped by source IP

This rule looks for repeated failed Windows login attempts.

### Rule 3: PowerShell Script Block Monitoring

- Event ID: 4104
- Severity: High
- Risk score: 73
- Execution interval: 5 minutes
- Look-back period: 10 minutes

This rule monitors PowerShell script-block activity.

All three exported configurations were marked as enabled. However, actual execution and alert generation were not verified because Elastic/Kibana was inaccessible.

## 6. Purple Team Detection Gap Analysis

The Purple Team compared the suspicious activity with the existing detection rules.

| Observed activity | Existing detection coverage | Improvement needed |
|---|---|---|
| DNS requests | DNS monitoring rule exists | Correlate DNS events with other network activity |
| Repeated external communication | No dedicated rule among the three reviewed | Create an outbound connection monitoring rule |
| Executable-associated HTTP response | No dedicated download detection rule among the three reviewed | Monitor executable downloads |
| Failed Windows logins | Credential stuffing rule exists | Validate using controlled failed-login events |
| PowerShell activity | PowerShell monitoring rule exists | Validate event collection and alert generation |

### Main findings

1. DNS monitoring is included in the existing detection rules.
2. Windows failed-login monitoring is included.
3. PowerShell script-block monitoring is included.
4. Executable-associated downloads need additional detection coverage.
5. Repeated external IP communication needs additional monitoring.
6. Actual alert generation still requires validation.

## 7. Purple Team Recommendations

### 7.1 Improve Network Monitoring

Create detection rules to identify:

- Repeated connections to unusual external IP addresses.
- Unexpected outbound HTTP communication.
- Executable-associated file downloads.
- Unusual patterns of repeated network requests.

### 7.2 Improve DNS Monitoring

The DNS monitoring rule should be supported by:

- Reviewing unusual domain requests.
- Investigating repeated DNS lookups.
- Correlating DNS resolutions with network connections.
- Checking suspicious domains against trusted threat-intelligence sources.

### 7.3 Improve Endpoint Monitoring

Ensure that Windows systems collect the necessary security information.

Important events include:

- Event ID 4625 for failed login attempts.
- Event ID 4104 for PowerShell script-block activity.
- Sysmon Event ID 22 for DNS queries.

### 7.4 Improve Alert Validation

Every detection rule should be tested using controlled activity.

The team should:

1. Generate a safe test event.
2. Confirm that the event reaches the SIEM.
3. Check whether the detection rule identifies it.
4. Verify whether an alert is generated.
5. Record screenshots and investigation details.
6. Adjust the rule if the expected alert is not produced.

### 7.5 Improve Incident Response

When suspicious activity is identified, analysts should:

- Record the affected internal computer.
- Identify the external IP address or domain involved.
- Collect relevant packet and event records.
- Investigate potentially downloaded files safely.
- Determine whether the activity is legitimate or suspicious.
- Escalate confirmed incidents using the organisation's incident response process.

## 8. Purple Team Collaboration Plan

The following collaboration process is recommended:

| Stage | Red Team | Blue Team | Purple Team |
|---|---|---|---|
| 1. Identify activity | Demonstrates attack techniques in an authorised environment | Prepares monitoring | Defines the exercise objectives |
| 2. Collect evidence | Provides activity details | Collects logs and network evidence | Connects both sets of findings |
| 3. Review detection | Explains the activity performed | Checks existing rules | Identifies detection gaps |
| 4. Improve security | Provides attack insights | Updates detection rules | Recommends improvements |
| 5. Validate | Repeats safe test activity | Checks for alerts | Reviews whether detection works |

This process helps both teams understand how security weaknesses can be identified and addressed.

## 9. Assessment Results

| Assessment area | Result |
|---|---|
| Red Team findings reviewed | Completed |
| Network evidence investigated | Completed |
| DNS activity reviewed | Completed |
| Three detection-rule configurations reviewed | Completed |
| Detection gaps identified | Completed |
| Live alert generation | Not verified |
| Practical detection accuracy | Not verified |
| Detection improvement recommendations | Completed |

## 10. Conclusion

The Purple Team assessment brought together the offensive security findings and defensive investigation results.

The network investigation identified repeated external communication, DNS activity, and an HTTP response associated with an executable file type. The Blue Team's existing detection-rule configurations covered DNS monitoring, failed Windows logins, and PowerShell script-block activity.

The assessment identified additional monitoring needs, especially for executable-associated downloads and repeated outbound connections.

The main lesson from this project is that creating detection rules is only one part of cybersecurity defence. Those rules must also be tested against real or controlled security events to confirm that they work correctly.

Although live alert generation could not be verified during this assessment, the investigation and configuration review provided a foundation for improving detection coverage and collaboration between Red and Blue Teams.


**Overall Project Status:** Red Team findings reviewed, Blue Team investigation documented, and Purple Team improvement recommendations prepared. Live detection validation remains pending.
