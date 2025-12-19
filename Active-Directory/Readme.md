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

## Type in _EMPLOYEES. This folder will hold all of the employees in the directory 
<img width="750" height="530" alt="12  Type in Employees" src="https://github.com/user-attachments/assets/a844551c-ccb7-40bc-b961-d74d5f76215f" />

## Repeat last step but type in _ADMINS and click OK
<img width="752" height="527" alt="13  Repeat last step and type in ADMINS" src="https://github.com/user-attachments/assets/60eee859-39aa-4895-9a2d-5a351ba2d742" />

## Create a new user in the _ADMINS folder Adding the name and creating a username by right clicking _ADMINS
<img width="756" height="611" alt="14  Created a new user in admins" src="https://github.com/user-attachments/assets/224292fd-e691-4670-9fe6-b48a0c67e593" />
<img width="751" height="528" alt="15  Created a new user in admins  2" src="https://github.com/user-attachments/assets/406690bf-9898-4ae3-8dbd-8521963285a5" />

## Create a password
<img width="747" height="526" alt="16  Create a Password" src="https://github.com/user-attachments/assets/dce1b4e9-bd1c-4ce9-baf6-4b68a50827f1" />

## We need to make this user an Admin by right clicking the users name and clicking "Properties" "Member Of" 
<img width="750" height="835" alt="17  Right click username, member of, Add" src="https://github.com/user-attachments/assets/dbd0610e-f69c-407e-a80d-9f5049f03fdd" />

## Type in "Domain Admins" click "Check Group" click OK, APPLY, OK. Now logout
<img width="752" height="837" alt="18  Type in Domain Admins, Check names, Then OK" src="https://github.com/user-attachments/assets/a7c5a992-0709-49ae-8b88-ccc2ea020855" />

## Now sign in as the new Admin Account that was just created
<img width="463" height="435" alt="19  Login as the new admin account" src="https://github.com/user-attachments/assets/c7063b75-9644-4776-be0e-448160260dae" />

## Log into the CLIENT1 VM right click "Start Menu" and click "System" Click Rename this pc advanced then under "computer name" chick "change"
<img width="308" height="613" alt="20  Login into CLient-1 vm and right click start menu and click system" src="https://github.com/user-attachments/assets/93b4c7a7-40f9-48c7-a6e6-3b3bbc95f7be" />
<img width="1213" height="508" alt="21   Click rename this pc advanced then under computer name chick change" src="https://github.com/user-attachments/assets/c03c613c-e906-4d72-8c6b-cd2e87fb5284" />

## This is where the you are joining the client into the Domain. Click domain and type in "mydomain.com"
<img width="411" height="422" alt="22  joining the client into the Domain Click domain and type in mydomaincom" src="https://github.com/user-attachments/assets/8f65876a-d1f1-47b5-bfb1-f574ce632a2c" />

## Enter the username and password of the Admin account, press ok and allow the VM to restart. This user is now added to the Domain.
<img width="455" height="300" alt="23  Enter the admins username and password and OK then restart" src="https://github.com/user-attachments/assets/42aa0773-da54-43f8-b200-41ad1dcda2bb" />
<img width="299" height="151" alt="24  Admin is now added to the domain" src="https://github.com/user-attachments/assets/0113fa73-2c02-4cc0-ab77-43864c9e7aea" />















