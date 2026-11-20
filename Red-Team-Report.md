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
| MITRE ATT&CK | Mapping observed behaviour to known attacker
