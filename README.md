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
### OSI Model for DevOps Enginner.
OSI ( Open System Interconnection) Model is important for a DevOps Engineer as it helps to troubleshoot, provides security, optimize proper delivery of artifact and used in infrastructre as code (IAC).

OSI LAYERS uses 7 layers of data transmission, how a DevOps Engineer make a http/API request and how data is passed through each layer till it reached the last layer i.e physical layer.

Here is my understanding of a OSI layer:

Application Layer 7th: I created a CI/CD pipeline to deploy my Python application to a production server. The pipeline is triggered via GitLab’s UI or API over HTTPS.
   
Presentation Layer 6th: GitLab encrypts webhook payloads using TLS when communicating with external services (e.g., monitoring tools or deployment APIs), protecting sensitive data like commit messages and project metadata.
   
Session Layer 5th: The pipeline establishes an SSH session to the GitLab Runner or target VM, maintaining connection state and handling token expiration or timeouts.
   
Transport Layer 4th: Reliable data transfer occurs over TCP (e.g., ports 22 for SSH or 443 for HTTPS), ensuring artifact uploads and job logs are transmitted correctly.
   
Network Layer 3rd: The GitLab Runner routes traffic to the target VM using IP addressing and subnet configurations.
   
Data Link Layer 2nd: The runner checks MAC address reachability; VLAN misconfigurations may disrupt connectivity in self-hosted environments.
   
Physical Layer 1st: The deployment reaches the VM via its NIC, completing the pipeline and delivering the Python application to the server.

### Same Example using  TCP/IP Model which 4 layer and most commmonly used nowadays.
#### TCP/IP Model

Application Layer: This is a combination of original Application layer along with Presentation and Session Layer. When CI/CD pipeline triggers via HTTP/HTTPS, Webhook is secruly sent to a external service and SSH is used for deployment. Python app logic and metadata handled here.

Transport Layer: TCP ensures reliable delivery of data ( eg artifacts and logs). Port like SSH (22) and HTTPS (443) are validated. Handles retransmissions and error correction.

Internet Layer: GitLab Runner routes traffic using IP addresses. Subnetting, routing tables, and NAT may be involved. Ensures packets reach the correct VM or cloud endpoint.

Network Access Layer: This is a Combination of Data link Layer and Physical Layer. MAC address resolution and VLAN checks (especially in self-hosted runners) NIC status and physical connectivity to VM. Diagnosing low-level network issues.

### Ports and Protocol
Above transport layer of TCP/IP model also introduce the concept of  ports and protocol, Its like a package arriving to your computer from internet, that comptures have many department like apps/services and each department have a TCP port number.
The OS uses this port number to route data to correct process.
Here are some known port numbers that are non-privileged:



##### Port Number|Process|	What it’s used for:


##### 22	          SSH	   Secure shell, remote access, and file transfer,
##### 53	          DNS	   Resolving domain names into IP addresses,
##### 80	          HTTP	   Serving web pages,
##### 443	       HTTPs	Serving web pages in a secure manner,
##### 3306	       MySQL	Database connections,

non-privilegedanyone can use them without special permission, some require root permissions. Ports 1-1023 are called “well-known ports” and require root permissions before a server can listen to them. It’s a good practice to avoid running web servers as root, assign minimal permissions to services, and use nonprivileged ports when possible. That’s why sometimes we can see ports 8080 for HTTP and ports 433 for HTTPS they’re non-privileged.



