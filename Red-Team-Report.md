# Red Team Report

## 1. Introduction

The purpose of this report is to investigate suspicious activities observed during the HawkEye cybersecurity investigation.

The Red Team approach focuses on understanding possible attacker behaviour, including how an attacker may communicate with a compromised system and what techniques may be involved.

## 2. Objective

The main objectives of this investigation are:

- Understand suspicious network activity.
- Study possible malware communication methods.
- Identify suspicious IP addresses and domains from the available evidence.
- Understand possible attacker techniques.
- Map observed behaviour to the MITRE ATT&CK framework.

## 3. Investigation Scope

This investigation focuses on the HawkEye lab evidence and the network traffic available in the provided PCAP file.

The investigation includes examining DNS requests, HTTP communication, external network connections and possible indicators of suspicious activity.

No real-world systems will be attacked.

## 4. Evidence Analysis

The available network traffic was examined using Wireshark to identify:

- Suspicious network connections.
- DNS requests and domain resolutions.
- HTTP requests and responses.
- Possible communication with external servers.
- Potential indicators of automated or malicious activity.

The identified IP addresses and domains are documented in Section 6.

## 5. MITRE ATT&CK Mapping

The observed network activities were compared with the MITRE ATT&CK framework to identify possible attacker techniques.

### 5.1 Ingress Tool Transfer (T1105)

- **Technique:** Ingress Tool Transfer
- **Tactic:** Command and Control
- **Evidence:** HTTP GET request for `tkraw_Protected99.exe`.
- **Packet:** 210
- **Explanation:** An executable file was requested from an external server. The server returned an HTTP 200 OK response containing executable content.

This activity is consistent with file transfer behaviour described by MITRE ATT&CK. However, the malicious nature of the file has not been independently verified, and its execution has not been confirmed.

**MITRE Reference:** https://attack.mitre.org/techniques/T1105/

### 5.2 Application Layer Protocol: Web Protocols (T1071.001)

- **Technique:** Web Protocols
- **Tactic:** Command and Control
- **Evidence:** Repeated HTTP GET requests to `66.171.248.178`.
- **Source IP:** `10.4.10.132`
- **Explanation:** Repeated HTTP communication was observed at approximately 10-minute intervals.

This pattern may be consistent with automated communication or possible beaconing activity. However, additional evidence is required to confirm command-and-control behaviour.

**MITRE Reference:** https://attack.mitre.org/techniques/T1071/001/

### 5.3 Mapping Limitations

The MITRE ATT&CK technique mappings are preliminary and are based on the network traffic observations.

Further investigation of the downloaded executable, endpoint activity and HTTP communication is required before confirming malicious behaviour.

## 6. Network Investigation Findings

### 6.1 Suspicious Executable Download

Wireshark analysis identified an HTTP GET request for the following file:

`/proforma/tkraw_Protected99.exe`

**Evidence:**

- Request packet: 210
- Response packet: 3155
- Source IP: `10.4.10.132`
- Destination domain: `proforma-invoices.com`
- Server IP: `217.182.138.150`
- HTTP response: `200 OK`
- Content type: `application/x-msdownload`
- Content length: `2025472` bytes

The HTTP response indicates that the external server returned executable content to the investigated computer. However, this evidence alone does not confirm that the file was executed.

### 6.2 Repeated External Communication

Repeated HTTP GET requests were observed from the investigated computer (`10.4.10.132`) to the external IP address `66.171.248.178`.

The requests occurred at approximately 10-minute intervals.

The repeated communication may indicate automated beaconing activity. However, further investigation is required to determine the purpose of this communication and whether it represents command-and-control activity.

### 6.3 DNS Investigation

The following external domains and their resolved IP addresses were observed in the DNS traffic:

| Domain | Resolved IP |
|---|---|
| `proforma-invoices.com` | `217.182.138.150` |
| `bot.whatismyipaddress.com` | `66.171.248.178` |
| `macwinlogistics.in` | `23.229.162.69` |

These domains and IP addresses have been documented as indicators for further investigation. Their malicious status has not been independently confirmed.

### 6.4 Summary of Findings

The network investigation identified the following activities:

1. An HTTP request for an executable file from `proforma-invoices.com`.
2. An HTTP 200 OK response containing executable content.
3. Repeated HTTP GET requests to `66.171.248.178` at approximately 10-minute intervals.
4. DNS requests resolving the external domains listed in this report.

These observations provide useful indicators for further malware analysis and defensive monitoring.

## 7. Overall Conclusion

The Red Team investigation identified potentially suspicious network activities in the HawkEye PCAP file, including an executable download and repeated communication with an external server.

The observed activities were mapped to relevant MITRE ATT&CK techniques as preliminary findings.

Although these observations may indicate suspicious behaviour, the available network evidence alone does not confirm malware execution or command-and-control activity.

The findings can help the Blue Team develop detection rules, investigate suspicious network traffic and improve defensive monitoring.
