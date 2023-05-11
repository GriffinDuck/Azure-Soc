# Azure-Soc
# Building a SOC + Honeynet in Azure (Live Traffic)
## Introduction

In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below.

## Metrics Gathered

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture of the Project

![Architecture](https://i.imgur.com/TVs8Epc.jpg)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/v03nG2p.jpg)

This architecture represents the insecure state of the system prior to implementing security controls. It was completely exposed to the internet, with both Network Security Groups and built-in firewalls set to allow all traffic. Access control rules were created to allow unrestricted communication between network endpoints. In addition, all other resources were deployed with public endpoints visible to the internet, without using any Private Endpoints

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/GGQ5zhO.jpg)

This architecture represents a more secure state of the system after implementing security controls. Access control rules were put in place to block all traffic except for that from my home device. To comply with the Boundary Protection section of NIST SP 800-53, I followed the compliance section of Microsoft Defender and created a Virtual Network and Subnet. This change made all resources into private endpoints.

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/pjUb6BH.png)<br>
![Linux Syslog Auth Failures](https://i.imgur.com/Nr9MOXK.png)<br>
![Windows RDP/SMB Auth Failures](https://i.imgur.com/ZVRdkMm.png)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-05-08T17:01:48
Stop Time 2023-05-09T17:01:48

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 34495
| Syslog                   | 5360
| SecurityAlert            | 2
| SecurityIncident         | 296
| AzureNetworkAnalytics_CL | 699

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-05-09T21:06:01
Stop Time	2023-05-10T21:06:01


| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8778
| Syslog                   | 25
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastially reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
