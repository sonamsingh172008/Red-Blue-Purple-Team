# Red Team Report

## 1. Introduction

The purpose of this report is to understand suspicious activities observed during the HawkEye cybersecurity investigation.

The Red Team approach focuses on understanding how an attacker may communicate with a compromised system and what techniques may be involved.

## 2. Objective

- Understand suspicious network activity.
- Study possible malware communication methods.
- Identify suspicious IP addresses and domains from the available evidence.
- Understand possible attacker techniques.
- Map observed behaviour to the MITRE ATT&CK framework.

## 3. Investigation Scope

The investigation focuses on the previously collected HawkEye lab evidence and network traffic.

No real-world systems will be attacked.

## 4. Evidence Analysis

The available network traffic will be examined to identify:

- Suspicious network connections.
- DNS requests.
- HTTP communication.
- SMTP communication.
- Possible communication with external servers.

Specific IP addresses, domains and timestamps are documented in Section 7.

## 5. MITRE ATT&CK Mapping

Observed attacker behaviour will be compared with the MITRE ATT&CK framework.

Only techniques supported by the investigation evidence will be included.


## 6. Network Investigation Findings

### 6.1 Suspicious Executable Download

Wireshark analysis identified an HTTP GET request for:

`/proforma/tkraw_Protected99.exe`

**Evidence:**
- Request packet: 210
- Response packet: 3155
- Destination domain: proforma-invoices.com
- Server IP: 217.182.138.150
- HTTP response: 200 OK
- Content type: application/x-msdownload
- Content length: 2025472 bytes

This activity indicates that an executable file was successfully served to the investigated computer.

### 6.2 Repeated External Communication

Repeated HTTP GET requests were observed from 10.4.10.132 to 66.171.248.178.

The requests occurred approximately every 10 minutes.

This regular communication may indicate automated beaconing activity and requires further investigation.

### 6.3 DNS Investigation

The following domains were observed:

| Domain | Resolved IP |
|---|---|
| proforma-invoices.com | 217.182.138.150 |
| bot.whatismyipaddress.com | 66.171.248.178 |
| macwinlogistics.in | 23.229.162.69 |

These domains have been identified for further investigation. Their malicious status has not been independently confirmed.

### 6.4 Summary of Findings

The network investigation identified an executable download and repeated communication with an external server.

These findings provide useful indicators for further malware analysis and defensive monitoring.


## 7. Overall Conclusion

The Red Team investigation aims to understand possible attacker behaviour and provide useful information to help the Blue Team improve security monitoring and detection.
