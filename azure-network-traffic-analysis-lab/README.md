# Azure Network Traffic Analysis & Firewall Configuration Lab

# Azure Network Traffic Analysis & Firewall Configuration Lab

## Objective
Build and analyze a cloud-based network environment using Azure virtual machines to observe network traffic, apply firewall rules, and understand how common protocols operate in a real-world scenario.

## Environment
- Microsoft Azure
- Windows 10 Virtual Machine
- Ubuntu Linux Virtual Machine
- Azure Virtual Network & Subnet
- Network Security Groups (NSGs)
- Wireshark

## Part 1: Virtual Machine & Network Setup
Created a resource group containing both a Windows 10 Virtual Machine and an Ubuntu Virtual Machine within the same Azure Virtual Network and subnet to allow internal network communication between systems.


<img width="901" height="875" alt="2  Created windows and linux vm in azure" src="https://github.com/user-attachments/assets/4e11fc8a-7110-4ecb-8377-51f1dbe8e1ea" />

## Part 2: Network Traffic Observation
Connected to the Windows VM via RDP and used Wireshark to capture and analyze:
- ICMP traffic (ping between VMs and external sites)
- SSH traffic during remote Linux access
- DHCP traffic during IP renewal
- DNS traffic using nslookup
- RDP traffic over TCP port 3389
-
- Started packet capture within Wireshark and filtered for only ICMP traffic.
- <img width="748" height="579" alt="3  Filtered for Icmp traffic in Wireshark inside VM" src="https://github.com/user-attachments/assets/33609888-fc2c-432a-9a78-ea5e648f005e" />
From the Windows VM I pinged the Linux VM using Powershell. The ICMP filter in Wireshark displayed the ICMP/Ping reply traffic from the Ubuntu Linux Vm.
<img width="840" height="729" alt="4  Used powershell to ping the linuxvm" src="https://github.com/user-attachments/assets/b6f70e61-842d-4d5e-8a9e-47fd1a91a84c" />

<img width="1052" height="579" alt="5  The ICMP ping traffic reply from the linux vm" src="https://github.com/user-attachments/assets/3ad78e8c-0619-4a92-a6da-723b5d31622c" />




  

## Part 3: Firewall Configuration & Traffic Control
Configured Network Security Group (NSG) rules to block inbound ICMP traffic to the Ubuntu VM and observed the resulting packet loss and behavior in Wireshark. Re-enabled ICMP to restore connectivity and validated traffic flow.

Here is the initiation of a perpetual/non-stop ping from the Windows 10 VM to the Linux VM

<img width="858" height="730" alt="6  Ran a perpetual ping to the Linux VM" src="https://github.com/user-attachments/assets/f2872ee8-0fca-4732-b984-57cc060fcd94" />
Opened the Network Security Group in Azure, located the Inbound Security Rules (Firewall) for the Linux VM and disabled incoming (inbound) ICMP traffic

<img width="906" height="929" alt="7  Added a firewall rule to deny traffic" src="https://github.com/user-attachments/assets/5e1daa97-8daa-40f4-8599-85b87048d39d" />
Linux VM 10.0.0.5 firewall rule has blocked ping to Windows VM 10.0.0.4
<img width="1052" height="578" alt="8  Linux Firewall rule has blocked responses to windows VM" src="https://github.com/user-attachments/assets/8602e678-e8da-4281-ad78-b16f093fc7f0" />

Deleted firewall rule, re-enabling ICMP traffic
<img width="910" height="582" alt="9  Delete firewall rule re-enabling ICMP traffic" src="https://github.com/user-attachments/assets/55945d2a-9838-45eb-9236-fe7385884ad7" />
<img width="715" height="577" alt="10  The ICMP traffic is re-enabled, there are replies to requests" src="https://github.com/user-attachments/assets/35b4b744-302a-477f-a3e1-27f181a886e3" />

SSH

Observerd SSH traffic of the communication between the Windows VM 10.0.0.4 and Linux VM 10.0.0.5
<img width="856" height="733" alt="11  Using powershell to observe ssh traffic" src="https://github.com/user-attachments/assets/52655751-cda8-40c8-82d9-5b175412397a" />
<img width="1237" height="582" alt="12  Filtered ssh tracffic in wireshark" src="https://github.com/user-attachments/assets/931eef5f-b929-4804-aaae-8eaaee905a48" />

DHCP

Forced the CPU to forget its network identity/IP and then asked for a new one so that Wireshark could watch the DHCP conversation happen.
<img width="852" height="1039" alt="13  Created batch file to force an IP reset so that DCHP conversation traffic that created a new IP could be viewed in wireshark" src="https://github.com/user-attachments/assets/cca8b8a1-a1ab-4b04-9727-16a77a015237" />
<img width="853" height="578" alt="14  this is the DHCP traffic captured by Wireshark" src="https://github.com/user-attachments/assets/0d00abaf-baf5-459e-b001-0fecf347dd46" />








## Evidence


## Skills Demonstrated
- Azure virtual machine deployment
- Virtual networking and subnet configuration
- Network Security Group firewall rules
- Packet capture and traffic analysis
- Protocol analysis (ICMP, SSH, DHCP, DNS, RDP)
- Cloud resource cleanup and cost management
