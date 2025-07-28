# DevOps Networking
## This documentation is helpful to understand the networking concept required for a DevOps Engineer. Please note I am using Ubuntu Linux OS and its commands.
### IP Address Concept.
IP (Internet Protcol) address is a unique address provided to a device, every device have its own IP address which is connected to a network, like our home address but this is in a digital format.
This unique addresses have two version that is IPV4 and IPV6. IPV4 is commonly used and we can identify the difference between, IPV4 -> 127.0.0.1, 192.168.x.x and IPV6 -> fe80:: or 2001::, IPV4 is a 32 bit (8+8+8+8) and IPV6 is 128 bit. To check IP addresses of the system use commands ifconfig, ip addr show. To check IP address of active connections then we can use command like netstat -tunp. 
### Difference between Public, Private IP addresses and NAT.
#### Public IP
The most common example is web-server, VPN, this is for those device which need to be accessed from internet. For instance 8.8.8.8 is a IP of google.com
#### Private IP
This is ideal for internal communication which uses local network, internal routing for device to device communication. For example home router 192.168.1.1, 10.0.0.1 etc
#### NAT Gateway
This is very useful, help the device exposed to private IP to access securely to internet using a shared Public IP address.
### CIDR (Classes Inter-Domain Routing) Concept for IPV4.
CIDR is a method use to allocate IP addresses and manage network routing more efficiently. It helps to save unused IPs, like if we want to use  IP address betweenthese ranges 172.16.0.0 <-> 172.16.255.255 then we can provide IP address 172.16.0.0/255. This site is very useful if you guys want to learn CIDR calculation https://ipcisco.com/lesson/cidr-and-cidr-calculation/
### Classful and Classless IP
Classful are divided into Class A, B, C. In below image you can see, how they are divided ( here rooms = IP). This is an old method and there is wastage of IP addresses and complicated networking rules.

<img width="509" height="131" alt="image" src="https://github.com/user-attachments/assets/98aabb79-86bd-4e85-b7b7-30e4f6f6fb8b" />

Solution: If someone want only 300 IPs so instead if using two Class C we can simply decrease the subnet by 1 and get slighly bigger unsed IP addresses range.
So instead of using /24 mask which is 256, we can use /23 which gives 510 usead IP.
Calculation of unused IP is:
CIDR notation like /24 means:
The first 24 bits are for the network, and the rest are for hosts.”
Since IP addresses are 32 bits total, that leaves: 32 − 24 = 8 bits for host addresses.
If you have 8 bits for hosts, the total number of IPs is:
2^8 = 256 \text{ total IPs}. Here first IP is of network address and last IP is of broadcast addresses. So final value of unsed IP is 254.
Now if we decrease subnet by 1 then:
The first 23 bits are for the network, and the rest are for hosts.”
Since IP addresses are 32 bits total, that leaves: 32 − 23 = 9 bits for host addresses.
If you have 8 bits for hosts, the total number of IPs is:
2^9 = 512 \text{ total IPs}. Here first IP is of network address and last IP is of broadcast addresses.So final value of unsed IP is 510.
Summary:
- You need 300 IPs
- Class C only gives 254
- CIDR lets you adjust the size of your network
- Use /23 instead of /24 → problem solved!
### Virtual Machine
Virtual Machine runs on a portion of a physical device, it mimics like a computer, it have all components of a computer like CPU, RAM, Networks and storage.
DevOps teams use a hypervisor to manage virtual machines. A hypervisor, or a Virtual Machine Monitor (VMM), is a piece of software, firmware, or hardware that creates and runs VMs.
The hypervisor runs on top of a physical dedicated server or an operating system to emulate the underlying hardware.
Virtualization relies on cloud computing to ensure optimal performance at all times. Cloud allows a VM to scale up or down on-demand and in a matter of minutes to meet resource requirements.
<img width="623" height="384" alt="image" src="https://github.com/user-attachments/assets/562fa448-236c-49ec-b4e2-83dab51e4ff3" />

Virtual machines allow a team to build, test, and deploy code within simulated environments without wasting computing resources.
