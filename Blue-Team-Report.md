# Blue Team Report – HawkEye Network Investigation

## 1. Introduction

The purpose of this Blue Team investigation was to examine network traffic from the HawkEye PCAP file and identify suspicious communication that could indicate a security threat.

The investigation was performed using Wireshark. DNS and HTTP traffic were examined to identify unusual external connections, repeated communication patterns and potentially suspicious file downloads.

## 2. Investigation Scope

The investigation focused on:

- Identifying the computer involved in the network activity.
- Examining DNS requests and responses.
- Investigating HTTP requests and server responses.
- Identifying repeated communication with external IP addresses.
- Suggesting defensive actions to reduce security risks.

### Network Information

| Item | Details |
|---|---|
| Investigated computer | `10.4.10.132` |
| Internal DNS server | `10.4.10.4` |
| Total packets in capture | 4,003 |
| Analysis tool | Wireshark |

## 3. DNS Traffic Investigation

DNS traffic was examined to identify the domains contacted by the investigated computer.

### 3.1 Repeated External DNS Requests

Repeated DNS queries were observed for the following domains:

| Domain | Resolved IP address |
|---|---|
| `bot.whatismyipaddress.com` | `66.171.248.178` |
| `macwinlogistics.in` | `23.229.162.69` |

Repeated DNS queries were observed for these domains during the captured network activity. This activity may indicate automated network communication and should be investigated further.

This repeated pattern may indicate automated network communication and should be investigated further.

### 3.2 Suspicious Domain Related to File Download

The computer also queried:

- Domain: `proforma-invoices.com`
- Resolved IP: `217.182.138.150`

The same IP address was involved in an HTTP request for an executable file, which is discussed in the HTTP investigation section.

This connection should be treated as suspicious and investigated further.

### 3.3 Normal DNS Activity

Other DNS requests included Windows connectivity checks, Google update requests and internal domain-controller lookups.

These requests provide useful context and should not automatically be classified as malicious.

## 4. HTTP Traffic Investigation

HTTP traffic was examined using the Wireshark display filter `http`.

Two external destination IP addresses were identified in the displayed HTTP traffic.

### 4.1 Executable File Download

Packet 210 showed an HTTP GET request from the investigated computer to an external server.

**Observed details:**

| Field | Finding |
|---|---|
| Source IP | `10.4.10.132` |
| Destination IP | `217.182.138.150` |
| Domain | `proforma-invoices.com` |
| Requested file | `tkraw_Protected99.exe` |
| HTTP method | GET |
| Packet number | 210 |

The server response was observed in packet 3155.

The response contained:
- HTTP status: `200 OK`
- Content type: `application/x-msdownload`
- Content length: `2,025,472` bytes

**Blue Team observation:**

The computer successfully requested an executable file from an external server, and the server returned executable content.

This activity is suspicious because unexpected executable downloads can introduce malware into a system.

However, the PCAP evidence alone does not prove that the file was opened or executed.

### 4.2 Repeated HTTP Communication

Repeated HTTP requests were observed between the investigated computer and the following external destination:

`66.171.248.178`

The associated domain was:

`bot.whatismyipaddress.com`

The requests used the following details:

| Field | Finding |
|---|---|
| Source IP | `10.4.10.132` |
| Destination IP | `66.171.248.178` |
| HTTP method | GET |
| Requested path | `/` |
| Response status | `200 OK` |
| Content type | `text/html` |
| Response content length | 14 bytes |

The requests occurred repeatedly at approximately 10-minute intervals.

The server successfully returned a small HTML response.

**Blue Team observation:**

The regular communication pattern may indicate an automated process running on the investigated computer.

This behaviour should be investigated because repeated external connections can sometimes be associated with unwanted software or automated communication.

However, this evidence does not independently confirm command-and-control activity.

## 5. Identified Security Concerns

The investigation identified the following areas requiring attention:

1. **Unexpected executable download:** An executable file was requested from an external server.
2. **Repeated external communication:** The computer repeatedly contacted `bot.whatismyipaddress.com` at regular intervals.
3. **Repeated DNS activity:** Queries for `bot.whatismyipaddress.com` and `macwinlogistics.in` occurred repeatedly.
4. **Potentially unwanted automated activity:** The regular timing of network requests should be investigated to identify the process responsible.

These observations are indicators for further investigation, not proof that every associated domain or IP address is malicious.

## 6. Blue Team Recommendations

Based on the evidence collected, the following defensive actions are recommended:

### 6.1 Investigate the Endpoint

- Examine the computer for the downloaded executable file.
- Check whether the file exists and determine whether it was executed.
- Review endpoint security alerts and system activity around the time of the download.
- Run an approved antivirus or endpoint security scan.

### 6.2 Monitor Network Connections

- Monitor repeated connections to the identified external IP addresses and domains.
- Investigate unusual communication occurring at regular intervals.
- Review DNS and HTTP logs for similar patterns on other computers.

### 6.3 Apply Network Protection

- Use firewall rules to restrict unauthorised outbound connections where appropriate.
- Use DNS filtering to investigate and manage suspicious domains.
- Alert security analysts when unexpected executable downloads are detected.

### 6.4 Improve Security Monitoring

- Monitor unusual downloads and repeated external requests.
- Correlate network activity with endpoint logs.
- Maintain regular security reviews to identify suspicious behaviour early.

Any blocking action should be based on further verification and organisational security policy.

## 7. Conclusion

The Blue Team investigation examined DNS and HTTP traffic from the HawkEye PCAP file using Wireshark.

The investigation identified an executable download request from `proforma-invoices.com` and repeated HTTP and DNS communication involving external destinations.

These activities represent potential security concerns and should be investigated further by examining the endpoint and correlating network evidence with system logs.

The findings demonstrate the importance of monitoring network traffic, identifying unusual communication patterns and responding to suspicious downloads before they can cause damage.

The investigation provides useful indicators for defensive monitoring, but the available packet capture does not independently confirm malware execution or command-and-control activity.
