## DNS

In this lab I focused on basic DNS name resolution inside of an Active Directory environment by creating and testing an Address record. I attempted to communicate with a hostname (mainframe) that didn't exist in my DNS> I confirmed that failed resolution with ping and nslookup, and then created a new DNS A-record on the domain controller. After assigning the hostname to the server’s private IP address, name resolution immediately worked from the client machine. This demonstrated  how DNS records control hostname mapping and how administrators can fix resolution issues inside of a domain.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Opened the local DNS cache to see if it had any "Mainframe" titled DNS records, as there were none as the cache is the first place DNS will look for the IP. Next is the hostfile. So I pinged "Zebra" and nothing was found. But then I opened the hostfile in windows-system32-drivers-etc-host. I typed in zebra next to the loopback IP 127.0.0.1 and pinged Zebra again and the log populated in powershell. Used nslookup to search mainframe but it has no resolution because I haven't connected it to an IP Address. 
<img width="859" height="726" alt="1  ipconfig display dns" src="https://github.com/user-attachments/assets/42ebc377-1e50-4aea-83b6-b4ec12e7911d" />
<img width="855" height="650" alt="2  nslookup mainframe when theres no record of this because it hasnt been connected to an ip address" src="https://github.com/user-attachments/assets/3ecfc127-d0d5-4ee7-bae8-c4e9d5426926" />

## Created a record in the DNS for "mainframe" and have it point to the domain controllers private IP address.

## Start Menu - DNS
<img width="770" height="768" alt="3  START MENU DNS" src="https://github.com/user-attachments/assets/b92c8688-bf17-447e-b718-4d6b5d81acfe" />

## In the DNS Manager drop down DC-1-Forward Lookup Zones-my domain. Inside of the mydomain to the right will be records with their corresponding ip's inside of my domain. Right click  that screen and click "New Host.
<img width="858" height="520" alt="4  in dns get to new host a record" src="https://github.com/user-attachments/assets/06ed12e8-ff86-4d55-a6a9-76325b6f9b20" />

## Adding mainframe to the dns to point to 10.0.0.4 which is the ip of the domain controller.
<img width="340" height="348" alt="5  adding mainframe to the dns to point to 10 0 0 4 which is the ip of the domain controller" src="https://github.com/user-attachments/assets/d18b6c4c-681f-4a11-9ee6-8432043ffe64" />

## Pinged mainframe and recieved a response.
<img width="845" height="728" alt="6  Pinged mainframe and recieved a response" src="https://github.com/user-attachments/assets/2c60fe9f-556f-44ff-a171-ecca08072d98" />

## Changed the mainframe IP to 8.8.8.8
<img width="701" height="800" alt="7  changed mainframes ip from 10 0 0 4 to 8 8 8 8" src="https://github.com/user-attachments/assets/3de6b871-feac-4090-9d17-fbcd26d4bb91" />

## Pinged mainframe again, but didn't recieve IP 8.8.8.8 because the cache is checked first, thus 10.0.0.4 is still being populated.
<img width="855" height="719" alt="8  pinged mainframe again but recieved IP 10 0 0 4 again because the cache still has mainframe pointing to 10 0 0 4 not 88888" src="https://github.com/user-attachments/assets/a63aaa47-7662-4748-8f22-2b43ea26bb43" />

## flushed dns, and pinged mainframe and see the ip has been updated
<img width="859" height="728" alt="9  flushed dns, and pinged mainframe and see the ip has been updated" src="https://github.com/user-attachments/assets/7291ec65-93be-4c40-9637-98234e54ebbd" />





