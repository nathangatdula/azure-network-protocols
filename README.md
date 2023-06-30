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

Now copy and paste VM1's public IP address into Remote Desktop Control and login with the credentials used in making VM1.
<p>
<img src="https://i.imgur.com/p7TjN7W.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/UzKOLMz.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
Once logged into VM1, search up "wireshark download" in a web browser and download Wireshark with all the default settings. 
</p> 
<img src="https://i.imgur.com/ZHGR4Bl.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
Open Wireshark. The first protocol we will observe is ICMP, so first press the blue fin symbol by the text line, then type in "icmp" and hit enter.
</p>
<img src="https://i.imgur.com/p9aTg0N.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
Get VM2's private IP address from Azure and perpetually ping it from the command line in VM1 by using the command: ping 10.0.0.5 -t
<p>
See that Wireshark is showing requests from VM1 and replies from VM2 which means VM1 is successfully pinging and getting replies back from VM2
</p>
<img src="https://i.imgur.com/b8YjSD2.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<p>
<img src="https://i.imgur.com/swlBr1t.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<p>
  
</p>
We will now block any inbound ICMP traffic from VM2's networking settings in Azure. From VM2's networking settings, press "Add inbound port rule".
</p>
<img src="https://i.imgur.com/gRX8ofJ.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<p>
Select ICMP under Protocol
</p>
<img src="https://i.imgur.com/SmUeant.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
Under "Action" select Deny and set the priority to 250. (Priority works in numerical order, so for this demonstration it will be prioritized before anything else in the rules.) Click Save
<p>
<img src="https://i.imgur.com/y6xfupt.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
Going back to VM1, we can now see that in the command line as well as Wireshark, VM2 has blocked VM1's ping. Ping uses ICMP which is why in Wireshark, it only shows the ping requests from VM1 and no replies from VM2.
<p>
<img src="https://i.imgur.com/KFTcqEh.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
Now to enable ICMP traffic back to VM2, go back to VM2's networking settings in Azure, click on the new rule that we created, select Allow instead of Deny under "Action", then press save. After some time, you can see that VM2 is now sending replies back to Wireshark and the command prompt.
<p>
<img src="https://i.imgur.com/FNGOmpk.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/s035fBU.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
You can also ping different websites and it should send replies, for example with google:
<p>
<img src="https://i.imgur.com/02JUEy8.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<br />
<p>
The next protocol we will observe is SSH. In the command line, type in "ssh 10.0.0.5" with the IP address being the private IP address of VM2. This lets you connect to VM2 through the command line, similar to the Remote Desktop Connection we are currently using but with no image. It will ask you if you want to continue connecting, so type "yes". You will be asked for the password to connect to VM2 which is the password you created while making VM2. It will not show when you type in your password, but once you type it in, press enter. You will now be connected to VM2 in the command line. To exit, simply type "exit".
<p>
<img src="https://i.imgur.com/ElYD5s8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
