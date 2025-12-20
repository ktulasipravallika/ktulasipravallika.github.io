
#### Request Path of the service calls

* Domain → DNS → IP
  google.com → 142.250.72.14

* IP → Routing table → Subnet
  172.31.64.0/20 → direct
  default → via 172.31.64.1

* Subnet → Firewall/Security Group
    **Subnet**  → Defines who is directly reachable
    **Firewall Layers**
    * Host firewall	→ iptables / nftables
    * Cloud firewall →	AWS Security Group
    * Network firewall →	NACL
  
* Firewall → Port → Process
    * **Port** → Logical endpoint on a machine
      * 80 → HTTP 
      * 443 → HTTPS

  * **Process** → Program bound to the port
    * nginx → port 80
    * postgres → port 5432

* Process → Container → Pod → Service → Ingress
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


#### IP Address

* **IP address** is machine identity.
  
* An IP address uniquely identifies a machine on a network

* Example : 142.250.72.14

#### DNS 

* **DNS** is name → IP mapping.
  
* DNS translates human-friendly names to machine IPs.

* Example: google.com → 142.250.x.x

#### CNAME

* CName is a Canonical name whihc points to another domain name.

#### TTL 

* TTL is Time To Live. (in Seconds)

* Caches the result for n seconds.

##### Commands 

* `ip a`
  * Gives the IP Address Information.
   
* `ip route`
  * This shows where the packets are sent.
  * The most specific route wins, local subnets bypass gateways, and the default route forwards unknown traffic to the router.
     
* `hostname -I` → Shows the IP Addresses assigned to the machine.

* `nslookup` → Queries DNS servers to resolve domain names to IP addresses(and vice versa).
  
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

