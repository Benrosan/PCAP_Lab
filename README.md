# PCAP_Lab

## Objective

Conduct PCAP analysis via Wireshark and provide a report on attack vectors used and various IOCs associated with malware infection.

### Skills Learned

- PCAP Analysis
- Detailed understanding of web traffic components as they relate to the OSI model

  
### Tools Used

- Wireshark
- NMAP

### Steps

**1.** Created custom columns and filters to make data more legible.<br>

![Screenshot 2024-03-22 112834](https://github.com/Benrosan/PCAP_Lab/assets/160042310/2cda1e53-f3cc-4233-8e65-b5ef02ba3f09)
###

**2.** Tried filtering for DHCP and NetBios frames to find host name. Only the DHCP discover frame contained that info.
###
![Screenshot 2024-03-25 094658](https://github.com/Benrosan/PCAP_Lab/assets/160042310/6a5252c2-5465-4e1a-96aa-cf40b484ac0c)
###
  - I subsequently enabled name resolution in the view menu to keep the host name visible as I continued looking through the PCAP. filtering for NetBios frames also provides the hostname.
  - I was also able to get the device's MAC Address from the Frames (00:60:52:b7:33:0f).
###
![Screenshot 2024-03-25 095224](https://github.com/Benrosan/PCAP_Lab/assets/160042310/c184092e-7020-4f1c-8687-92e5d2a09e6b)

**3.** First thing to note in the PCAP was that after the user navigated to oceriesfornot.top, a DNS query was made to another domain: antnosience.com at IP 157.245.142.66
###
![2024-03-25 11_22_27-_2022-03-21-traffic-analysis-exercise pcap](https://github.com/Benrosan/PCAP_Lab/assets/160042310/c1a6b2eb-0124-4611-bf98-9f7ab069d0ab)
###

**4.** I needed more information on what exactly between the TCP 3-way handsahke and the DNS query, so I decided to update my filter to capture all HTTP/1.1 traffic.
###
![2024-03-25 11_35_04-_2022-03-21-traffic-analysis-exercise pcap](https://github.com/Benrosan/PCAP_Lab/assets/160042310/cd5e45e4-431d-4640-b984-fd463c14776a)
###
The screenshot above that the user downloaded a package from 188.166.118. 
###
**5.** Next step was to export all HTTP objects to take a closer look at them. A total of 2 objects were exported from the object list. In order to learn more about each object, I spun up my Linux VM to check attributes via the CLI.
###
![2024-03-25 11_11_27-Kali Linux on GENIE - Virtual Machine Connection](https://github.com/Benrosan/PCAP_Lab/assets/160042310/9a82d2fd-9146-4295-8b0b-1b52e49ec955)
###
I checked the SHA256 hash value of the file and uploaded it to TotalVirus.com. It returned the results below:
###
![2024-03-25 11_08_24-Kali Linux on GENIE - Virtual Machine Connection](https://github.com/Benrosan/PCAP_Lab/assets/160042310/1e2d4621-492c-4393-a4bb-b92f75ac568d)
###
Checking the various file names for additional info I noticed the following:
###
![2024-03-25 11_09_37-Kali Linux on GENIE - Virtual Machine Connection](https://github.com/Benrosan/PCAP_Lab/assets/160042310/f7da97bd-c7c4-42a8-b10e-b73a5beede43)
####
I then conducted a search for the **IcedID** malware in the MITRE database. It returned the following:
###
![2024-03-25 11_48_07-IcedID, Software S0483 _ MITRE ATT CK®](https://github.com/Benrosan/PCAP_Lab/assets/160042310/89ed2276-b31d-4cef-82eb-c8725b3cf234)
###
Among other things, IceID uses HTTPS to reach out to C2 servers.
###
**6.** Another HTTP Get request was made to this potentially malicious domain.
###
![2024-03-26 10_39_55-2022-03-21-traffic-analysis-exercise pcap](https://github.com/Benrosan/PCAP_Lab/assets/160042310/5158984f-4213-4d92-a2c7-4d0b0e0cf747)
###
The file downloaded was .der file, indicating it was a certificate. It's possible that this may be some sort of self-signed certificate designed to facilitate a Man-in-the-Middle attack via proxies, which would be consistent with some IcedID attack vectors.<br>
###
**7.** Upon further investigation, it looks like the host was redirected to various malicious sites, which ultimately led to the downloading of the certificates.
###
![2024-03-26 10_58_37-2022-03-21-traffic-analysis-exercise pcap](https://github.com/Benrosan/PCAP_Lab/assets/160042310/42b0efed-c278-4b48-8cf8-94e02e8d8498)





















