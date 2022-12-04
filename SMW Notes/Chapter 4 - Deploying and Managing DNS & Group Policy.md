___

## Implementing Microsoft DNS
---
###### Domain Name System
- TCP/IP application protocol that enables a DNS server to resolve 
	- Domain and Computer Names to IP Addresses (aka **Forward Lookup**)
	- IP Addresses to Domain and Computer Names (aka **Reverse Lookup**)
		- Refusal for connection from host without reverse lookup record
- DNS Servers provide the DNS namespace for an enterprise
- One of the requirements of Active Directory is to have DNS server(s) setup for its domains
- Installed as a server role
---

## DNS Zones
---
- DNS name resolution is enabled through the use of tables of information
	- That links computer names and IP addresses
	- These tables are associated with partitions in a DNS server (aka **Zones**)

###### Forward Lookup Zone
- The zone that links computer names to IP addresses
- Holds host name records called address records
- Most DNS queries are handled using the resource records of this zone
- In IPv4, a host record is called a **host address (A) resource record**
- In IPv6, a host record is called an **IPv6 host address (AAAA) resource record** 
- Forward lookup zones are automatically created for the domain with the DNS server's address record already entered

###### Stub Zone
- Has only the bare necessities for DNS functions, which are copies of:
	- SOA record zone
	- Name Server records to identify authoritative servers
	- Record of name servers that are authoritative
- Commonly used to help quickly resolve computer names between 2 different namespaces
- Zone Transfer Privilege
	- Local DNS requires to have zone transfer privilege granted from the target DNS which owns the Forward Zone
		- I.e. cannot setup stub zone for google.com without zone transfer privilege
---

## Using the DNS Dynamic Update Protocol
---
- Microsoft DNS is also called Dynamic DNS (DDNS)
	- Modern form of DNS that enables client computers and DHCP servers to automatically register IP addresses

###### DNS Dynamic Update Protocol
- Enables information in a DNS server to be automatically updated in coordination with DHCP
	- Saves administrators time because they no longer have to manually register each new workstation or each time a new IP leease is issued
- Ensure that DNS Dynamic Update Protocol is secured
---

## DNS Replication
---
###### Primary DNS Server
- Main administrative server for a zone
- Authoritative server for that zone

###### Secondary DNS Server
-  Contains a copy of the primary DNS server's zone database, but is not used for administration (**not authoritative**) 
- Obtains copy of zone database through a zone transfer over the network
- **Vital Services:** 
	- Ensure there is always a copy of the primary DNS server's data
	- Enable DNS load balancing among a primary DNS server and secondary servers
	- Secondary DNS can face and answer queries from public network
	- Reduce congestion in one part of the network 
---

## DNS Queries
---
###### Workflow
1. Client requests a name to IP address resolution from local DNS
2. Local DNS gives an immediate answer when:
	- It is the authoritative server for that domain
	- Local DNS has the required info from its cache
3. Local DNS looks up the IP address of the correct **authoritative server** from one of the **root servers** (root servers addresses are built into DNS installation)
4. Local DNS acts as a client to visit multiple authoritative DNS servers to get the final answer (aka **Iterative Lookup**) 
5. Once the correct authoritative server is identified, Local DNS contacts the remote DNS directly and gets the required info
---

## Additional DNS Server Roles
---
- Common to designate one DNS server to forward name resolution requests to a specific remote DNS server
- Forwarding can be set up that if the DNS server that receives the forwarded request cannot resolve the name --> The server that originally forwarded the request attempts to resolve it via other ways
	- Nonexclusive Forwarding

###### Caching Server
- DNS Server can function as a caching server
	- Used to provide fast queries 
	- Results of each query is stored in RAM 
- DNS Server without zones is caching-only
	- A caching-only DNS server queries a primary or secondary DNS server and caches the results to provide a fast response for the next identical query
	- Used to reduce number of secondary servers and reduce extra network traffic
- Limitation:
	- Takes time to build up a comprehensive set of resolved names to IP addresses
	- May be necessary to flush the DNS server cache -> cache lost
---

## Forwarder vs Root Hints
___
###### Forwarder
- Faster -> Recurisve query (try to provide answer, possibly non-authoritative)
- Local DNS has no way to ensure security configuration of external Forwarder
- Can enable customisable DNS service within an organisation (For security enhancement at DNS level)
	- DNS Filtering/Logging

###### Root Hints
- Slower -> Interactive queries (try to provide best answer)
- More reliable
	- 13 Root Hints are supported by >200 load balancing servers
---

## Creating a DNS Implementation Plan 
---
###### Best Practices
- Implement Windows Server 2016 DNS servers instead of other versions of DNS, and use Active Directory
- The resource records and zones that can be set up for IPv4 can also be set up for IPv6
- Consider using namespaces to represent natural organizational boundaries
- Make sure the DNS servers on a private network are well secured in terms of Windows Server 2016 security options
- Plan to locate a DNS server across most site links
- Create two or more DNS servers to take advantage of the load balancing, the [[Chapter 2 - WIndows Configurations & Active Directory Basics#^684cdc|multi-master]] relationships (with AD-integrated zones), and the fault tolerance
- Designate one DNS server as a forwarder to reduce traffic
- Blocking your network clients to access to external DNS directly to prevent data exfiltration via DNS tunneling
- If you have multiple servers used for one application use round robin to distribute the load
	- Only applicable for a namespace with cluster setup
- If a branch location with a read-only domain controller (RODC) needs local DNS services because there are many users, make the RODC a secondary DNS server and not a primary DNS server
	- Unidirectional replication (compromised RODC will not spread malicious updates)
	- Not caching any passwords on a RODC
---

## DNS Enhancement in Windows Server 2016
---
- DNS group policies for:
	- Filtering malicious IP addresses and redirecting malicious clients to a dead end rather than to the computer they want to reach
	- Redirecting clients to specific data sources or servers according to the time of day
	- Managing client access to account for high traffic situations
	- Directing clients to the best source for a specific application
- The ability for DNS to work with client computers that have more than one NIC
- New PowerShell cmdlets for configuring DNS
---

## Troubleshooting DNS 
---
- Steps to take to troubleshoot DNS problems:
	- Restart DNS Server and DNS Clients
	- Check for the most recent log errors relating to DNS
---

## DNS Threats
---
###### Possible DNS related threats 
- DDOS with DNS Amplification Attack
	- Bogus queries are sent to a DNS to trigger it to send high volume of replies to the targeted victim
- Cache Poisoning
	- The DNS cache / Stub Zone / Forwarder is comprised, causing the DNS to return incorrect IP addresses, diverting traffic to the attacker's computer (or any other computer).
- Registrar Hijacking
	- aka Domain hijacking
	- Changing the registration of a domain without the permission of its original registrant.
	- Generally done by exploiting a vulnerability in the domain name registration system or through social engineering
---

## Microsoft Baseline Security Analyser
---
- A tool used to scan Windows-based computers for common security holes
	- Compares a computer's settings against Microsoft's released patches and listed vulnerabilities
- Provides a streamlined method to identify missing security updates and common security misconfigurations
- Checks the following desktop application parameters:
	- Internet Explorer security zone settings per local user
	- Outlook security zone settings per local user
	- Office products security zone settings per local user
- For MBSA tool to be run on multiple machines or remotely, following must be enabled:
	- Server service, Remote Registry service, File & Print Sharing
	- May disable all these by default, and use Group Policies to enable them prior to a routine MBSA scan for the entire network or sub-net

###### Applicable to: 
- Win Vista, Win 7, Win 8, Win 8.1, Win2k3, Win2k8, and Win2012R2
-  Internet Information Services (IIS)
- SQL Server 2012
- Internet Explorer 5.01 and later
- Exchange 
- Windows Media Player 6.4 and later
- Microsoft Office 
- Microsoft Data Access Components (MDAC)
- MSXML
- Microsoft Virtual Machine
- Commerce Server
- Content Management Server
- SharePoint Server
- Host Integration Server
---

## Microsoft Security Compliance Manager
---
- Enables automation of deployment and monitoring baseline compliance

###### Key Features & Benefits:
- Download security baseline from Microsoft
- Compare and customise security baselines
- Export baselines in format like XLS, and/or Group Policy objects (GPOs)
---

## An Overview of Security Features in Window Server 2016
--- 
1. Windows Server 2016 was created to emphasise security
	- Reduced attack surface of the kernel through Server Core and Nano Server
	- Expanded and evolving Group Policies
	- Windows Firewall
	- Windows Defender
	- Security Templates and Security Configuration and Analysis tools
	- User Account Control
	- BitLocker Drive Encryption
2. Server Core or Nano Server can be a good solution for a server that handles critical network operations such as DNS and DHCP
	- Can be a good solution for a Web or other server in the demilitarized zone of a network
		- Demilitarized zone (DMZ)
			- A portion of a network that is between two networks, such as between a private network and the Internet
			- Computers in the DMZ have fewer security defenses via routers and firewalls
	- They also can offer better performance and lead to fewer problems
3. Group policy is a way to bring consistent security and other management to Windows Server 2016 and clients connecting to a server
4. Windows Firewall and IPsec
	- Settings are merged for consistency
5. Windows Defender
	- Software that scans for viruses, spyware, and malware
	- Windows Server 2016 is the first Windows Server OS to include Windows Defender
6. Security Templates and Security Configuration and Analysis tools
	- Enable you to configure server-wide security
7. User Account Control (UAC)
	- Designed to keep the user running in the standard user mode as a way to:
		- More fully insulate the kernel
		- Keep operating system and desktop files stabilized
	- Another element of UAC is the Administrator Approval Mode
		- Prevents malware or an intruder from acquiring control through a back door without the administrator knowing
- BitLocker Drive Encryption
	- Prevents an intruder from bypassing ACL file and folder protections
---
