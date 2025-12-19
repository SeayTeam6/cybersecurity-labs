## Active Directory 
Created a  resource group, virtual network, and subnet in Azure, followed that up by deploying a Windows Server VM that will act as the domain server, assigned it a static private IP, and disabled the firewall for connectivity testing. I deployed a second Windows Virtuall Machine which will act as the Client in the same region and virtual network, its DNS settings are pointed to Domain servers private IP, the VM is restarted, and connectivity is verified by pinging the Domain Server and confirming its DNS configuration in PowerShell.
<img width="526" height="546" alt="1  Turned off firewalls in domain VM" src="https://github.com/user-attachments/assets/6cbed85a-dcd9-47da-b589-ad1d1e624041" />
<img width="780" height="458" alt="2  Set Client VM DNS settings to the Domain VMs private address" src="https://github.com/user-attachments/assets/d574b3d8-7797-46cd-9751-d2232c62db43" />
<img width="858" height="701" alt="3  Pinged Domain server from client" src="https://github.com/user-attachments/assets/860e1eb3-df67-4f84-8dad-1c4cc06e95e8" />
## Installing Active Directory
Logged into the domain server virtual machine and installed the Active Directory Domain Services role. After installation, I promoted the server to a domain controller by creating a new forest named mydomain.com. Once the configuration completed, I restarted the machine and logged back in using the domain account mydomain.com\labuser.

## Start menu, Server Manager

<img width="858" height="724" alt="4  go to the domain server press start menu and click server manager" src="https://github.com/user-attachments/assets/cca9644f-34e5-4707-90bf-79ef1d4fae9b" />

## Add Roles and Features

<img width="574" height="279" alt="5  Add roles and features" src="https://github.com/user-attachments/assets/0ba0b58f-ce61-4f02-8286-9107951a7b75" />

## Click next twice, then choose Active Directory Domain Services. Click next until asked to install and install.
<img width="783" height="561" alt="6  Active directory domain services" src="https://github.com/user-attachments/assets/8c4f60eb-efba-46e5-bb18-c822b6a712cc" />

## Click the yellow flag in the top right and select "Promote this server to a domain controller"

<img width="647" height="325" alt="7  Click the flag in the top right and click promote this server to  a domain controller" src="https://github.com/user-attachments/assets/ac766924-55a1-47a6-b5c2-ad5c53c24c08" />

## Select "Add a new forest" and then type in the domain name, Next
<img width="757" height="553" alt="8  Add a new forest and type in the domains name" src="https://github.com/user-attachments/assets/60722f51-6919-40d2-9ddd-913d3794507d" />

## Create and enter a password, Continue to click next as nothing else will be needed to be added or clicked and install. The VM will restart once install is complete.
<img width="757" height="558" alt="9  create and enter a password" src="https://github.com/user-attachments/assets/db6d1136-3ddb-4343-a597-93db67fad09b" />

## Once installed, allow the restart and log back into the VM using Remote Desktop. Be sure to add "mydomain.com\(Your username)" as the Username. Click "Start" and search for "Active Directory Users and Computers"
<img width="1280" height="723" alt="10  Active directory Users and computers" src="https://github.com/user-attachments/assets/3c1f6fa1-52c9-4144-b55f-2e788719b2fe" />

## Right click "Mydomain.com", then "New', then "Organizational Unit"
<img width="755" height="529" alt="11  File New Organizational Unit" src="https://github.com/user-attachments/assets/07721769-b375-4090-8757-3a4916c9f259" />
















