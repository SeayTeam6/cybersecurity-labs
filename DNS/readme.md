## DNS

In this lab I focused on basic DNS name resolution inside of an Active Directory environment by creating and testing an Address record. I attempted to communicate with a hostname (mainframe) that didn't exist in my DNS> I confirmed that failed resolution with ping and nslookup, and then created a new DNS A-record on the domain controller. After assigning the hostname to the server’s private IP address, name resolution immediately worked from the client machine. This demonstrated  how DNS records control hostname mapping and how administrators can fix resolution issues inside of a domain.

Opened the local DNS cache to see if it had any "Mainframe" titled DNS records, as there were none as the cache is the first place DNS will look for the IP. Next is the hostfile. So I pinged "Zebra" and nothing was found. But then I opened the hostfile in windows-system32-drivers-etc-host. I typed in zebra next to the loopback IP 127.0.0.1 and pinged Zebra again and the log populated in powershell. 
<img width="859" height="726" alt="1  ipconfig display dns" src="https://github.com/user-attachments/assets/42ebc377-1e50-4aea-83b6-b4ec12e7911d" />


