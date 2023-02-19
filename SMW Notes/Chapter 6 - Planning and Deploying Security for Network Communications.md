___

## IPsec Principles
---
- A set of protocols, used to ensure private, secure communications over IP networks by using cryptographic security services; based on:
	- Protecting the contents of IP packets
	- Providing packet filtering 
	- Enforcing trusted communication
	- Securing communication with encryption of the information traveling the network
- Mostly used for IPv4 implementations

###### Security Issues
- Source spoofing
- Replay packets
- No data integrity or confidentiality
- Resulting in:
	- DOS attacks, Replay attacks, Spying  etc.

###### Control Elements
- **Internet Key Exchange (IKE):** 
	- Protocol for exchanging encryption keys
		- Authenticate other computer before performing key exchange (or prevents any communication with unauthenticated computers)
	- Responsible for:
		1. Initial security negotiation 
			- Base on the Authentication method(s) defined in the IPsec rule
		2. Determine secret keying material
			- To secure network communication
			- Related to Filter Action setting of the associate IPsec rule
			- ![](https://i.imgur.com/JwEGjya.png)
	- AKA IKEEXT in Microsoft Implementation 
- **Authentication Header (AH):** 
	- Provides an authenticity guarantee for packets
		- Using checksum
	- Data origin authentication, data integrity, and replay protection
		- Replay protection: If packet comes from A, and is intercepted at B. When it finally arrives at C, the sequence number in AH will be able to show that the packet was 'replayed' as it has been processed before 
- **Encapsulating Security Payload (ESP):** 
	- Provides confidentiality through packet encryption

- IPsec also utilizes IP Compression (IPComp), which is used to compress raw IP data

###### Implementation 
- Windows Server 2016 supports the implementation of IP security (IPsec)
- When an IPsec communication begins between two computers
	- The computers first  negotiate (using IKE module) and  authenticate between the receiver and sender (using Microsoft AuthIP extension)
- Next, extra hashing scheme [optional] will help to ensure data integrity at packet header
- Finally, data is encrypted with integrity check [optional] at the NIC of the sending computer as it is formatted into an IP packet

- IPsec can provide security for all TCP/IP-based applications and communications protocols
- IPsec Security Policy
	- IPsec security policies can be established through the Group Policy in an Active Directory
	- IPsec security policies can also be configured through the IP Security Policies Management MMC snap-in
- Windows Firewall Advanced Security Rule
	- IPsec security can also be configured via the Windows Firewall Advanced Security Rules.
	- Provide more IKE authentication options and AES encryption support

###### Trade-Offs
- Deploying IPsec can affect network performance and compatibility with other services & applications
- Impacts:
	- Time needed to establish IPsec connection
	- Time needed to filter and encrypt packets
	- Increased packet size
	- Network inspection technologies used in routers, firewalls, Intrusion Detection System (IDS) may not work on IPsec packets
	- Application compatibility with other platforms
	- Effect on Active Directory and domain controller connections
---

## Planning an IPsec Deployment
---
- IPsec is **not recommended** for the following:
	- To secure communication between domain members and their domain controllers
		- Reduces network performance
		- Configuration of the IPsec policy is complicated
	- To secure all traffic in a network
		- Again, reduced network performance
		- IPsec can’t support multicast and broadcast traffic
		- Network tools that need to inspect packet headers may not work
- **Proper uses** of IPsec:
	- Packet filtering such as using IPsec with the Routing and Remote Access service to permit or block inbound or outbound traffic
	- Securing host-to-host traffic on specific paths 
	- Securing traffic to servers
	- Combining L2TP and IPsec (L2TP/IPSec) for securing VPN scenarios
	- Incorporating site-to-site or gateway-to-gateway tunnelling
	- ![](https://i.imgur.com/PE3TAvI.png)
- In a simple network structure, a single IPsec policy can be designed that may contain multiple rules 
	- One policy for all
- In a large environment, many different IPsec policies may be designed
	- Factors that can increase the number of policies required include:
		- Computer Roles
		- Sensitivity of data traveling over the network
		- Computer operating systems
		- Domain relationships and memberships
		- Number of applications that require IPsec
---

## 5 Elements of a Rule
---
- Each IPsec Policy may consist of multiple rules
- Each rule contain 5 configurable elements
	- Connection Type (LAN, Remote, ALL)
	- Mode (Transport or Tunnel) 
	- Filter List
	- Host to Host Authentication Method 
		- Used by IKE – Phase 1
	- Filter Action ( include choice of AH/ESP)
		- Negotiated in IKE Phase 2, and carry out the agreed scheme in the actual traffic

###### Connection Type
- Choose which type of connection the rule is applied 
	- LAN / Remote / All Connections

###### IPsec Mode
- Transport:
	- Used to secure communications within a network and it can be server-to-server or server-to-client 
	- IPsec provides end-to-end security
	- If IPsec protection caters for systems within a LAN
	- Only protects the data portion of the IP packet and leaves the original IP header untouched
- Tunnel:
	- Used to secure communications between networks
		- E.g. Between two gateways 
	- Entire IP packet is encapsulated within a new IP packet, with a new IP header added to the front of the packet
		- The original IP packet becomes the payload of the new packet, and the entire packet, including the original IP header, is protected by IPSec
	- Primarily used for interoperability with gateways or end systems that do not support L2TP/IPsec or PPTP VPN site-to-site connections
	- If IPsec protection involves WAN 

###### Filter List
- IPsec filter is a specification in the IPsec rule that is used to match IP packets
	- Filters are grouped together in a system wide Filter List
- In the IPsec rule properties setting
	- The system wide filter list will be available for the choice of the filter.
- Packets which match a filter
	- Will be applied with the associated filter actions such as permit, block, or negotiate security
- **Caveat:**
	- A system configured with IPsec may not apply the expected security scheme because the filter is set wrongly
	- When the network traffic does not match the IPsec, it will not be blocked, but it will just pass through.

- Filter list identifies traffic based on its source, destination, and protocol. Examples included with Win2K3, Win2K8:
	- All ICMP Traffic
	- All IP Traffic
- Filter action is set for each type of traffic as identified by a filter list. Examples included with Windows Server since Win2k3
	- Permit
	- Request Security
	- Require Security
- Administrator may construct/customise specific Filter actions

###### Authentication Method
- If the connection matches the filter, IKE (phase 1) will be invoked for initial authentication 
- Available Authentication Methods:
	- Kerberos V5  
		- Default authentication method for Windows 2000  server or later
		- Based on mutual authentication
		- Use when all of your clients can authenticate using Kerberos V5
		- A method that requires the least administrative effort
	- Certificates
		- Requires PKI (Public Key Infrastructure)
		- A method of granting access to users based on their unique identification
		- Used in situations that include access to corporate resources, external business partner communications, or computers that do not run the Kerberos V5
	- Pre-shared Key
		- Used when other methods are not available
		- It is a shared secret key
- The authentication process is done using DH asymmetric key encryption for data exchange
- More than one authentication method can be selected
	- With designated priority level
	- IKE Phase 1 will sort out if two parties share one common Authentication method
- IPsec Authentication specifies how the computers will prove their identities to each other when trying to establish a SA (Security Association)
- ![](https://i.imgur.com/U8MhrIr.png)
###### Filter Action
- Will only be triggered when the incoming or outgoing connections match the filter 
- Available actions:
	- Permit
	- Block
	- Negotiate Security
		- Will be carried out at the Phase 2 of IKE
---

## Encryption & Protocols
---
- Two basic categories of encryption:
	- Symmetric key encryption
	- Public key encryption
- Lifetime settings determine when a new key is generated

- Methods of hashing:
	- Secure Hash Algorithm (SHA): uses a 160-bit encryption key, very-high security method 
	- Message Digest 5 (MD5): uses a 128-bit encryption key, lower performance than SHA 
	- Hashing method is used to support AH (Authentication Traffic)
- Methods of encryption
	- Data encryption standard (DES): uses a 56-bit key, not recommended for high-security
	- Triple DES (3DES): key length is 168 bits, provides medium- and high-security networks
	- Encryption method is used to support ESP (Encapsulating Security Payload)

- Tunnel mode uses double encapsulation, suitable for protecting traffic between network systems, such as an un-trusted medium like the Internet
	- **AH Tunnel Mode:** Encapsulates an IP packet by placing an AH header between internal IP header and external IP header
	- **ESP Tunnel Mode:** IP packet is first encapsulated with an ESP header, then the result is encapsulated with an additional IP header
---

## Deploying IPsec Policies
---
- IPsec policies can be deployed using:
	- Local Policy Objects
		- A way to enable IPsec for computers that are not members of a domain
	- Group Policy Objects
		- IPsec policy is propagated to any computer accounts that are affected by the GPO
	- Command-line tools
		- netsh IPsec command in Windows Server 2003/2008
	- Windows Defender Firewall Advanced Security Settings (WFAS) 
		- Starting from Windows Server 2016

###### Using IPsec Policies
- IPsec policies from different OUs are never merged
- For domain-based IPsec policy, limit the number of rules to 10 or less
- Create and apply an IPsec policy at the domain level to provide a baseline of IPsec protection
- Use the Export and Import Policies commands in the IP Security Policy Management console to back up and restore the IPsec policy objects
- Be sure to adequately test the impact of new IPsec policies before assigning them in the domain

###### Precendence
- Possible to configure IPsec for multiple containers that will affect a computer
- Only one IPsec policy can be assigned to a computer at a time
	- If there are multiple IPsec policies assigned at different levels, the last one takes effect
- Precedence sequence: From lowest to highest (Local GPO, Site, Domain, OU)
- Persistent IPsec policy has the highest precedence of all, even though it is stored on the local computer
	- Adds to or overrides local or Active Directory policy 
	- Remains in effect regardless of whether other policies are applied
	- Provides backup security in case IPsec policy gets corrupted or if errors occur
	- Can be set using command line tools – netsh
- Default order can be overridden using Enforced, Block Policy Inheritance

- When troubleshooting IPsec policies and their precedence, remember:
	- Only a single IPsec policy can be assigned at a specific level in Active Directory
	- An IPsec policy assigned to an OU takes precedence over a domain-level policy for members of that OU
	- IPsec policies from different organizational units are never merged
	- An OU inherits the policy of its parent OU unless the policy inheritance is explicitly blocked or a separate policy is explicitly assigned to that OU
	- Before assigning an IPsec policy to a GPO, verify the group policy settings that are required for the IPsec policy
---
