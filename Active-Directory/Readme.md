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

## Go back to the DC-1 User VM and go to "Active Directory Users and Computers". Make a new organizational Unit and name it _CLIENTS. Click "Computers" and see clients inside of that folder. Drag it to the new  _CLIENTS folder you just created 
<img width="753" height="527" alt="25  make a new organizational unit in dc1 users and computers drag clients computers to new client folder" src="https://github.com/user-attachments/assets/d8532513-937b-43f6-9be4-11b4bae58082" />

## Log into the CLIENT VM as the admin user
<img width="408" height="489" alt="26  log into the CLIENT vm as the admin user" src="https://github.com/user-attachments/assets/8641e28d-81a9-4e95-8dad-ee9261e9319c" />

## Start Menu, System, Remote Desktop
<img width="866" height="877" alt="27  Start System Remote desktop" src="https://github.com/user-attachments/assets/f87e1a7f-3428-4f33-b954-0b288923024b" />
<img width="972" height="688" alt="28  Select users that can remotely access this pc" src="https://github.com/user-attachments/assets/3b205ad6-3244-4347-b404-fdba334625f8" />

## type in domain users then click check names.Press ok. This step makes all users a member of this domain and will be permitted to log in to this computer. 
<img width="665" height="533" alt="29  type in domain users then check names" src="https://github.com/user-attachments/assets/0660c5c4-9f4c-4588-b6fa-e6ac9d057cca" />

## Here we will create additional users and log into client-1 with one of the users. 

## Log Into the DC-1 Domain Controller VM, Start Menu, and Run Powershell ISE as administrator. Create a new file and paste the content script of users.
<img width="793" height="595" alt="30  Open Powershell ISE as administrator in DC1 and paste script" src="https://github.com/user-attachments/assets/8838e600-8566-4a38-805f-75369e8befa0" />

##  Press the play/start button and allow the script to run to create 1000 users
<img width="798" height="599" alt="31  Press the play start button and allow the script to run to create 1000 users" src="https://github.com/user-attachments/assets/42e8a7c6-22fe-4df5-a398-a4b94de42d8a" />

# Go to Active Directory Users and Computers. Drop down "mydomain.com" and select an employee account in the _EMPLOYEES folder.
<img width="749" height="599" alt="32  choose an employee that was created by the script" src="https://github.com/user-attachments/assets/aa5f47f7-b119-48b2-bafc-320bfccd1440" />

## Use that employee account to log into CLIENT1
<img width="409" height="497" alt="33  Log into the CLIENT1 with one of the created accounts" src="https://github.com/user-attachments/assets/8154dc97-22db-44a4-bc0d-409c133d0b9f" />
<img width="471" height="486" alt="34  Log into the CLIENT1 with one of the created accounts" src="https://github.com/user-attachments/assets/e1c3089f-7688-4592-9e2e-a56754e17fff" />

## New user that was created by the script (ban.wel) is successfully logged in. 
<img width="611" height="443" alt="35  ban wel is succesfully logged in" src="https://github.com/user-attachments/assets/921bd09f-736d-46c4-84af-9b06b260045c" />

## Now I will set up an Account Lockout policy in Active Directory using the Group Policy Management Console (GPMSC). Run (Win+R) Enter gpmc.msc
<img width="412" height="225" alt="36  set up an Account Lockout policy in Active Directory using the Group Policy Management Console" src="https://github.com/user-attachments/assets/ab9cadfd-10f9-4bed-a963-4672a5027561" />

##  Right click Default domain policy then click edit
<img width="749" height="531" alt="37  Right click Default domain policy then click edit" src="https://github.com/user-attachments/assets/dc070bda-ecb9-463a-ac10-d63cdae015ae" />

##  Computer Configuration - Policies-Windows Settings-Security Settings- Account Policies- Account lockout Policy then click threshhold and set to 5. 5 login attempts will trigger a lockout
<img width="866" height="694" alt="38  Computer configuration - policies-windos settings-security settings- account policies- account lockout policy then click threshhold and set to 5" src="https://github.com/user-attachments/assets/9b9b5adb-7a47-419e-a15d-0d21c7628c18" />

## Log into Client-1 as your first admin (Mine is jane_admin) to force this new Account Lockout Group Policy to update. Running the command line as administrator we will run gpupdate /force to force the update. Next we will run gpgupdate /r to see the results of the update. Now you can see the time and date of the policy and which specific policy was updated.
<img width="628" height="976" alt="39  force the domain policy to update using command line in client 1" src="https://github.com/user-attachments/assets/38f3dfe0-99be-4239-9868-b1019268770e" />

## Now logout of the admin Client1 VM and log back into CLIENT1 using the new user and  fail to login to force a lockout
<img width="453" height="409" alt="40  Now logout of the admin client and log back into CLIENT1 using the new user and  fail to login to force a lockout" src="https://github.com/user-attachments/assets/35e07d1d-14be-43f9-a390-6f619669f9d8" />

<img width="557" height="145" alt="41  Locked out" src="https://github.com/user-attachments/assets/7008c529-3f66-42e8-8a19-78e285a06f1b" />

## Go back to the Domain Controller, go to Active Directory Users and Computers right click "mydomain". click "find" and type in the locked out account's name and click "Find Now". Click the account at the bottom. A properties tab will appear, click "Account" and Check "Unlock account. This account is currently locked out of the Active Directory Domain Controller" then press "Apply". Now log in with that formerly locked out account and the account should now be unlocked and accessible. 
<img width="1137" height="630" alt="43  unlock the account" src="https://github.com/user-attachments/assets/3a92ff1f-7e03-4279-91f9-1158d5ed9fc1" />
<img width="613" height="573" alt="44  Logged in" src="https://github.com/user-attachments/assets/f6bb05ac-14ed-4c44-871a-a5889d8a4767" />
<img width="518" height="198" alt="45  Ran whoami comandline in powershell to show that i have logged in" src="https://github.com/user-attachments/assets/49979cea-8205-4738-897a-0a1df9791a26" />

## Reset a accounts password by going to ADUC mydomain right click find type in the user account find now click the account and reset password.
<img width="518" height="386" alt="47  Reset password" src="https://github.com/user-attachments/assets/b073ad40-408f-41ff-955d-a30659bd4cd8" />

## Go to DC1 VM click start and type in eventvwr.msc and click it to see authentication logs
<img width="776" height="783" alt="48  Go to DC1 VM click start and type in eventvwr msc to see authentication logs" src="https://github.com/user-attachments/assets/457342f4-dd00-4825-9e6b-16dcb330b81a" />

## Right click "Security" and click find
<img width="860" height="547" alt="49  Right click security and click find" src="https://github.com/user-attachments/assets/1877afa8-8ee6-4680-bcf8-2d5f5b40fa38" />

## Type in account name and click "Find Next". Logs will be highlighted of that account with information of the log at the bottom screen. Each time you click "Find Next" it finds a new log associated with that account. Here shows a log showing a logout event.
<img width="860" height="970" alt="50  Type in account name and click Find Next  Logs will be highlighted of that account with information of the log at the bottom screen" src="https://github.com/user-attachments/assets/ea8afd34-3e10-4418-a541-6ba55ad2c30a" />

## Now I will be viewing event logs associated with the failed log in attempts in CLIENT1. I am signed into the "focu.xax" account, however I will run the eventviewer as administrator as the admin account jane_admin. When in eventviewer I click "Windows Logs" , Security, and the "Audit Failure" Logs will show the failed login attempts with information of the event at the bottom showing details like the time, date, account name, endpoint the event happened on, etc.  
<img width="1099" height="1015" alt="51  Log of failed login in event viewer" src="https://github.com/user-attachments/assets/17e64e07-2c0f-4f52-8e96-47a5df0ef8c0" />
















