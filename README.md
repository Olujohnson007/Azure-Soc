
# Building a SOC + Honeynet in Azure (Live Traffic)
![image](https://github.com/Olujohnson007/Azure-Soc/assets/169572108/af88d0c7-7698-47f6-b2d3-0aae20b4cc70)


## Introduction

In this initiative, I developed a compact honeynet on the Azure platform and aggregated log data from various sources into a Log Analytics workspace. This setup facilitated the use of Microsoft Sentinel for constructing attack visualizations, triggering security alerts, and generating incident reports. I quantified specific security metrics within an unsecured environment over a 24-hour period, implemented targeted security controls to strengthen the system's defenses, and then reassessed these metrics for an additional 24 hours. The following sections detail the comparative results of these metrics:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![image](https://github.com/Olujohnson007/Azure-Soc/assets/169572108/667cbd4e-cbd9-4739-b4a3-90bcc481d358)

## Architecture After Hardening / Security Controls
![image](https://github.com/Olujohnson007/Azure-Soc/assets/169572108/c7950b4b-84ab-430d-8435-6c5de977c23b)


The architecture of the honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were initially deployed and exposed to the internet. The Virtual Machines were configured with their Network Security Groups (NSGs) and built-in firewalls set to allow all traffic, and all other resources were deployed with public endpoints, meaning they were directly accessible from the internet without Private Endpoints.

For the "AFTER" metrics, the security posture was significantly enhanced. Network Security Groups were tightened to block all traffic except that from my admin workstation. Additionally, all resources were safeguarded using their built-in firewalls and by implementing Private Endpoints, effectively isolating them from direct public access.

## Attack Maps Before Hardening / Security Controls
![image](https://github.com/Olujohnson007/Azure-Soc/assets/169572108/fba03c31-ab91-49de-8c30-1473bdc9598f)

![image](https://github.com/Olujohnson007/Azure-Soc/assets/169572108/c4b8f000-de97-4791-ac0e-c477f5cba516)

![image](https://github.com/Olujohnson007/Azure-Soc/assets/169572108/7b356797-3111-4cbb-b438-6f41f55a79fc)


## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-05-06T15:56:11.0799413Z
Stop Time 2024-05-07T15:56:11.0799413Z

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 54931
| Syslog                   | 3498
| SecurityAlert            | 4
| SecurityIncident         | 258
| AzureNetworkAnalytics_CL | 1031

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 8/5/2024 2:02:06
Stop Time	9/5/2024 2:02:06

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 2779
| Syslog                   | 5
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a compact honeynet was set up in Microsoft Azure, and log sources were aggregated into a Log Analytics workspace. Utilizing Microsoft Sentinel, the system was configured to generate alerts and incidents from the collected logs. Security metrics were evaluated in the environment before and after the application of security controls. Notably, there was a significant reduction in the number of security events and incidents post-implementation, underscoring the efficacy of these controls.

It is important to mention that if the network's resources had been extensively used by regular users, it is plausible that an increased number of security events and alerts could have been observed within the 24-hour period following the implementation of security measures.
