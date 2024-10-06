<h1>Enable Log Collection for VMs and Network Security Groups</h1>

- <b>This tutorial outlines the configuration of storage accounts, network security groups, and log analytics workspace</b>

<h2>Environments and Technologies Used</h2>

- <b>Microsoft Azure</b> 
- <b>Storage Accounts</b>
- <b>Network Security Groups</b>
- <b>Log Analytics Workspace</b>

<h2>Operating Systems</h2>

- <b>Windows 10</b>


<h2>Configuration Steps</h2>

![image](https://github.com/user-attachments/assets/dcf97a04-8e03-4402-94cd-d055e5e7ea63)
- <b>Navigate to storage accounts and click create storage account</b>
- <b>Resource Group: RG-Cyber-Lab</b>
- <b>Storage account name: sacyberlab1234</b>
- <b>Region EAST US 2</b>
- Click Review + create</b>

![image](https://github.com/user-attachments/assets/301921dc-6e22-48d4-ba32-4a39cebf751d)
- <b>Navigate to Network Security Groups</b>
- <b>Select linux-vm-nsg</b>
- <b>Select settings and NSG flow logs</b>
- <b>Click create flow log</b>

![image](https://github.com/user-attachments/assets/45f7ef39-798c-4450-8a90-53b0be3d786b)
- <b>Click "Select target resource"</b>
- <b> Select both linux-vm-nsg and windows-vm-nsg and confirm selection</b>

![image](https://github.com/user-attachments/assets/45589b5f-22e2-45cd-9d0b-7ec81e8b6770)
- <b>Retention (days): 60

![image](https://github.com/user-attachments/assets/7b6833f9-ad33-4287-9515-912ab7becd02)
- <b>Enable traffic analytics</b>
- <b>Choose every 10 mins and review + create</b>

![image](https://github.com/user-attachments/assets/889c49f6-b4f2-4bb4-95de-84b8be293fd6)
- <b>Navigate to Microsoft Sentinel and select content hub</b>

![image](https://github.com/user-attachments/assets/d0a18263-5a9b-48c1-8f53-29a127f52856)
- <b>Select Windows Security Events and click install</b>

![image](https://github.com/user-attachments/assets/564677d9-a72b-40f9-9dc5-d8a1aefb910e)
- <b>Select Windows Security Events and click manage</b>
- <b>Select Windows Security Events via AMA</b>
- <b>Open connector page</b>

![image](https://github.com/user-attachments/assets/d5b08a3b-03e9-49f1-95c2-464a9ac0a2a6)
- <b>Create data collection rule</b>
- <b>Rule Name: DCR-Windows</b>
- <b>Subscription: Azure Subscription 1</b>
- <b>Resource Group: RG-Cyber-Lab</b>
- <b> Click Next: Resources</b>

![image](https://github.com/user-attachments/assets/c1991416-f0e7-4131-8f3c-a8086bbcb135)
- <b>Click add resource(s)</b>
- <b>Select windows-vm</b>

![image](https://github.com/user-attachments/assets/aec6fceb-4720-41bb-a206-aef2d3448679)
- <b>AzureMonitorWindowsAgent is created</b>

![image](https://github.com/user-attachments/assets/9e0e63d8-c64b-4e22-b16e-0c6bfd4fd01b)
- <b>Navigate to Microsoft Sentinel</b>
- <b>Select content hub under content management</b>
- <b>Select Syslog and click install</b>

v![image](https://github.com/user-attachments/assets/397142b1-aac7-4405-aeeb-97d9449b1cdb)
- <b>Select Syslog and click manage</b>
- Select Syslog via AMA and open the connector page</b>

![image](https://github.com/user-attachments/assets/7a11e380-1cf6-443e-a387-75ca44dbd53b)
- <b>Click create data collection rule</b>
- <b>Rule name: DCR-Linux</b>
- <b>Subscription: Azure Subscription 1</b>
- <b>Resource Group: RG-Cyber-Lab</b> 

![image](https://github.com/user-attachments/assets/e24967d3-55f8-489d-ab93-d8c689c09671)
- <b>Select linux-vm</b>

![image](https://github.com/user-attachments/assets/207040da-8650-4547-8581-85f4accb73ee)
- <b>Select LOG_AUTH: LOG_DEBUG and click review + create</b>

![image](https://github.com/user-attachments/assets/7881fe74-1806-4a11-9dc2-57e2668c7995)
- <b>AzureMonitorLinuxAgent is created
  
![image](https://github.com/user-attachments/assets/d95259b9-d33e-4ef3-963c-02d6e5c4f9a7)
- <b>Navigate to Log Analytics Workspace</b>
- <b>Query AzureNetworkAnalytics_CL</b>

![image](https://github.com/user-attachments/assets/b21d3a7b-b7a9-4593-ad08-f07d0d295047)
- <b>Perform 3 login attempts on your linux-vm using Windows PowerShell from your host computer</b>

![image](https://github.com/user-attachments/assets/c4c92cf0-96c2-4fc1-993a-cfeb330e4231)
- <b> - <b>Perform 3 login attempts on your windows-vm using Remote Desktop connection from your host computer</b>

![image](https://github.com/user-attachments/assets/13103471-5230-4c25-becd-f8a4f80af84f)
- <b>Navigate to Log Analytics Workspace and view the failed login attempts for the windows-vm under logs using this query command:
``` 
SecurityEvent
| where EventID == 4625
| where TimeGenerated desc
| where EventID == 4625
``` 
![image](https://github.com/user-attachments/assets/d548ea01-560c-4eb9-b9ef-5df9064b53e1)
- <b>Use this query to view the failed login attempts for the linux-vm:</b>
``` 
Syslog
| where SyslogMessage startswith "Failed password for invalid user"
``` 
