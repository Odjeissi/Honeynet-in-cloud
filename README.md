# Building a SOC + Honeynet in Azure
![image](https://github.com/user-attachments/assets/ba017083-0601-4069-8de3-cabb5c5474d8)


## Introduction

In this project, I created a small honeynet in Azure. I connected logs from different sources to a Log Analytics workspace. Then, I used Microsoft Sentinel to generate attack maps, send alerts, and track incidents. First, I collected security data from the vulnerable setup for 24 hours. Then, I implemented security measures to improve its safety and collected data for another 24 hours. The results are presented below, highlighting the key metrics.

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into honeynet)

## Architecture Before Hardening / Security Controls
![image](https://github.com/user-attachments/assets/f527f2f2-27b2-4469-81a5-cd7a26078e90)


## Architecture After Hardening / Security Controls
![image](https://github.com/user-attachments/assets/80a9cf6a-6ba3-4e43-9562-7034d55a7660)


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
![image](https://github.com/user-attachments/assets/ea84c954-caf2-4f39-951b-583f579d041a)<br> 
![image](https://github.com/user-attachments/assets/1675b551-5b89-4d80-b8a0-ab9985ccb822)<br>
![image](https://github.com/user-attachments/assets/2d732bef-8828-4138-9cd5-94438d4c12f1)<br>
![image](https://github.com/user-attachments/assets/490091ab-85c5-4136-892a-52b01cf8d085)<br>

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
