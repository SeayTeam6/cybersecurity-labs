# DNS -  Active Directory Name Resolution


### Lab Overview 
In this lab, I focused on basic DNS name resolution inside of an Active Directory environment by creating and testing DNS records. DNS plays a critical role in Active Directory because it allows systems to locate each other by name instead of IP address. The purpose of this lab was to understand how DNS resolution works, what happens when records do not exist, and how administrators create and troubleshoot DNS records inside of a domain.

I attempted to communicate with a hostname called **mainframe** that did not exist in DNS. I confirmed the failed name resolution using **ping** and **nslookup**, then created a DNS A record on the domain controller. After assigning the hostname to the server’s private IP address, name resolution immediately worked from the client machine. This demonstrated how DNS records control hostname mapping and how administrators resolve DNS issues in an Active Directory environment.

---

### Understanding DNS Cache and the Hosts File
Before creating any DNS records, I first explored how Windows attempts to resolve names locally. DNS resolution checks the local DNS cache first, then the hosts file, before querying a DNS server. This section demonstrates how name resolution behaves when no DNS record exists and how the hosts file can manually resolve names.

## Checked the local DNS cache and tested unresolved hostnames
I opened PowerShell and checked the local DNS cache to see if there were any existing records for **mainframe**. There were none, which confirmed that the system had no prior knowledge of that hostname. Since the DNS cache is the first place Windows checks during name resolution, this was an important step to verify.

I then attempted to **ping a hostname called zebra**, which failed because no DNS or hosts file entry existed for it.

<img width="859" height="726" alt="1  ipconfig display dns" src="https://github.com/user-attachments/assets/42ebc377-1e50-4aea-83b6-b4ec12e7911d" />

## Verified that mainframe had no DNS resolution using nslookup
I used **nslookup mainframe** to query the DNS server directly. The lookup failed because **mainframe was not connected to any IP address in DNS**, confirming that no A record existed for it.

<img width="855" height="650" alt="2  nslookup mainframe when theres no record of this because it hasnt been connected to an ip address" src="https://github.com/user-attachments/assets/3ecfc127-d0d5-4ee7-bae8-c4e9d5426926" />

## Edited the hosts file to manually resolve a hostname
To demonstrate local name resolution, I opened the hosts file located at `Windows\System32\drivers\etc\hosts`. I manually added the hostname **zebra** next to the loopback IP address **127.0.0.1**. After saving the file, I pinged **zebra** again and received a response, showing that the hosts file can override DNS resolution locally.

---

### Creating an A Record in DNS
This section focuses on creating an A record, which maps a hostname to an IPv4 address. In this environment, the domain controller also acts as the DNS server, so all DNS records are created there.

## Opened DNS Manager on the domain controller
I opened the DNS Manager from the Start Menu on **DC-1**, which is hosting the DNS Server role for the domain.

<img width="770" height="768" alt="3  START MENU DNS" src="https://github.com/user-attachments/assets/b92c8688-bf17-447e-b718-4d6b5d81acfe" />

## Navigated to the Forward Lookup Zone for my domain
Inside DNS Manager, I expanded **DC-1**, then **Forward Lookup Zones**, and selected **mydomain**. On the right side of the window, I could see existing DNS records and their associated IP addresses. From this screen, I right-clicked and selected **New Host (A or AAAA)** to begin creating a new A record.

<img width="858" height="520" alt="4  in dns get to new host a record" src="https://github.com/user-attachments/assets/06ed12e8-ff86-4d55-a6a9-76325b6f9b20" />

## Created the mainframe A record
I entered **mainframe** as the hostname and assigned it the IP address **10.0.0.4**, which is the private IP address of the domain controller. This connects the hostname to the server at the DNS level.

<img width="340" height="348" alt="5  adding mainframe to the dns to point to 10 0 0 4 which is the ip of the domain controller" src="https://github.com/user-attachments/assets/d18b6c4c-681f-4a11-9ee6-8432043ffe64" />

---

### Testing DNS Name Resolution
After creating the A record, I verified that the client machine could now resolve the hostname.

## Pinged mainframe to confirm DNS resolution
From the client machine, I pinged **mainframe** and successfully received a response. This confirmed that DNS was now resolving the hostname to the correct IP address.

<img width="845" height="728" alt="6  Pinged mainframe and recieved a response" src="https://github.com/user-attachments/assets/2c60fe9f-556f-44ff-a171-ecca08072d98" />

---

### Understanding DNS Cache Behavior
This section demonstrates how DNS caching can cause old IP addresses to persist even after a DNS record is changed.

## Changed the mainframe IP address in DNS
I edited the existing A record for **mainframe** and changed its IP address from **10.0.0.4** to **8.8.8.8**, which is owned by Google.

<img width="701" height="800" alt="7  changed mainframes ip from 10 0 0 4 to 8 8 8 8" src="https://github.com/user-attachments/assets/3de6b871-feac-4090-9d17-fbcd26d4bb91" />

## Observed cached DNS results after the change
I pinged **mainframe** again from the client machine, but it still resolved to **10.0.0.4**. This occurred because the DNS cache was checked first and still contained the old IP address.

<img width="855" height="719" alt="8  pinged mainframe again but recieved IP 10 0 0 4 again because the cache still has mainframe pointing to 10 0 0 4 not 88888" src="https://github.com/user-attachments/assets/a63aaa47-7662-4748-8f22-2b43ea26bb43" />

## Flushed the DNS cache and tested again
I flushed the local DNS cache and then pinged **mainframe** once more. This time the hostname resolved to **8.8.8.8**, confirming that the updated DNS record was now being used.

<img width="859" height="728" alt="9  flushed dns, and pinged mainframe and see the ip has been updated" src="https://github.com/user-attachments/assets/7291ec65-93be-4c40-9637-98234e54ebbd" />

---

### Creating and Testing a CNAME Record
This final section focuses on creating a CNAME record, which maps one readable hostname to another fully qualified domain name.

## Created a new CNAME record in DNS Manager
In DNS Manager, I created a new alias record, which allows one human readable name to point to another domain name.

<img width="859" height="501" alt="10  In dns manager create a new alias" src="https://github.com/user-attachments/assets/bda32f89-e55b-4c6a-9153-906f90dc2155" />

## Configured the alias to point to google.com
I set the alias name to **search** and mapped it to the fully qualified domain name **google.com**.

<img width="682" height="493" alt="11  Alias name is search and the qualified domain i chose is googlecom" src="https://github.com/user-attachments/assets/e8aed99d-f205-41bd-a98a-4c76d6e8825d" />

## Tested the CNAME record using ping and nslookup
I pinged **search** and observed that it resolved to Google along with its IP address. I also ran **nslookup search**, which confirmed that the domain controller resolved the alias to **google.com**.

<img width="858" height="710" alt="12  pinged search and nslookup search to populate google ip and name" src="https://github.com/user-attachments/assets/39624990-f783-45a4-a075-d8bf3aef1c18" />








