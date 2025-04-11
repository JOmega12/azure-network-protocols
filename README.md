<p align="center">
<img src="https://learn.g2.com/hubfs/G2CM_FI634_Learn_Article_Images_%5BNetwork_traffic_analysis%5D_V1b.png" height="70%" width="70%" alt="network traffic"/>
</p>



<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we will observe a network between two virtual machines. We will be observing ICMP traffic, SSH traffic, DHCP traffic, DNS traffic, and RDP traffic. It's crucial to know how network traffic works because knowing how data flows across a network enables IT professionals to diagnose and troubleshoot performance issues, identify security threats, and others

<h2>Environments and Technologies Used</h2>

- Microsoft Azure
- Remote Desktop Protocol
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 Pro (21H2)
- Ubuntu Server 22.04

<h2>Key Steps</h2>

- Create Resource Group
- Create Windows 10 Machine
- Create Ubuntu Server Machine
- Install WireShark in Windows 10 Machine 
- Observe ICMP Traffic
- Configure Firewall (Network Security Group)
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic

<h2>Actions and Observations</h2>


<h3>Create Resource Group</h3>

<h3>Create Windows 10 Machine</h3>

- Create your Windows VM and choose the Windows 10 Pro for your image

- Make your size is at minimum 2vcpus and 8gb of memory

<h3>Create a Linux/ Ubuntu Server</h3>

- Same process the previous step!
- Only difference is that your image is Ubuntu 22.04


<h3>Install Wireshark in Windows 10 Machine</h3>

- In the windows 10 machine, install <a href="https://www.wireshark.org/">wireshark</a> 

- Start Packet capture (it's the shark fin)
- What this means is that youre seeing all the stuff that's happening on the backend of the computer. The computer is communicating all these traffic within each other and the numbers are known as packets


<h3>Observe ICMP Traffic</h3>

- Within Wireshark, type on the search bar filter `icmp` which will only show ICMP traffic
- Within Azure, we're going to copy the private IP address of Linux server and then attempt to ping it within the windows VM
- Then, observe the reply and the response


<h3>Configure Firewall for Network Security Group</h3>

- Go to VM
- Linux VM -> networking -> network setting -> Network Security Group (NSG) -> Left side Inbound Security Rules -> Configure rules based on this screenshot

- And observe if we ping the linux private IP address and see that the request has timed out meaning that the firewall worked


- Now delete the Configured Rules 290 and the reobserve after you ping again


<h3>Observe SSH Traffic</h3>

- In Wireshark, start a packet capture (it's the shark fin from earlier)
- Filter for SSH by writing on filter search `ssh`
- Then from Powershell, type `ssh labuser@privateIPAddress` with the Ubuntu/linux private IP server


- PLEASE NOTE: you will be asked to login from the powershell for the ubuntu/linux server. Login into that using that VM's login info

<h3>Observe DHCP Traffic</h3>

- Back in Wireshark, filter for `DHCP` traffic
- From the WindowsVM in powershell administrator, type in `ipconfig /renew` then observe the traffic that comes in


<h3>Observe DNS Traffic</h3>

- Back in Wireshark, filter for `DNS` traffic
- Then on the command line, use nsloopkup for google.com to retrieve the ip address of google.com then observe

  

<h3>Observe RDP Traffic</h3>

- Within Wireshark, filter RDP port `tcp.port == 3389` then observe
- The reason why there is a lot of network is because RDP is constantly streaming from the server to our local machine 


<h3>Clean Up</h3>

- To clean up your environment, you go to Azure -> Resource Groups and Delete the resource group where the Virtual Machine lives.


<h2>Conclusion</h2>
Congrats on making through the project! I hope this tutorial has taught you how to use Azure and VM and understand how data flows to the network!


<p></p>
