## Networking

Real-world analogy

* Your house → computer/server
* Your home address → IP address
* Your name → domain name
* Phone number extensions → ports
* Post office → router
* Security guard → firewall

**Networking** is "How computers find each other and exchange data"

Every networking problem boils down to these 5 questions:

* Who are you talking to? → IP / DNS
* Which application? → Port
* Can you reach it? → Routing
* Are you allowed? → Firewall
* Who translates addresses? → NAT

#### DNS 

* **DNS** is name → IP mapping. 
* DNS translates human-friendly domain names to machine IPs (IP Addresses).
* Example: google.com → 142.250.x.x
* Order of events:
  * Browser asks OS: “Do we already know this IP?” → OS asks DNS server → DNS replies with IP → Browser connects to that IP.
  * Your system gets DNS from:
  *   ISP (home network)
  *   Cloud VPC settings
  *   /etc/resolv.conf

#### IP Address

* **IP address** is machine identity.  
* An IP address uniquely identifies a machine on a network
 * Example : 142.250.72.14

* **IPV4 :**
  * Format:
      `x.x.x.x` → Each `x` varies from `0` to `255` and is 1 byte` or `8 bits`.
  * IP Address is 4 Bytes or (4 * 8) 32 bits.
  * Each x = 0–255
   * Example: 10.0.0.5

* **Pulic Vs Private**

  * **Private IPs**
    * Used in home, offices and Cloud VPC. These cannot be accessed directly from the internet.
    * Examples:
      * 10.x.x.x
      * 172.16.x.x - 172.31.x.x
      * 192.168.x.x 

   * **Public IPs**
    * Globally reachable and is assigned by ISP. (Internet Service Provider)
    * Globally Unique and used to communicate over the internet.

#### PORTS

* IP Adrress identifies the machine, but one machine can run many applications like Web server, SSH, Database, Monitoring Agent.
* A port is a number that identifies a specific application running on a machine.
* Ports defines which application the traffic should reach.
* Port Range → 0 - 65535
* Example : 192.168.1.10:**80**
  * HTTP → 80
  * HTTPS → 443
  * SSH → 22
  * DNS → 53
  * FTP → 21
  * MySQL → 3306
  * Postgres → 5432

#### PROTOCOLS

A **protocol** is a set of rules that define how data is sent and received between systems. 

**TCP**
 * Transmission Control Protocol
 * Reliable and Connection Oriented Protocol that guarantees delivery and ordering of packets.
 * Example : HTTP, HTTPS, SSH, FTP, SMPT

**UDP**
 * User Datagram Protocol
 * Connectionless protocol prioritizes speed and low latency.
 * Example : DNS, DHCP, NTP, Video Streaming, Online Gaming, VoIP.

#### CNAME

* CNAME is a Canonical name whihc points to another domain name.

#### TTL 

* TTL is Time To Live. (in Seconds)

* Caches the result for n seconds.

#### Subnets 

* A subnet is a group of IP addresses that belong to the same network.
* Machines in same subnet can communicate directly.
* **Subnetting** → Dividing a Large Network into smaller networks.
* **CIDR** (Classless Inter-Domain Routing)
* It is a way to represent IP address ranges using a prefix length like /24.
  * `x.x.x.x/8` (8 bits common out of 32) → Class A IP Addresses → 256 * 256 * 256 IP Addresses
  * `x.x.x.x/16` (16 bits common out of 32) → Class B IP Addresses → 256 * 256 IP Addresses
  * `x.x.x.x/24` (24 bits common out of 32) → Class C IP Addresses → 256 IP Addresses.
  * **Usable IPs = TotalIPs - 2**
       * 1 IP is fixed for Network IP.
       * Other is fixed for Broadcast IP: 192.168.1.255
    * Example : 192.168.1.0/24 
       * Network IP: 192.168.1.0
       * Broadcast IP: 192.168.1.255

#### ROUTING 

* Routing determines where packets go and the default gateway connects the local network to external networks.
* The system sends packets to a gateway.
* Gateway forwards packets to the destination.

#### GATEWAY

* A gateway is a device (usually a router) that connects your network to other networks.

#### FIREWALL:

* A firewall is a security system that allows or blocks network traffic based on rules.
* Rules are usually based on IP address, Port, Protocol (TCP/UDP), Direction (inbound/outbound)

* **Stateful firewall**
 * Remembers connections and allows return traffic automatically
 * Response traffic is automatically allowed.
 * Security Groups (AWS) are stateful.

**Stateless firewall**
 * Does NOT remember connections
 * You must allow both directions explicitly
 * NACLs (AWS) are stateless.

**Firewall Layers**
    * Host firewall	→ iptables / nftables
    * Cloud firewall →	AWS Security Group(Stateful)
    * Network firewall →	NACL(Stateless)

#### ICMP — Internet Control Message Protocol

* **ICMP** is a protocol used to send network control and error messages.
* It is used to check connectivity and report problems.
* ICMP fits in Network Layer.
  
#### Request Path of the service calls

* **Domain → DNS → IP**
  google.com → 142.250.72.14

* **IP → Routing table → Subnet**
  172.31.64.0/20 → direct
  default → via 172.31.64.1

* **Subnet → Firewall/Security Group**
    
* **Firewall → Port → Process**
  * **Process** → Program bound to the port
    * nginx → port 80
    * postgres → port 5432

* **Process → Container → Pod → Service → Ingress**
    * This is Kubernetes-specific abstraction
      * **Container** → Isolated runtime for a process.
      * **Pod** → Smallest deployable unit and it contains one or more containers.
      * **Service**
        * Stable virtual IP (ClusterIP)
        * Load balances across pods
      * **Ingress**
        * HTTP entry point
        * Routes by hostname/path

#### Linux + Network view

Application → DNS Lookup (Name → IP) → Routing (ip route) → Gateway → Destination IP

##### Full Path

```text
app.company.com
   ↓ DNS
34.120.10.5
   ↓ Route
Internet Gateway
   ↓ Firewall
AWS Security Group (443 allowed?)
   ↓ Port
443
   ↓ Process
nginx
   ↓ Container
Docker
   ↓ Pod
k8s pod
   ↓ Service
ClusterIP
   ↓ Ingress
Routes to backend
```

#### Linux + network view

Application
   ↓
DNS Lookup (Name → IP)
   ↓
Routing (ip route)
   ↓
Gateway
   ↓
Destination IP

## OSI Model

When an application connects to a service, it first resolves the domain using **DNS**, then establishes a TCP connection via the **three-way handshake**, and only then sends request through the layers as below.

* **DNS Resolution**
 * DNS resolution is the process of converting a domain name into an IP address.
   
* **TCP Handshake**
 * TCP handshake is how two machines establish a reliable connection before data transfer.
    * Client → `SYN`
    * Server → `SYN-ACK`
    * Client → `ACK`
      
* **Seven Layers of Data.**
 * Layer - 7 → Application Layer
    * Where applications talk to the network.
    * Example : HTTP, HTTPS, SSH, FTP.
      
 * Layer - 6 → Presentation Layer
    * Encryption of data is done here.
    * Example : HTTPS encryption (TLS)
      
 * Layer - 5 → Session Layer
    * Session is created for the request.
    * Maintains session and handles reconnecting.
    * Example : SSH Session, HTTPS keep-alive
      
 * Layer - 4 → Transport Layer
    * This is where TCP vs UDP lives.
    * TCP : Connection established (3-way handshake) → Data sent → Acknowledgements received → Retransmit if lost.
      * Used by HTTP, HTTPS, SSH, Databases
    * UDP : This is Fast and no guaranteed connection
     * Used by DNS, Streaming, Monitoring
       
 * Layer - 3 → Networking Layer
    * This handles IP addressing and routing between networks.
    * Assigns IP addresses and Routes packets and Handles subnets.
      
 * Layer - 2 → Data Link Layer
    * MAC address
    * ARP
     
 * Layer - 1 → Physical Layer →
    * Data is converted to electronic signals.
    * Cables, WiFi and Ethernet.
  
##### Commands 

**Network Layer**

   * `ip a` → { `a` is address }
      * Gives the IP Address Information.

   * `hostname -I` → { `-I` is IPAddress }
      * Shows the IP Addresses assigned to the machine.
      * `hostname`
      * `hostname -i`
  
   * `ip route` → { `route` is path }
      * This shows where the packets are sent, Default gateway and Local subnets.
      * The most specific route wins, local subnets bypass gateways, and the default route forwards unknown traffic to the router.

   * `ping ` → Checks IP Connectivity
      * Tests reachability
      * Uses ICMP, not TCP/UDP
    
   * `traceroute url` → { trace = trace the path }
      * `traceroute google.com`
      * It is a network diagnostic tool that maps the path packets take from your computer to a destination. 

   * `ipcalc 192.168.1.0/24`
      * This helps to understand CIDR ranges and usable IPs.

   * `iptables -L`
      * `iptables` Controls packet filtering on Linux.
      * Shows the firewall Rules.
        
   * `ufw status` → { user-friendly wrapper } 
      * Shows firewall status
      * Simpler than iptables

**Transport Layer**

   * `ss -tuln` → { `ss` → sockets `-t` → TCP, `-u` → UDP, `-l` → Listening, `-n` → Numeric }
      * Shows listening ports and connections.

   * `netstat -tuln` → legacy version of `ss`

   * `lsof -i :80` → { List the open files (ports are files here) }
      *  To check which process is using port 80.
    
   * `nc` → { netcat }
      * `nc google.com 443` 
      * Netcat tests whether a port is reachable.
      * `nc -vz google.com` → { `-v` → Verbose, `-z` → Zero-I/O mode ( Do NOT send any data — just check if the port is open ) }
    
**Application Layer**
 
   * `curl`
      * `curl google.com` 
      * Sends HTTP/HTTPS requests and Tests Applications Level connectivity.
  
   * `wget
      * Used mainly for downloading files. 
  
   * `ssh ipaddress`
      * Secure remote login
      * Uses TCP port 22

   * `nslookup` → Queries DNS servers to resolve domain names to IP addresses(and vice versa)
      * `nslookup amazon.com`
      * `nslookup 8.8.8.8`
    
   * `dig` → Powerful DNS query tool with detailed output.
      * `dig google.com`  
      * Records:
        * `A record` maps domain name to IPV4 Address
        * `AAAA record` maps domain name to IPV6 Address.
        * `CNAME` maps to alias to another domain.
        * `MX` maps to mail servers
        * `NS` maps to Name Servers     
      * Status :
        * `NOERROR` → Success
        * `NXDOMAIN` → Domain doesn’t exist
        * `SERVFAIL` → DNS server failure

   * `resolvectl` → Manages DNS resolver on systemd systems.
        * `sudo resolvectl dns ens5 8.8.8.8` → Sets the DNS for the interface.
        * `resolvectl status` → Shows which DNS servers are configured.
        * `sudo resolvectl revert ens5` → Revert back to the original DNS.

##### Status Codes

**1xx**
  * `100` → Continue
  * `102` → Processing
**2xx**
 * `200` → OK
 * `201` → Created
 * `202` → Accepted
 * `203` → Non-Authoritative Information
 * `204` → No Content
**3xx**
 * `300` → Multiple Choices
 * `302` → Found
 * `304` → Not Modified
**4xx**
 * `400` → Bad Request
 * `401` → Unauthorized
 * `403` → Forbidden
 * `404` → Not Found 
**5xx**
 * `500` → Internal Server Error
 * `501` → Not Implemented
 * `502` → Bad Gateway
 * `503` → Service Unavailable

