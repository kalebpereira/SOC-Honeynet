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

In the refined architecture post-hardening, a robust framework was established to fortify the Azure-based honeynet against potential cyber intrusions. The components of the enhanced architecture included:

- Virtual Network (VNet): The Virtual Network served as the foundational framework for hosting the interconnected resources of the honeynet. Through meticulous configuration and segmentation, network traffic was carefully controlled to enhance security posture.
- Network Security Group (NSG): Following the implementation of stringent security measures, the NSG underwent significant hardening. Traffic was meticulously filtered, with access restricted to essential entities, notably excluding unauthorized sources and potential threat vectors.
- Virtual Machines (2 windows, 1 linux): The virtual machines within the honeynet underwent comprehensive security enhancements. Both Windows and Linux-based systems were shielded behind fortified Network Security Groups and reinforced with robust built-in firewalls.
- Log Analytics Workspace: The Log Analytics Workspace continued to serve as the central repository for logging and monitoring activities within the honeynet. Enhanced security protocols ensured that all pertinent log data was meticulously analyzed to detect and respond to potential security incidents swiftly.
- Azure Key Vault: To safeguard critical cryptographic keys and secrets, Azure Key Vault played a pivotal role in the fortified architecture. Access controls were rigorously enforced to prevent unauthorized access and ensure the integrity of sensitive information.
- Azure Storage Account: The Azure Storage Account, an essential component of the honeynet architecture, was fortified with stringent access controls and encryption mechanisms. Data-at-rest and data-in-transit were safeguarded to mitigate potential data breaches.
- Microsoft Sentinel: As the primary tool for threat detection and incident response, Microsoft Sentinel assumed an elevated role in the fortified architecture. Advanced analytics and machine learning capabilities were leveraged to proactively identify and mitigate emerging cyber threats.

All resources were initially delivered with wide-open configurations during the "BEFORE" metrics phase, making them vulnerable to possible cyber attacks.  In the "AFTER" metrics phase. Network security groups were strengthened to prevent access from any non-essential source, with carefully defined exceptions that allowed access only from sources that were permitted. In addition, strict firewall regulations were put into place and resources were hidden behind Private Endpoints , which significantly reduced the possibility of unwanted access and strengthened the honeynet's overall security posture. For example, one of these Firewall regulations was limiting access through whitelisting the VMs to only my local IP address.

## Number of Incidents Before Hardening / Security Controls 

<img width="1440" alt="# of Incidents (Before)" src="https://github.com/kalebpereira/SOC-Honeynet/assets/169097865/773a3b19-ee4a-4d4e-b849-06a51733ed9a">


## Attack Maps Before Hardening / Security Controls
<img width="1440" alt="nsg-malicious-allowed-in (before)" src="https://github.com/kalebpereira/SOC-Honeynet/assets/169097865/f4c127f5-b55c-41d6-a522-3c2e29d37c61">
<img width="1440" alt="linux-ssh-auth-fail (before)" src="https://github.com/kalebpereira/SOC-Honeynet/assets/169097865/42229ba1-3415-452e-831d-07f988f4c2b6">
<img width="1440" alt="windows-rdp-auth-fail (before)" src="https://github.com/kalebpereira/SOC-Honeynet/assets/169097865/7c1d1f8e-e369-4dfa-83c6-a8c6cb66750b">

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

## Number of Incidents After Hardening / Security Controls 

<img width="1440" alt="# of Incidents (after)" src="https://github.com/kalebpereira/SOC-Honeynet/assets/169097865/b17c9fb3-2629-4b70-a0f1-0a06f9674922">

## Attack Maps After Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

<img width="562" alt="Screenshot 2024-05-11 at 3 41 30 PM" src="https://github.com/kalebpereira/SOC-Honeynet/assets/169097865/db025ecf-653d-41f7-91cd-1ba3542b457a">


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

## % Reduction in Incidents/Alerts After Hardening/Security Controls 

<img width="524" alt="Screenshot 2024-05-11 at 4 20 15 PM" src="https://github.com/kalebpereira/SOC-Honeynet/assets/169097865/a7224e56-c73a-46fb-a38d-4e0afb1a9f4d">


## Key Components and Actions 

Virtual Machine Setup: Within the Microsoft Azure environment, I provisioned three distinct virtual machines: an Attack-VM, a Linux-VM, and a Windows VM. These machines were strategically deployed to emulate various components of a network, facilitating the simulation of real-world cyber threats.

Security Configuration: To replicate authentic cybersecurity scenarios, deliberate measures were taken to disable Network Security Groups (NSGs) and firewalls within the Linux and Windows VMs' operating systems. This deliberate vulnerability enabled comprehensive analysis of potential security breaches and facilitated the collection of pertinent log data.

Log Analysis and Incident Response: Leveraging the robust capabilities of Azure's Log Analytics workspace and Microsoft Sentinel, I meticulously analyzed the generated logs from the vulnerable VMs. Adhering to established industry standards, including NIST 800-53 guidelines, I promptly identified and responded to potential security incidents, initiating remediation procedures to mitigate risks effectively.

Security Metrics and Evaluation: Over a meticulously observed 48-hour period, I meticulously measured and evaluated various security metrics. These metrics encompassed SecurityEvent (Windows Event Logs), Syslog (Linux Event Logs), SecurityAlert (Log Analytics Alerts Triggered), SecurityIncident (Incidents created by Sentinel), and AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet). These metrics provided critical insights into the effectiveness of the implemented security measures and served as benchmarks for evaluating system hardening efforts.

## Conclusion

This project underscores the critical importance of proactive cybersecurity measures in safeguarding digital assets within cloud environments, exemplified through the construction and analysis of a miniature honeynet in Microsoft Azure. By systematically orchestrating the integration of log sources into a Log Analytics workspace and leveraging Microsoft Sentinel for alerting and incident response, I successfully demonstrated the tangible benefits of implementing robust security controls.

Moreover, the observed reduction in security events and incidents following the implementation of security measures highlights the efficacy of proactive cybersecurity strategies. Moving forward, the insights gained from this project will serve as a foundation for enhancing cybersecurity practices, fortifying Azure environments, and effectively mitigating evolving cyber threats.
