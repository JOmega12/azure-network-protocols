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

![createResouce](https://github.com/user-attachments/assets/62124556-9b33-4dc0-9542-c7d070ae1c30)

<h3>Create Windows 10 Machine</h3>

- Create your Windows VM and choose the Windows 10 Pro for your image

![creatVmWindows](https://github.com/user-attachments/assets/ab4de9f6-6a0c-4a22-a580-60ee7ce47d7a)

- Make your size is at minimum 2vcpus and 8gb of memory

<h3>Create a Linux/ Ubuntu Server</h3>

- Same process the previous step!
- Only difference is that your image is Ubuntu 22.04

![createVM_linux](https://github.com/user-attachments/assets/89ddbd99-5217-496a-af73-f0037bf2a3c5)

NOTE: Make sure your Virtual Network is the same as Windows VM!

![createVN](https://github.com/user-attachments/assets/c428b3f2-64c0-4401-9d7f-c734190f2a5d)


<h3>Install Wireshark in Windows 10 Machine</h3>

- In the windows 10 machine, install <a href="https://www.wireshark.org/">wireshark</a>

![installWireShark](https://github.com/user-attachments/assets/6e7e7bea-f0c7-4869-9799-7d61ee2ae892)

- Start Packet capture (it's the shark fin)
- What this means is that youre seeing all the stuff that's happening on the backend of the computer. The computer is communicating all these traffic within each other and the numbers are known as packets
- 
![clickFin](https://github.com/user-attachments/assets/8b33c3bd-1402-49e0-97b8-53664ce464e1)


<h3>Observe ICMP Traffic</h3>

- Within Wireshark, type on the search bar filter `icmp` which will only show ICMP traffic
- Within Azure, we're going to copy the private IP address of Linux server and then attempt to ping it within the windows VM
- Then, observe the reply and the response

![icmpSearch](https://github.com/user-attachments/assets/354ca3d1-87a1-4399-9c39-82e007cbff57)


<h3>Configure Firewall for Network Security Group</h3>

- Go to VM
- Linux VM -> networking -> network setting -> Network Security Group (NSG) -> Left side Inbound Security Rules -> Configure rules based on this screenshot

![goToNSGInUbuntuNetwork](https://github.com/user-attachments/assets/5a01dafd-933e-456c-b25b-5ce4b3c417d8)

![goToInbound](https://github.com/user-attachments/assets/3484fafb-36c9-4c14-bbee-39d82a3b88ce)

![add290ForFirewall](https://github.com/user-attachments/assets/0cb3e2b3-d7b3-4d09-b800-87d8d4e839b9)

- And observe if we ping the linux private IP address and see that the request has timed out meaning that the firewall worked
- 
![ICMP Network FireWall](https://github.com/user-attachments/assets/9fb5bc6e-b5ae-4533-8d7b-1b775a05a02e)


- Now delete the Configured Rules 290 and the reobserve after you ping again


<h3>Observe SSH Traffic</h3>

- In Wireshark, start a packet capture (it's the shark fin from earlier)
- Filter for SSH by writing on filter search `ssh`

![searchSSH](https://github.com/user-attachments/assets/07f6c764-6dfe-4665-aabe-db8c35128be2)


- Then from Powershell, type `ssh labuser@privateIPAddress` with the Ubuntu/linux private IP server

![ssh toLabyuser](https://github.com/user-attachments/assets/b873a2e7-eb36-4970-af33-15ecbe8b7382)

- PLEASE NOTE: you will be asked to login from the powershell for the ubuntu/linux server. Login into that using that VM's login info

![sshUbuntuLabuser](https://github.com/user-attachments/assets/738579b4-84e5-4a34-8965-f91af4f908e6)


<h3>Observe DHCP Traffic</h3>

- Back in Wireshark, filter for `DHCP` traffic
- From the WindowsVM in powershell administrator, type in `ipconfig /renew` then observe the traffic that comes in
- 
![dhcP (2)](https://github.com/user-attachments/assets/3ca5a098-5fa1-4165-b45b-12dfbc31cb37)


<h3>Observe DNS Traffic</h3>

- Back in Wireshark, filter for `DNS` traffic

![dns](https://github.com/user-attachments/assets/af7c6b79-fb02-4ade-a491-19e32f52d5e2)

- Then on the command line, use nsloopkup for google.com to retrieve the ip address of google.com then observe
- 
![dnsGoogl](https://github.com/user-attachments/assets/6a7a3e9a-4dcb-4ea7-aa43-cdf38a13b0de)

  

<h3>Observe RDP Traffic</h3>

- Within Wireshark, filter RDP port `tcp.port == 3389` then observe
- The reason why there is a lot of network is because RDP is constantly streaming from the server to our local machine
- 
![rdpSearch](https://github.com/user-attachments/assets/95daf504-ac4f-40de-a951-e2f7c1dd52bc)


<h3>Clean Up</h3>

- To clean up your environment, you go to Azure -> Resource Groups and Delete the resource group where the Virtual Machine lives.


<h2>Conclusion</h2>
Congrats on making through the project! I hope this tutorial has taught you how to use Azure and VM and understand how data flows to the network!


<p></p>
