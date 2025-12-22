# Azure Virtual Machine IP Address and VPN Location Lab

## Azure Virtual Machine and Public IP Analysis

### Lab Overview and Purpose
In this lab, I explored how public IP addresses change based on geographic location and network routing by using an Azure Virtual Machine and a VPN service. The purpose of this lab was to understand how cloud hosted systems appear on the internet compared to local machines, and how VPNs can alter perceived location and network identity. This is important in real world IT and security environments where location based access, logging, and traffic analysis are common.

I first identified my own public IP address from my local machine. I then created a Windows 10 Virtual Machine in Azure located in a different country and compared its public IP address. After that, I installed and configured Proton VPN inside the virtual machine and connected to a VPN server in another country. Finally, I tested how websites responded based on the VPN location, observing changes related to geography and content delivery.

---

## Identify my local machine’s public IP address
From my personal computer, I navigated to **https://whatismyipaddress.com/** to determine my current public IP address. I saved this information in a text file to use as a reference point for comparison later in the lab. This IP represents how my local network appears to the internet.

## Create a resource group in Azure
I logged into the Azure portal and created a new resource group. This resource group is used to organize and manage all of the resources related to this lab, including the virtual machine, networking components, and public IP address.

## Create a Windows 10 Virtual Machine in another geographic location
I created a new **Windows 10 Virtual Machine** in Azure and selected a geographic region located in a different country than my own. Choosing a different region allows me to observe how Azure assigns public IP addresses based on physical data center locations.

## Log into the virtual machine using Remote Desktop
After the virtual machine finished deploying, I connected to it using **Remote Desktop (RDP)**. This allowed me to interact with the VM as if it were a physical computer located in that other country.

## Identify the virtual machine’s public IP address
Inside the Azure virtual machine, I opened a web browser and navigated to **https://whatismyipaddress.com/**. I recorded this public IP address in a text file. This IP was different from my local machine’s IP and reflected the Azure region where the VM was hosted.

---

## VPN Configuration and Location Testing

### Purpose of VPN Testing
This section of the lab focuses on how VPNs affect public IP addresses and perceived geographic location. VPNs are commonly used for privacy, security, and testing how applications behave across different regions.

## Sign up for Proton VPN on my local machine
On my personal computer, I signed up for the free version of **Proton VPN** using the official signup page. This account would later be used inside the Azure virtual machine.

## Download and install Proton VPN inside the virtual machine
While logged into the Azure virtual machine, I downloaded and installed the Proton VPN client. Installing the VPN inside the VM allows the VM’s internet traffic to be routed through a VPN server instead of directly through Azure’s public IP.

## Log into Proton VPN and connect to a server in another country
I logged into the Proton VPN client and connected to a VPN server located in a different country, such as Japan. This created a new network path and assigned the VM a new public IP address associated with the VPN server’s location.

## Identify the public IP address while connected to the VPN
With the VPN active, I navigated again to **https://whatismyipaddress.com/** from inside the virtual machine. I recorded the new public IP address in a text file. This IP reflected the VPN server’s country instead of the Azure data center location.

## Test location based website behavior
While still connected to the VPN, I browsed to websites such as **Google**, **Disney**, and **Amazon**. I observed whether there were any differences in content, language, or URLs based on the VPN server’s location. This demonstrated how websites can tailor content depending on a user’s perceived geographic region.

---

### Key Skills Demonstrated
- Azure Virtual Machine deployment
- Public IP address identification and comparison
- Geographic region awareness in cloud environments
- VPN installation and configuration
- Understanding how VPNs affect network routing and location
- Observing location based web behavior
