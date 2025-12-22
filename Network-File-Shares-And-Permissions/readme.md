## Network File Shares and Permissions
## Overview and Purpose of the Lab
In this lab I will be sharing resources over the network, and creating files shares to  read, write, or denying access to individual groups and users. Proper permission management is critical for security and least privilege access.

## Create sample file shares with different permission levels

### Purpose of this section
This section focuses on creating shared folders on a domain controller and assigning different permissions to simulate real world access scenarios. By testing access as a normal domain user, I was able to verify how permissions affect visibility and file modification.

## Connect to DC-1 as the domain administrator
I logged into **DC-1** using the domain admin account **mydomain.com\jane_admin**. Administrative access is required to create folders, share them, and assign permissions.

## Connect to Client-1 as a normal domain user
I logged into **Client-1** using the standard domain user account **mydomain\focu.xax**. This user account is used to test access restrictions and permissions.

## Create shared folders on the DC-1 C drive
On DC-1, I navigated to the **C:\ drive** and created four folders named **read-access**, **write-access**, **no-access**, and **accounting**. These folders represent different access scenarios that are commonly seen in enterprise environments.

## Share the “read-access” folder with read only permissions
I shared the **read-access** folder and assigned the **Domain Users** group **Read** permissions. This allows users to view files but prevents them from making changes.

## Share the “write-access” folder with read and write permissions
I shared the **write-access** folder and assigned the **Domain Users** group **Read and Write** permissions. This allows users to view, create, and modify files within the folder.

## Share the “no-access” folder with admin only permissions
I shared the **no-access** folder and assigned **Read and Write** permissions only to the **Domain Admins** group. Normal domain users do not have access to this folder.

## Skip permission assignment for the accounting folder
At this stage, I did not assign any permissions to the **accounting** folder. This folder is used later when testing access based on security group membership.

---

## Test file share access as a normal user

### Purpose of this section
This section verifies that the permissions assigned on the domain controller behave as expected when accessed by a normal domain user.

## Navigate to shared folders from Client-1
While logged into Client-1 as **focu.xax**, I opened the Run dialog and navigated to **\\DC-1** to view the available shared folders.

## Attempt to access each shared folder
I attempted to open each of the shared folders that were created earlier. I confirmed which folders were accessible, which folders allowed file creation, and which folders denied access entirely. The results aligned with the permissions that were configured on DC-1.

---

## Create an ACCOUNTANTS security group and test group based access

### Purpose of this section
This section demonstrates how security groups are used to grant access to specific resources without assigning permissions to individual users. This is a common best practice in Active Directory environments.

## Create the ACCOUNTANTS security group
On DC-1, I opened **Active Directory Users and Computers** and created a new security group named **ACCOUNTANTS**.

## Assign permissions to the accounting folder
On the **accounting** folder, I assigned the **ACCOUNTANTS** group **Read and Write** permissions. This ensures that only members of this group can access and modify files in the folder.

## Test accounting folder access as a non member
While logged into Client-1 as **focu.xax**, I attempted to access the **accounting** shared folder. Access was denied because the user was not a member of the ACCOUNTANTS group.

## Log out and update group membership
I logged out of Client-1 and returned to DC-1. I added **focu.xax** as a member of the **ACCOUNTANTS** security group.

## Test accounting folder access as a group member
After signing back into Client-1 as **focu.xax**, I accessed the **accounting** shared folder again. This time, access was successful and file creation was allowed due to group membership.

---

## Cloud based permissions using Google Drive

### Purpose of this section
This section compares traditional file server permissions with cloud based access control by using Google Drive. It demonstrates how permissions can be inherited and modified at both the file and folder level.

## Access Google Drive
I logged into my Google account and navigated to **drive.google.com**, which represents my personal cloud storage environment.

## Create a document and add content
I created a new document, entered a single word, and named the document. This file is used to test sharing and permission changes.

## Test access using a private browsing window
I opened an incognito or private browsing window and pasted the document URL. Since the document was private, access was denied.

## Change document permissions to public viewer
I updated the document permissions to allow anyone with the link to view the document. I confirmed that the document could be opened in the incognito window but could not be edited.

## Attempt to modify the document as a viewer
While in the incognito window, I attempted to edit the document and confirmed that changes were not allowed due to viewer only permissions.

## Change document permissions to public editor
I updated the document permissions to allow anyone with the link to edit the document. I confirmed that changes could now be made in the incognito window.

## Restrict document access
I removed public access and set the document permissions back to **Restricted**.

## Create a public folder in Google Drive
I created a folder named **Public Documents** and set the folder permissions to **Public with Viewer access**.

## Move the restricted document into the public folder
I dragged the restricted document into the **Public Documents** folder and observed the permission inheritance message.

## Test inherited permissions
I opened the document in an incognito window and confirmed that the document inherited the public viewer permissions from the parent folder.

---

### Key Skills Demonstrated
- File sharing and permission management in Active Directory
- Understanding read, write, and restricted access
- Security group based access control
- Permission testing and validation
- Cloud file sharing and permission inheritance
- Applying least privilege access principles
