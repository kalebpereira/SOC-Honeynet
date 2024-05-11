# SOC-Honeynet (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/ZWxe03e.jpg)

## Introduction

In today's digitally connected landscape, cybersecurity is paramount. As technology advances, so too do the methods and sophistication of cyber threats. To confront these challenges head-on, I embarked on a comprehensive cybersecurity project leveraging Azure's robust infrastructure. The primary objective was to construct a miniature honeynet within Azure, comprising three distinct virtual machines: an Attack-VM, a Linux-VM, and a Windows VM. By deliberately exposing the Linux and Windows VMs to potential attacks, I aimed to simulate real-world cyber threats and analyze their impact.

## Project Overview

My project entailed orchestrating a series of strategic steps to fortify the Azure environment against potential cyber intrusions. Initially, I configured the virtual machines with minimal security measures, deliberately leaving them vulnerable to external threats. Subsequently, I meticulously monitored and logged various activities within the environment, utilizing Azure's Log Analytics workspace to consolidate data streams.

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

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/1qvswSX.png)<br>
![Linux Syslog Auth Failures](https://i.imgur.com/G1YgZt6.png)<br>
![Windows RDP/SMB Auth Failures](https://i.imgur.com/ESr9Dlv.png)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-05-07 2:19:55
Stop Time 2024-05-08 2:19:55

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 19551
| Syslog                   | 3746
| SecurityAlert            | 1
| SecurityIncident         | 410
| AzureNetworkAnalytics_CL | 2196

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2024-05-10 12:24:50
Stop Time	2024-05-11 12:24:50

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 9076
| Syslog                   | 5
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 21

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
