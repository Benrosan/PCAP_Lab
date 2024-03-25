# PCAP_Lab

## Objective

TBD

### Skills Learned

TBD

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
























