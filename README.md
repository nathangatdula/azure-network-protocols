<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer) 

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create two Azure virtual machines
  - Virtual Machine #1 using Windows 10
  - Virtual Machine #2 using Ubuntu (Linux)
- Through Remote Desktop Connection, log into Virtual Machine #1 and download Wireshark
- Observe different types of network protocols with Command Prompt or Powershell and Wireshark 
  - Manipulate Virtual Machine #2's Network to DENY/ALLOW ICMP
- Display and flush DNS cache

<h2>Actions and Observations</h2>

<p>

</p>
<p>
First of all, in Azure create both of your virtual machines:

  - Virtual Machine #1 (VM1)
    - Windows 10 Version 22H2
    - 2 vcpu's and 16 GiB of memory
    - Username: labuser (or whatever you prefer)
    - Password: Labpassword1 (or whatever you prefer)
<img src="https://i.imgur.com/dBBDzSI.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/SUlZPHS.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
Observe in the Network tab of the process of creating VM1 that the VM creates its own Virtual Network
</p>
<img src="https://i.imgur.com/08VKnEj.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>

- Virtual Machine #2 (VM2)
  -  Ubuntu (Linux)
  -  2 vcpu's and 16 GiB of memory
  -  Set the Authentication type to Password
  -  Username: labuser (or whatever you prefer)
  -  Password: Labpassword1 (or whatever you prefer)

</p>
<img src="https://i.imgur.com/5hgzQPn.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/hzbxAYG.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

</p>
In the Network tab while creating VM2, check to make sure that VM2 is using the same virtual network as VM1
</p>
<img src="https://i.imgur.com/VC1zjkt.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<br />
</p>
Now copy and paste VM1's public ip address into Remote Desktop Control and login with the credentials used in making VM1.
<p>
<img src="https://i.imgur.com/p7TjN7W.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/UzKOLMz.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/DJmEXEB.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/DJmEXEB.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
