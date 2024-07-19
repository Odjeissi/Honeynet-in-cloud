# Building a SOC + Honeynet in Azure
![Cloud Honeynet / SOC](htt.jpg)

## Introduction

In this project, I set up a mini honeynet in Azure. I connected logs from different sources into a Log Analytics workspace. Microsoft Sentinel uses this workspace to create attack maps, send alerts, and track incidents. First, I recorded security data from the vulnerable setup for 24 hours. Then, I added security measures to make it safer and recorded the data for another 24 hours. The results are shown below, highlighting these key metrics:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https.jpg)

The architecture of this project consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 Linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, and exposed to the internet. Both Windows and Linux VMs had their Network Security Groups (NSG) and built-in firewalls wide open, and all other resources were deployed with public endpoints visible to the Internet.

For the "AFTER" metrics, NSG was hardened by blocking ALL traffic except my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint.

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https.png)<br>
![Linux Syslog Auth Failures](https.png)<br>
![Windows RDP/SMB Auth Failures](https.png)<br>
![MSSQL Auth Failures](https.png)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics I used in the insecure environment for 24 hours:
<br/> Start Time 07-07-2024 8:27:34 PM
<br/>Stop Time 07-08-2024 8:27:34 PM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 63395
| Syslog                   | 3054
| SecurityAlert            | 56
| SecurityIncident         | 295
| AzureNetworkAnalytics_CL | 775

## Attack Maps After Hardening / Security Controls

```All map queries returned no results due to no instances of malicious activity for the 24 hours after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics I used in the insecure environment for another 24 hours, but after I applied security controls:
<br/> Start Time 07-15-2024 7:16:40 PM
<br/>Stop Time 07-16-2024 7:16:40 PM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 15187
| Syslog                   | 8
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was built in Microsoft Azure, and logs were sent to a Log Analytics workspace. Microsoft Sentinel was used to trigger alerts and create incidents from these logs. Metrics were recorded before and after implementing security measures in the insecure environment. The number of security events and incidents significantly decreased after applying the security measures, showing their effectiveness.

It is important to note that if the network resources had been heavily used by regular users, more security events and alerts might have been generated within the 24 hours following the implementation of the security controls.
