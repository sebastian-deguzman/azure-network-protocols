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

- 2 Virtual Machines
- Observe ICMP traffic
- Observe SSH traffic
- Observe DNS traffic
- Observe RDP traffic

<h2>Actions and Observations</h2>

To begin, we will create 2 virtual machines in the Azure portal. The first VM will use windows 10 22h2 and the other VM will use Ubuntu (linux). Make sure to use at least 2 vCPUs so it runs smoothly. We also need to ensure both VM's are under the same network.

![Screenshot 2025-04-26 000020](https://github.com/user-attachments/assets/8ffb6fd4-d7f9-47cb-a9ad-2d2bc07d3c07)

![Screenshot 2025-04-26 000337](https://github.com/user-attachments/assets/ae7dc5f2-b1b3-41a0-a08d-be1e9696d8ed)


We then use remote desktop (RDP) and log into the Windows VM. Once inside the VM we will download and install Wireshark from https://www.wireshark.org. This protocol analyzer is used to obeserve the network traffic.

![Screenshot 2025-04-26 001027](https://github.com/user-attachments/assets/057e2904-5fbb-41ec-8bc8-acf1d2717ed3)

Once installed, open wireshark and we will begin to observe the ICMP traffic. to do this open powershell and ping the private IP address of the linux vm (can be found in the azure portal).

![Screenshot 2025-04-26 001534](https://github.com/user-attachments/assets/de2ce808-cb8a-4751-a708-00beeb8a2660)

We now configure a firewall on the linux VM, network settings > click linux-vm-nsg > inbound security rules add new rule

![Screenshot 2025-04-26 004030](https://github.com/user-attachments/assets/546c9acd-f3a7-4b65-87dc-4839c0a88448)

Next, we observe SSH traffic while in wireshark. To do this in powershell we will use the command ssh labuser@<private address> > yes > enter password once this is established this allows us to observe and analyze it in real time.

![Screenshot 2025-04-26 004044](https://github.com/user-attachments/assets/29b14e43-48c2-4b07-b874-047a74c5b825)

Now we will observe the DNS traffic, to do this, on powershell use the command nslookup (website). This will show us the IP address of the website.

![Screenshot 2025-04-26 004521](https://github.com/user-attachments/assets/5ab6ae76-bf94-47c6-b6ea-a9a6dd267d8f)


Lastly we will observe RDP traffic by inputing rdp or tcp.port==3389 and will show us the live feed of traffic being transmitted between VMs.

![Screenshot 2025-04-26 004650](https://github.com/user-attachments/assets/1673bb07-f515-4ef0-866a-12e9940cce2b)
