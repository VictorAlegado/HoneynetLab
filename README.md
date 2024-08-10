<h1>Honeynet Implementation and SIEM Threat Analysis in Azure</h1>

<h2>Description</h2>
In this project, I implemented a honeynet solution within Microsoft Azure which was operational for 24hrs to analyze and visualize cyber attack patterns to a virtual machine through brute force failed RDP (remote desktop protocol) requests around the world. The key objectives were to set up an isolated environment for capturing and analyzing malicious activity, and to leverage Azure’s native tools for detailed threat intelligence.
<br />

<h2>Overview</h2>
I created an Azure subscription to initiate the project environment, within Azure, I set up a virtual machine (VM) that will serve as the honeynet by disabling both external and Windows firewalls, exposing the VM to the internet. I established a log repository in Azure through Log Analytics Workspace to ingest failed RDP logs from the VM. Using PowerShell inside the VM, I automated the extraction of IP addresses from failed RDP requests via Windows Event Viewer and sent the data to a third-party API to derive latitude and longitude information. Finally, I configured Azure Sentinel, Azures cloud-native SIEM, to visualize the enrich the attacker data on a map. 
<br />
<br />
<img src="https://i.imgur.com/NliRmdI.png" height="80%" width="80%" alt="Overview"/>
<h2>Outcome</h2>
40,000+ API requests on failed RDP attempts into my honeynet virtual machine from over 20 different countries in only 24 hours indicates the threat level to any person or organization remains very high in regards to cybersecurity. Analysing the data from the failed RDP attempts indicates that these were mostly the result of a bots performing automated password-spraying brute force attacks. This is shown by the use of generic usernames such as "Admin", "Server", "User" within seconds of each attempt whilst coming from the same IP Addresses. It is essential to change default usernames, use strong passwords, configure and update firewalls to avoid being breached. 
<br />
<br />
<img src="https://i.imgur.com/rOEwXib.png" height="80%" width="80%" alt="Map"/>

<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Azure services - Virtual Machines, Log Analytics Workspace, Sentinel</b>
- <b>API Integration - ipgeolocation.io</b>
- <b>Network Utilities - Firewall and Port Configuration

<h2>Environments Used </h2>

- <b>Windows 10</b> 

<h2>Honeynet implementation walk-through:</h2>

<p align="center">
Virtual Machine Creation: Configured NSG Allow any traffic inbound <br/>
<img src="https://i.imgur.com/VXuLzCq.png" height="80%" width="80%" alt="1. Configure NSG Allow any inbound"/>
<br />
<br />
After creating Log Analytics Workspace, configured Defender to allow LAW to ingest logs from VM: <br/>
<img src="https://i.imgur.com/gdRQTv2.png" height="80%" width="80%" alt="Defender"/>
<br />
<br />
Inside Honeynet Virtual Machine, Disabled Firewalls:  <br/>
<img src="https://i.imgur.com/hHjsiXE.png" height="80%" width="80%" alt="2. Windows firewall Virtual Machine"/>
<br />
<br />
Using Powershell ISE script to create failed RDP log file and automate look up on attackers Geolocation information:  <br/>
<img src="https://i.imgur.com/bIjc4Lh.png" height="80%" width="80%" alt="Powershell"/>
<br />
<br />
Security Event Viewer Ip Addresses sent to 3rd party API to derive Geolocation:  <br/>
<img src="https://i.imgur.com/sgocHXv.png" height="80%" width="80%" alt="IPgeo"/>
<br />
<br />
Creating custom table on Azure to retrieve failed RDP logs from virtual machine  <br/>
<img src="https://i.imgur.com/WzNo4c3.png" height="80%" width="80%" alt="Custom Table"/>
<br />
<br />
Creating query to parse data from failed RDP logs in Log Analytics Workspace:  <br/>
<img src="https://i.imgur.com/rTu2LN7.png" height="80%" width="80%" alt="Query"/>
<br />
<br />
Adding query in Sentinel to plot log data through map visualization:  <br/>
<img src="https://i.imgur.com/hu0mfiw.png" height="80%" width="80%" alt="Map Query"/>
<br />
<br />
Configure Map by latitude/longitude, event count<br/>
<img src="https://i.imgur.com/ZPnYZNM.png" height="40%" width="40%" alt="Map Config"/>
<br />
<br />
Threat Intelligence Map Created with Failed RDP logs from honeynet VM<br/>
<img src="https://i.imgur.com/rOEwXib.png" height="80%" width="80%" alt="Map"/>
<br />
<br />
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
