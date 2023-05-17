# Azure-Soc
# Building a SOC + Honeynet in Azure (Live Traffic)
## Introduction

The aim of this project was to create a more secure environment for a mini honeynet in Microsoft Azure by implementing access control rules and following NIST SP 800-53 guidelines. To achieve this goal, I integrated log sources from various resources into a Log Analytics workspace and used Microsoft Sentinel to set up alerts and create incidents based on the ingested logs. In the initial phase of the project, I measured security metrics in the insecure environment for 24 hours to establish a baseline. I then applied security controls to harden the environment and measured the metrics again for another 24 hours. The results were impressive, with a drastic reduction in the number of security events and incidents, demonstrating the effectiveness of the security measures in reducing the system's vulnerability to cyber-attacks. In the following sections, I will provide a detailed overview of the project's architecture, security controls, and the metrics used to evaluate the system's security posture.

## Metrics Gathered

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture of the Project

![Architecture](https://i.imgur.com/TVs8Epc.jpg)

## Tools, Technology and Regulations Utilized

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel
- Microsoft Defender for Cloud
- Windows RDP
- Syslog
- Windows Event Viewer
- Powershell
- KQL
- NIST SP 800-53

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
Start Time 2023-05-08 1:48 PM EST
Stop Time 2023-05-09 1:48 PM EST

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
Start Time 2023-05-09 6:01 PM EST
Stop Time	2023-05-10 6:01 PM EST


| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8778
| Syslog                   | 25
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, I built a mini honeynet in Microsoft Azure and integrated log sources from various resources into a Log Analytics workspace. Using Microsoft Sentinel, I set up alerts and created incidents based on the ingested logs. I measured some security metrics in the insecure environment for 24 hours, applied security controls to harden the environment, and measured the metrics again for another 24 hours. One of the most significant achievements of this project was the drastic reduction in the number of security events and incidents after implementing the security controls. This clearly demonstrates the effectiveness of the security measures in reducing the system's vulnerability to cyber attacks.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 48-hour period following the implementation of the security controls. Overall, this project aimed to create a more secure state for the endpoints by implementing access control rules and following NIST SP 800-53 guidelines. The changes greatly improved the security posture of the system, making it less vulnerable to cyber attacks.

## Credit

This project was based on a course developed by Josh Madakor and can be found here: [leveld](https://www.leveldcareers.com/cyber-security-course)
