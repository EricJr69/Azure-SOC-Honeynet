# Azure-SOC-Honeynet

# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/ZWxe03e.jpg)

## Introduction

In this project, I deployed a mini honeynet in Azure, collecting log data from various sources into a Log Analytics workspace. Microsoft Sentinel was then used to create attack maps, alerts, and incidents. To demonstrate the effectiveness of security controls, I measured key metrics in an insecure environment, applied security hardening measures, and re-measured the metrics after 24 hours:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, resources were deployed with open Network Security Groups, built-in firewalls, and public endpoints, exposing them to the internet.

For the "AFTER" metrics, security was enhanced by restricting Network Security Groups to allow only admin workstation traffic, and activating built-in firewalls and Private Endpoints for all resources.

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/1qvswSX.png)<br>
![Linux Syslog Auth Failures](https://i.imgur.com/G1YgZt6.png)<br>
![Windows RDP/SMB Auth Failures](https://i.imgur.com/ESr9Dlv.png)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-11-13 17:12:43
Stop Time  2024-11-14 17:12:43

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 21247
| Syslog                   | 9227
| SecurityAlert            | 6
| SecurityIncident         | 326
| AzureNetworkAnalytics_CL | 3328

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2024-11-14 19:42:17
Stop Time	 2024-11-15T19:42:17

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 5468
| Syslog                   | 35
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

This project demonstrated the value of security controls in a cloud-based environment. A mini honeynet was built in Microsoft Azure, and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents. Key findings included a significant reduction in security events and incidents after applying security controls, underscoring their importance.

In a scenario where the network resources were heavily utilized by regular users, it's likely that the implementation of security controls would have resulted in an even greater number of security events and alerts being triggered during the 24-hour period.
