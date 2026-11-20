# Red Team Investigation Report – HawkEye Lab

## 1. Introduction

This report presents the Red Team investigation of suspicious network activities identified during the HawkEye cybersecurity lab exercise.

The purpose of the investigation is to understand possible attacker behaviour by examining network traffic, identifying suspicious external connections, investigating executable downloads, and mapping observed activities to the MITRE ATT&CK framework.

The investigation uses the available HawkEye PCAP file and Wireshark to examine network evidence.

## 2. Investigation Objectives

The main objectives of this investigation are:

- Identify potentially suspicious network connections.
- Investigate possible malware-related communication.
- Identify external IP addresses and domains involved in the observed traffic.
- Examine HTTP requests and responses.
- Identify possible attacker techniques.
- Map observed activities to the MITRE ATT&CK framework.
- Provide useful findings for the Blue Team investigation.

## 3. Investigation Scope

The investigation focuses on the network traffic captured in the HawkEye lab PCAP file.

The analysis includes:

- DNS requests and domain resolutions.
- HTTP requests and responses.
- External IP address communication.
- A suspicious executable download.
- Repeated communication between the investigated computer and an external server.

Wireshark was used to examine the available network packets.

This investigation is limited to the evidence available in the PCAP file. It does not include confirmation of malware execution or direct access to the investigated computer.

No real-world systems were attacked.

## 4. Tools and Frameworks Used

| Tool / Framework | Purpose |
|---|---|
| Wireshark | Examining and analysing network packets |
| HawkEye PCAP | Providing network investigation evidence |
| MITRE ATT&CK | Mapping observed behaviour to known attacker techniques |

## 5. MITRE ATT&CK Technique Mapping

The observed network activities were compared with the MITRE ATT&CK framework to identify techniques that may be relevant to the investigation.

These mappings are preliminary because network evidence alone cannot establish the attacker's intent or confirm that a system was compromised.

### 5.1 Ingress Tool Transfer – T1105

**Tactic:** Command and Control

**Evidence:**
- HTTP GET request for `tkraw_Protected99.exe`.
- Request packet: 210.
- Response packet: 3155.
- External server: `217.182.138.150`.

**Explanation:**

The investigated computer requested an executable-named file from an external server. The server returned an HTTP 200 OK response with the content type `application/x-msdownload`.

This activity is consistent with the transfer of a tool or file from an external system. However, the actual file contents, malicious nature, and execution status have not been independently verified.

**MITRE ATT&CK Reference:**  
https://attack.mitre.org/techniques/T1105/

### 5.2 Application Layer Protocol: Web Protocols – T1071.001

**Tactic:** Command and Control

**Evidence:**
- Repeated HTTP GET requests.
- Investigated computer: `10.4.10.132`.
- External IP address: `66.171.248.178`.
- Communication observed at approximately 10-minute intervals.

**Explanation:**

Repeated HTTP communication was observed between the investigated computer and an external server.

The regular communication pattern may indicate automated activity or possible beaconing. Such behaviour can be associated with command-and-control communication.

However, the available network evidence does not confirm that the external server was being used for command and control.

**MITRE ATT&CK Reference:**  
https://attack.mitre.org/techniques/T1071/001/

### 5.3 Technique Mapping Limitations

The technique mappings are based on observed network behaviour rather than confirmed attacker activity.

Additional endpoint investigation, file analysis, and examination of the complete communication would be required to confirm the techniques.

## 6. Network Investigation Findings

### 6.1 Suspicious Executable Download

During the Wireshark investigation, an HTTP request was identified for the following file:

`/proforma/tkraw_Protected99.exe`

**Evidence details:**

| Field | Observation |
|---|---|
| HTTP request packet | 210 |
| HTTP response packet | 3155 |
| Investigated computer | `10.4.10.132` |
| External server | `217.182.138.150` |
| Domain | `proforma-invoices.com` |
| Requested file | `tkraw_Protected99.exe` |
| HTTP response | `200 OK` |
| Content type | `application/x-msdownload` |
| Content length | 2,025,472 bytes |

**Analysis:**

The investigated computer requested an executable-named file from an external server. The server successfully responded with HTTP 200 OK and an executable-associated content type.

This is an important investigation finding because unexpected executable downloads can be associated with malware delivery.

However, the response does not independently prove that the file was malicious, successfully saved, or executed on the investigated computer.

### 6.2 Repeated External Communication

Repeated HTTP GET requests were observed from the investigated computer to the following external IP address:

`66.171.248.178`

**Evidence details:**

- Investigated computer: `10.4.10.132`
- External IP address: `66.171.248.178`
- Communication protocol: HTTP
- Observed pattern: Repeated requests at approximately 10-minute intervals.
- HTTP responses: Successful responses were observed.

**Analysis:**

The repeated communication pattern may indicate automated communication between the investigated computer and an external server.

Regular communication can be worth investigating because some malware communicates with external infrastructure at scheduled intervals.

This behaviour may be consistent with beaconing, but the available evidence does not confirm command-and-control activity.

### 6.3 DNS Investigation

The DNS traffic revealed the following domain-to-IP address resolutions:

| Domain | Resolved IP Address |
|---|---|
| `proforma-invoices.com` | `217.182.138.150` |
| `bot.whatismyipaddress.com` | `66.171.248.178` |
| `macwinlogistics.in` | `23.229.162.69` |

**Analysis:**

These DNS requests show that the investigated computer resolved multiple external domains during the captured network activity.

The resolution of `proforma-invoices.com` is relevant to the executable download identified in Section 6.1.

The resolution of `bot.whatismyipaddress.com` is relevant to the repeated communication observed with `66.171.248.178`.

These domains and IP addresses should be treated as investigation indicators. Their malicious status has not been independently confirmed.

## 7. Key Indicators Identified

The following indicators were identified during the network investigation.

| Indicator Type | Value | Reason for Investigation |
|---|---|---|
| Internal IP | `10.4.10.132` | Investigated computer |
| External IP | `217.182.138.150` | Server involved in executable download |
| External IP | `66.171.248.178` | Repeated HTTP communication |
| External IP | `23.229.162.69` | DNS resolution observed |
| Domain | `proforma-invoices.com` | Associated with executable download |
| Domain | `bot.whatismyipaddress.com` | Associated with repeated external communication |
| Domain | `macwinlogistics.in` | DNS resolution observed |
| File | `tkraw_Protected99.exe` | Executable-named file requested |

These indicators can be used by the Blue Team for further investigation and defensive monitoring.

## 8. Red Team Assessment

The investigation identified several activities that deserve further security analysis:

1. An HTTP request for an executable-named file from an external server.
2. A successful HTTP response containing executable-associated content.
3. Repeated HTTP communication with an external IP address at approximately 10-minute intervals.
4. DNS requests resolving multiple external domains.
5. Network behaviour that may be consistent with automated communication.

The executable download and repeated external communication are the most important findings for further investigation.

The findings should not be treated as proof of malware execution or confirmed command-and-control activity without additional evidence.

## 9. Recommendations for Further Investigation

Based on the identified findings, the following actions are recommended:

- Investigate the downloaded executable using a safe malware-analysis environment.
- Examine endpoint logs to determine whether the executable was executed.
- Monitor repeated outbound connections to identify further suspicious communication.
- Review DNS activity for unusual or unexpected domain requests.
- Create detection rules to monitor suspicious downloads and repeated external communication.
- Share the identified indicators with the Blue Team for defensive investigation.

## 10. Overall Conclusion

The Red Team investigation of the HawkEye PCAP file identified potentially suspicious network activities, including an executable download, repeated HTTP communication with an external server, and DNS requests involving multiple external domains.

The observed activities were compared with the MITRE ATT&CK framework and mapped to Ingress Tool Transfer (T1105) and Web Protocols (T1071.001) as preliminary technique assessments.

The investigation provides useful network indicators and findings for the Blue Team to examine further.

However, the available PCAP evidence alone does not confirm that the downloaded file was malicious, that it was executed, or that the repeated external communication represented command-and-control activity.

The findings will support the Blue Team investigation and the Purple Team assessment by helping identify areas where defensive monitoring and detection can be improved.

---

**Report Status:** Network investigation completed based on available PCAP evidence. Further file and endpoint investigation is recommended.
