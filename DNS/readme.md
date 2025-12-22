## DNS

In this lab I focused on basic DNS name resolution inside of an Active Directory environment by creating and testing an Address record. I attempted to communicate with a hostname (mainframe) that didn't exist in my DNS> I confirmed that failed resolution with ping and nslookup, and then created a new DNS A-record on the domain controller. After assigning the hostname to the server’s private IP address, name resolution immediately worked from the client machine. This demonstrated  how DNS records control hostname mapping and how administrators can fix resolution issues inside of a domain.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Opened the local DNS cache to see if it had any "Mainframe" titled DNS records, as there were none as the cache is the first place DNS will look for the IP. Next is the hostfile. So I pinged "Zebra" and nothing was found. But then I opened the hostfile in windows-system32-drivers-etc-host. I typed in zebra next to the loopback IP 127.0.0.1 and pinged Zebra again and the log populated in powershell. Used nslookup to search mainframe but it has no resolution because I haven't connected it to an IP Address. 
<img width="859" height="726" alt="1  ipconfig display dns" src="https://github.com/user-attachments/assets/42ebc377-1e50-4aea-83b6-b4ec12e7911d" />
<img width="855" height="650" alt="2  nslookup mainframe when theres no record of this because it hasnt been connected to an ip address" src="https://github.com/user-attachments/assets/3ecfc127-d0d5-4ee7-bae8-c4e9d5426926" />

## Created a record in the DNS for "mainframe" and have it point to the domain controllers private IP address.

## Start Menu - DNS
<img width="770" height="768" alt="3  START MENU DNS" src="https://github.com/user-attachments/assets/b92c8688-bf17-447e-b718-4d6b5d81acfe" />

## In the DNS Manager drop down DC-1-Forward Lookup Zones-my domain. Inside of the mydomain to the right will be files inside of my domain. Right click  that screen and click "New Host.
<img width="858" height="520" alt="4  in dns get to new host a record" src="https://github.com/user-attachments/assets/06ed12e8-ff86-4d55-a6a9-76325b6f9b20" />

