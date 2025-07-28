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
Classful are divided into Class A, B, C. In below image you can see, how they are divided.
<img width="509" height="131" alt="image" src="https://github.com/user-attachments/assets/98aabb79-86bd-4e85-b7b7-30e4f6f6fb8b" />

