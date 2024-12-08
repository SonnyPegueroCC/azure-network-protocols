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

- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic


<h2>Actions and Observations</h2>


 1.) Start by creating a resource group to hold both of your virtual machines (VMs).

Select the resource group, name the VM "VM1," and choose Windows 10 Pro, version 22H as the operating system. Make sure it has at least 2 vCPUs and 16GB of memory. Set a username and password, and leave the default port rules.
Click Next to move through until you reach the Networking page. It should automatically create a virtual network and subnet for you. Click Review and Create to finish.

<p>
<img src="https://imgur.com/WgPD275.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  

<p>
<img src="https://imgur.com/X6ZMTJG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  
  

<p>
<img src="https://imgur.com/XzdSPoR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  
  Follow the same steps to create the second virtual machine, but this time select Ubuntu Server 20.04 LTS.

For the authentication method, choose Password instead of SSH key.
In the Networking section, it should use the same virtual network and subnet as VM1. Click Review and Create to finish. 
  
<p>
<img src="https://imgur.com/0KT3Fmb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  
<p>
<img src="https://imgur.com/pyxsHfF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  
 
  
<p>
<img src="https://imgur.com/3fQXRcw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 
 
 2.) Use Remote Desktop Connection to connect to your Windows 10 VM (VM1).

Install Wireshark: Once connected, open a browser and download Wireshark, which is a tool used to analyze network traffic.
 
 3.) Open Wireshark and set the filter to only show ICMP traffic (this is used for pinging).
 
 <p>
<img src="https://imgur.com/RrtChUe.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 
 4.) Get the private IP address of your Ubuntu VM.
On VM1, open CMD or Powershell and type: ping [Ubuntu VM IP address] (e.g., ping 10.0.0.5).
Also try pinging www.google.com and watch the traffic in Wireshark.
 
<p>
<img src="https://imgur.com/zmJzyne.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 
<p>
<img src="https://imgur.com/pp4eZdK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 
 In either CMD or Powershell ping www.google.com and observe the traffic in wireshark.
 
5.) Set up a continuous ping from Windows 10 to Ubuntu to keep it pinging nonstop.
 
6.) Go to the Network Security Group for your Ubuntu VM.
Add a rule to disable incoming ICMP traffic (disable ping responses). This will cause the ping from VM1 to time out.
 
 <p>
<img src="https://imgur.com/r3dH3Yy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 
<p>
<img src="https://imgur.com/qiSIrsX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 
 Now that we have disabled incoming ICMP traffic from VM2 if we go back to VM1 you can see the ping request is timing out. 
 
 7.) Re-enable ICMP traffic in the Network Security Group for the Ubuntu VM.
In Wireshark, observe the ICMP traffic and check that the ping starts working again. Stop the ping.
 
 8.) The next thing we are going to do is Observe SSH Traffic.

 ![image](https://github.com/user-attachments/assets/2060ef35-5f92-4f5a-a02f-08b7b49dd1e7)

 
