# Purple Team Report

## 1. Introduction

The purpose of the Purple Team exercise is to connect the activities identified by the Red Team with the security detections created by the Blue Team.

This helps us understand whether suspicious activities can be detected and how the organization's security can be improved.

## 2. Red Team and Blue Team Findings

During the investigation, the following suspicious activities were identified:

| Red Team Finding | Blue Team Detection Focus |
|---|---|
| Executable file downloaded from `217.182.138.150` | Detecting suspicious file downloads |
| Repeated requests to `66.171.248.178` | Detecting repeated connections to suspicious IP addresses |
| Repeated DNS requests to unusual domains | Detecting suspicious DNS activity |

These findings help connect the attacker's activities with the security team's monitoring efforts.

## 3. Detection Gaps

The investigation highlights some areas where security monitoring can be improved:

1. Suspicious downloads should be investigated immediately.
2. Repeated connections to suspicious IP addresses should generate alerts.
3. Unusual DNS requests should be monitored carefully.
4. Security alerts should contain enough information to help investigators understand the activity.
5. Different security logs should be reviewed together to identify related suspicious activities.

## 4. Recommended Improvements

To improve security detection, the following actions are recommended:

- Create detection rules for downloads from suspicious sources.
- Monitor repeated connections to known suspicious IP addresses.
- Create alerts for unusual DNS requests.
- Maintain an updated list of suspicious IP addresses and domains.
- Review detection rules regularly to improve their accuracy.
- Reduce false alerts by testing rules against normal network activity.

## 5. Incident Response Recommendations

If similar suspicious activity is detected in the future, the Blue Team should:

1. Investigate the suspicious IP address or domain.
2. Check whether any suspicious files were downloaded.
3. Review network and system logs.
4. Isolate affected systems if there is evidence of compromise.
5. Remove malicious files and block confirmed malicious connections.
6. Document the incident and take steps to prevent it from happening again.

## 6. Purple Team Improvement Plan

| Area | Recommended Action |
|---|---|
| File Monitoring | Improve detection of suspicious downloads |
| Network Monitoring | Monitor repeated connections to suspicious IPs |
| DNS Monitoring | Detect unusual domain requests |
| Detection Rules | Regularly test and improve security rules |
| Investigation | Connect different security logs |
| Team Collaboration | Share findings between Red and Blue Teams |

## 7. Conclusion

The Purple Team exercise helped connect the attack activities identified by the Red Team with the monitoring and detection efforts of the Blue Team.

It also highlighted areas where security monitoring, detection rules, and incident response can be improved.

Working together, Red and Blue Teams can help identify weaknesses, improve detection capabilities, and strengthen an organization's overall security.
