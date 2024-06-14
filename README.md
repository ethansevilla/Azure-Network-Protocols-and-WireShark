<p align="center">
  <img src="https://i.imgur.com/Ua7udoS.png" height="80%" width="80%" alt="Ubuntu VM" alt="Traffic Examination"/>
</p>
<h1>Network Security Groups and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />
<!-- <h2>Video Demonstration</h2>
- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com) -->
<h2>Environments and Technologies Used</h2>
- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (ICMP, SSH, RDP, DNS, HTTP/S)
- Various Network Protocols (ICMP, SSH, DHCP, DNS, RDP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>
- Windows 10 (21H2)
- Ubuntu Server 20.04
<h2>High-Level Steps</h2>
- Create Resources
- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic
<h2>Actions and Observations</h2>
</br>
</br>
<h3 align="center">
  Set up your virtual environment
</h3>
</br>
<p>
  Create a Resource Group:
</p>
<p>
  <img src="https://github.com/ethansevilla/Azure-Network-Protocols-and-WireShark-/assets/170621372/fbc7ba65-c875-4201-98b8-8635bba2d09b"/>
</p>
<p>
  Create a Windows virtual machine.
</p>
<p>
  While creating the VM, select the previously created Resource Group(RG-Networks) and allow it to create a new Virtual Network (Vnet) and Subnet. Make sure to use the password option under the <strong>Administrator Account</strong> section (not seen in image):
</p>
<p>
  <img src="https://github.com/ethansevilla/Azure-Network-Protocols-and-WireShark-/assets/170621372/5402e424-eff5-42d0-be57-0ea553bb4f98"/>
</p> 
<p> 
  <img src = "https://github.com/ethansevilla/Azure-Network-Protocols-and-WireShark-/assets/170621372/2594d0ed-2c27-45e7-a796-c21f1cd9ff03"/>
</p> 
<p>
  Create an Ubuntu virtual machine.
</p>
<p>
  While creating the VM, select the previously created Resource Group and allow it to create a new Virtual Network (Vnet) and Subnet. Instead of using SSh key, we create a password option under the <strong>Administrator Account</strong> section :
</p>
<p>
  <img src="https://github.com/ethansevilla/Azure-Network-Protocols-and-WireShark-/assets/170621372/ef43792d-eb02-446d-843e-c415197c6116"/>
</p> 
<p>
  <img src= "https://github.com/ethansevilla/Azure-Network-Protocols-and-WireShark-/assets/170621372/94a07b8d-8988-47cd-b260-3b20043ad3a9" />
</p>
<p>
  Observe Your Virtual Network topology within Network Watcher:
</p>
<p>
  <img src="https://github.com/ethansevilla/Azure-Network-Protocols-and-WireShark-/assets/170621372/2ee4cd57-b146-4af4-afe8-498356652f43"/>
</p>
<br />
<br />
<h3 align="center">
 Observe ICMP traffic
</h3>
<br />
<p>
  Go remote desktop access into your Windows 10 Virtual Machine, install Wireshark, open it and filter for ICMP traffic only. If you are using a Mac , you'll have to download <strong><a href="https://apps.apple.com/us/app/microsoft-remote-desktop/id1295203466?mt=12">Microsoft Remote Desktop</a></strong> from the app store:
</p> 
<p>
  <img src="https://github.com/ethansevilla/Azure-Network-Protocols-and-WireShark-/assets/170621372/b01bd3a2-96bc-4c5c-9d37-8693e77271d7"/>
</p> 
<p>
  <img src= "https://github.com/ethansevilla/Azure-Network-Protocols-and-WireShark-/assets/170621372/6a6ae78d-1bf9-4f12-a852-6466ce636122" />
</p>
<p>
  Retrieve the private IP address of the Ubuntu VM back in Azure portal and attempt to ping it from within the Windows 10 VM. Observe ping requests and replies within WireShark:
</p>
<p>
  <img src="https://github.com/ethansevilla/Azure-Network-Protocols-and-WireShark-/assets/170621372/3552c6d5-3361-4282-b658-0510091d92fa"/>
  <img src="https://github.com/ethansevilla/Azure-Network-Protocols-and-WireShark-/assets/170621372/78bda900-8091-4fb1-9bd5-96e7cc2e4015"/>
</p>
<p>
  Attempt to ping a public website (such as www.bing.com) and observe the traffic in WireShark:
</p>
<p>
  <img src="https://github.com/ethansevilla/Azure-Network-Protocols-and-WireShark-/assets/170621372/6ebc0d0b-d2d4-40f5-81e2-b48985860a1a"/>
</p>
<p>
  Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM:
</p>
<p>
  <img src="https://github.com/ethansevilla/Azure-Network-Protocols-and-WireShark-/assets/170621372/af41aec2-a373-408d-b1c7-db31d85b63bf"/>
</p>
<p>
  Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic, while back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity:
</p>
<p>
  <img src="https://github.com/ethansevilla/Azure-Network-Protocols-and-WireShark-/assets/170621372/e90f44dc-e26e-49a8-9c68-d8b26b10c637"/>
  <img src="https://github.com/ethansevilla/Azure-Network-Protocols-and-WireShark-/assets/170621372/81828284-89cb-4630-9aa3-fbc9102fc96d"/>
</p>
<p>
  Re-enable ICMP traffic for the Network Security Group in your Ubuntu VM and back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line ping activity (should start working again).Finally, stop the ping activity:
</p>
<p>
  <img src="https://github.com/ethansevilla/Azure-Network-Protocols-and-WireShark-/assets/170621372/0e30aad1-42d2-49d8-af02-df090d392b45"/>
</p> 
<p>
  <img src= "https://github.com/ethansevilla/Azure-Network-Protocols-and-WireShark-/assets/170621372/69eb0f58-7350-4afc-be70-9757869d6d2b" />
</p>
<br />
<br />
<h3 align="center">
  Time to observe SSH traffic
</h3>
<br />
<p>
  Back in Wireshark, filter for SSH traffic only and from your Windows 10 VM, “SSH into” your Ubuntu virtual machine (via its private IP address). Type commands (ls, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark.
</p>
</p>
  Exit the SSH connection by typing ‘exit’ and pressing [return]:
</p>
  <img src="https://github.com/ethansevilla/Azure-Network-Protocols-and-WireShark-/assets/170621372/4ff48143-d598-4f7f-9ab0-263c039db10d"/> 
<p>
  <img src= "https://github.com/ethansevilla/Azure-Network-Protocols-and-WireShark-/assets/170621372/b8614537-7b98-454e-8c86-47127bbab585"/>
</p>
<p>
<br />
<br />
<h3 align="center">
  Observe DHCP Traffic 
</h3>
<br />
<p>
  Back in Wireshark, filter for DHCP traffic only. From your Windows 10 VM, attempt to issue your VM a new IP address with the command line (ipconfig /renew)
</p>
Observe the DHCP traffic appearing in WireShark:
</p>
<p>
  <img src="https://github.com/ethansevilla/Azure-Network-Protocols-and-WireShark-/assets/170621372/978f1f3a-65a4-401f-9aa6-419fdf35f76f"/>
</p>
<br />
<br />
<h3 align="center">
  Observe DNS traffic next part
</h3>
<br />
<p>
  Back in Wireshark, filter with DNS traffic only.
</p>
<p>
  From your Windows 10 VM within a command line, use nslookup command to see what google.com and disney.com’s IP addresses are and observe the DNS traffic being shown in WireShark:
</p>
<p>
  <img src="https://github.com/ethansevilla/Azure-Network-Protocols-and-WireShark-/assets/170621372/268b974b-b67e-491b-a47b-5f9ee84ea7b5"/>
</p>
<br />
<br />
<h3 align="center">
  And now we will observe RDP traffic to finish up this lab
</h3>
<br />
<p>
  Back in Wireshark, filter for RDP traffic only which is (tcp.port == 3389).
</p>
<p>
  OBserve the non-stap spam 
</p>
<p>
  This id due to the RDP (protocol) constantly showing a live stream from one computer to another, therefore traffic is always being transmitted:
</p>
<p>
  <img src="https://github.com/ethansevilla/Azure-Network-Protocols-and-WireShark-/assets/170621372/86e26f64-5cf5-4786-9b34-79d3f5f28685"/>
</p>
<br />
<br />
<p>
  I hope this tutorial has helped you learn more about network security protocols and how traffic is seen between virtual machines.
</p>
<p>
  And before finishing, DON'T FORGET TO CLEAN UP YOUR AZURE ENVIRONMENT and delete VM's and Resource Groups so that you don't incur unnecessary charges.
</p>
<p>
  Close your Remote Desktop connection, delete the Resource Group(s) created at the beginning of this tutorial, and verify Resource Group deletion.
</p>
