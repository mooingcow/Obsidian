___

## Introduction to Remote Access
---
###### Remote Access Services (RAS) Role
- Enables remote access through three means: 
	- Virtual Private Networking
	- DirectAccess
	- Web Application Proxy

###### Virtual Private Network (VPN) 
- Like a tunnel into a larger network that is restricted to designated member clients only

###### DirectAccess (Related; In textbook) 
- Establishes two “tunnels” for connecting to a DirectAccess server used in remote access 
- Transparent to users and always on

###### Web Application Proxy (Related; In textbook)
- Publishing applications so that users external to an organization can access those applications on the organization’s servers
---

## Implementing a VPN
---
- VPNs can use an Internet connection or an internal network connection as a transport medium to establish a connection with a VPN server
- A VPN uses LAN protocols as well as tunneling protocols
	- To encapsulate the data as it is sent across a public network such as the Internet
- **Benefits:** 
	- Users can connect to a local ISP and connect through the ISP to the local network
	- VPN is used to ensure that any data sent across a public network, such as the Internet, is secure
		- VPN creates an encrypted tunnel between the client and the RAS server
- **Note:**
	- Domain Controller <u>cannot</u> be used as VPN server
	- VPN server is public facing and is situated in the DMZ segment

###### Implementation
- A VPN server uses two or more NICs for communication
	- One NIC is used to connect to the private network inside the organisation that uses private IP addressing
	- The other NIC connects to the external public network
- To create this tunnel, the client first connects to the Internet by establishing a connection using a remote access protocol
- Once connected to the Internet, the client establishes a second connection with the VPN server
- The client and the VPN server agree on how the data will be encapsulated and encrypted across the virtual tunnel
- ![](https://i.imgur.com/CWXPvoU.png)
___

## Remote Access Protocols
---
- Remote access protocol carries the network packets over a wide area network (WAN) link
	- Encapsulates a packet, such as an IP datagram, so that it can be transmitted from a point at one end of a WAN to another point
- IP is the most commonly used transport protocol
- Several remote access protocols are used by Windows Server 2016 and its remote clients
	- Point-to-Point Tunneling Protocol
	- Layer Two Tunneling Protocol
	- Secure Socket Tunneling Protocol
	- IKE v2 Protocol (IPsec, tunnel mode, IKE version 2)

###### Point-to-Point Protocol (PPP) [Legacy]
- An early basic remote access protocol
- Used in legacy remote communications involving modems
- Enables the authentication of connections and encryptions for the network communications, but is not considered to be as secure as more modern options
- Can automatically negotiate communications with several network communication layers at once 

###### Point-to-Point Tunneling Protocol (PPTP)
- Offers PPP-based authentication techniques
- Encrypts data carries by PPTP using Microsoft Point-to-Point Encryption (MPPE)
- Easiest to set up as most network device support it
- Not a good solution for VPN channels that require long (or near permanent) session

###### Layer Two Tunneling Protocol (L2TP)
- Works similarly to PPTP
- Uses Layer Two Forwarding that enables forwarding on the basis of MAC addressing 
- Uses IP Security (IPsec) for additional authentication and for data encryption

###### Secure Socket Tunneling Protocol (SSTP)
- Uses PPP authentication techniques
- Encapsulates the data packet in the Hypertext Transfer Protocol (HTTP) used in Web communications
- Additionally uses a Secure Sockets Layer (SSL) channel for secure communications
	- SSL is a data encryption technique employed between a server and a client
	- SSL has now evolved into Transport Layer Security (TLS)
- Only uses port 443
	- Most firewall friendly protocol
- More secure than PPTP or L2TP

###### Internet Key Exchange Version 2 Protocol (IKE v2)
- Employs IPsec in tunnel mode protocol over UDP port 500 and 4500
- Encapsulates datagrams by using IPsec ESP or AH headers for transmission over the network

**Encryption:**
- AES-256 (Advanced Encryption Standard), AES-192, AES-128, and 3DES encryption algorithms
	- 3DES is not recommended

**Pros:**
- Believed to be faster and extremely secured protocol
- IKEv2 supports mobility (MOBIKE), it is much more resilient to changing network connectivity
	- Switch between access points/wired to wireless connection/celluar networks/Wi-Fi hotspot
	- Good for remote workers on mobile devices (laptops etc)

**Cons:**
- Proprietary (like SSTP)
	- But there are open-source implementation.
	- Support by some Network Devices vendor.

![](https://i.imgur.com/LGX2APj.png)
___

## Configuring a VPN Server
---
- General steps:
	1. Install the Network Policy and Access Services role
	2. Configure a Microsoft Windows Server 2016 server as a network’s VPN server, including configuring the right protocols to provide VPN access to clients
	3. Configure a VPN server as a DHCP Relay Agent for TCP/IP communications
	4. Configure the VPN server properties
	5. Configure a remote access policy for security

###### Configuring the Server's Firewall
- The VPN server must be able to send communications through the network
	- An early configuration step is to make sure its communications can go through a firewall set up at the server
- If using Windows Firewall on the server
	- TCP and UDP ports used by VPN are unblocked by default when you configure a VPN server
	- However, it is important to make certain they are unblocked

###### Configuring VPN Properties
- After the VPN server is set up, the configuration wizard will be invoked to guide you through the configuration
- After the initial setup, you can further configure it from the Routing and Remote Access tool
	- By right-clicking the VPN server in the tree and clicking Properties
		- ![](https://i.imgur.com/9dbh1Gp.png)
		- ![](https://i.imgur.com/pYTu3Im.png)

###### Configuring a DHCP Relay Agent
- DHCP Relay Agent
	- Broadcasts IP configuration information between the DHCP server on a network and the client acquiring an address
	- Meaning:
		1. The client contacts the VPN server to make a connection
		2. The VPN server, as a DHCP relay agent, contacts the DHCP server for an IP address for the client
		3. The DHCP server notifies the VPN server of the IP address
		4. The VPN server relays this IP address assignment to the client
- VPN server can be configured as a DHCP Relay Agent using the Routing and Remote Access tool

###### Configuring VPN Security
- VPN security can be set up through a remote access policy
	- Greatly reduces administrative overhead and offers more flexibility and control for authorising connection attempts
- Establishing a Remote Access Policy:
	- Using the Routing and Remote Access tool to create and configure a remote access policy
	- To create a new remote access policy, click to activate and then right-click the Remote Access Logging & Policies folder in the tree under the VPN server
	- Click Launch NPS to launch the Network Policy Server tool

- Elements of a Remote Access Policy:
	- Access Permission
	- Conditions
	- Constraints
	- Settings

**Access Permissions:**
- Determine if access permission is enabled at the VPN server
	- Default permission for this policy is set to Deny access
- Change the default permission to Grant access in the remote access policy

**Conditions:**
- The requirements that must be met by the user or device in order to be granted remote access to an organisation's network or resources
- Can include factors such as:
	- The type of device being used
	- The user's identity and authentication credentials
	- The user's location
	- The time of day
	- The purpose of the remote access

**Constraints:**
- The restrictions that are placed on remote access
- Can include restrictions such as: 
	- The type of data that can be accessed remotely
	- The specific applications or services that can be used
	- The amount of data that can be transferred

**Settings:**
- Configuration options that can be used to control and manage remote access to an organisation's network and resources
- Can include options such as:
	- The type of encryption used for remote connections
	- The length and complexity of passwords required for authentication
	- The types of devices that are allowed to connect remotely

###### Monitoring VPN Users
- Use the Routing and Remote Access tool to monitor connected users
- With the tool open:
	- Expand the elements under the server name in the left pane
	- Click Remote Access Clients in the left pane
	- The right pane shows the users who are connected 
	- If you want to disconnect a user, right-click the user and click Disconnect
---

## Troubleshooting VPN Installations
---
###### Hardware Solutions
- Use Device Manager to make sure network adapters and WAN adapters are working properly
- Also use Device Manager to make sure that an adapter has no resource conflicts
- For an external DSL adapter or a combined DSL adapter and router
	- Make sure the device is properly configured and connected
	- Check its monitor lights for problems
- Call your ISP to determine if problems are present on the ISP’s WAN

###### Software Solutions
- Use the Services tool or Server Manager to make sure the following services are started:
	- IP Helper, Remote Access Connection Manager, IKE and AuthIP IPsec Keying Modules, Routing and Remote Access, Netlogon, Remote Access Management service, Base Filtering Engine, Windows Firewall, and Secure Socket Tunneling Protocol Service
- Ensure that the Windows Firewall is set up to allow remote access
- Make sure that the VPN server is enabled
- Check the remote access policy to be sure that access permission is <u>granted</u>
- Be certain that the VPN server is started
- In the Routing and Remote Access tool, check the network interface
- Make sure that the IP parameters are correctly configured to provide an address pool for the VPN server
- Check that the remote access policy is consistent with the users’ access needs
- If only certain clients but not all are having connection problems, try these solutions:
	- Make sure the clients are using the same communications protocol as the server
	- If you manage access to a VPN server by using security groups, make sure that each user account or computer account that needs access is in the appropriate group
---

## Remote Desktop Services
---
- Enables clients to run sessions-based desktops, virtual desktops, and software applications on Windows Server 2016 instead of at the client
	- **Session-based desktops:**
		- The client accesses an RDS server to run applications on that server during a connection session
	- **Virtual desktops:**
		- Are used in association with accessing virtual machines on a virtual server through Hyper-V
		- Multiple virtual desktops can be in a pool of desktops for different purposes
- Used for 3 broad purposes:
	- To run applications on a server instead of the client
	- To support thin clients
		- Downsized PCs that have minimal Windows-based OSs that access a Windows Server 2016 server so that most CPU-intensive operations are performed on the server
		- Generally used to save money and reduce training and support requirements
		- Also used for portable field or handheld remote devices
	- To centralise program access
		- Highly classified or sensitive documents can be stored and modified only on the server
		- Server can be configured to provide a high level of security
- Besides thin clients, RDS also supports other OSs including:
	- Windows 10
	- Windows Server 2016
	- UNIX and UNIX-based X-terminals
	- Linux
	- Mac OS
	- Tablet operating systems

###### Components Enabling Remote Desktop Server Connectivity
- Windows Server 2016 Multiuser Remote Desktop Services
- Remote Desktop Services Client
- Remote Desktop Protocol (RDP)
- Remote Desktop Services Administration Tools

###### Role Services
- Remote Desktop Session Host
- Remote Desktop Web Access
- Remote Desktop Virtualization Host
- Remote Desktop Licensing
- Remote Desktop Gateway
- Remote Desktop Connection Broker

###### Connecting Through Remote Desktop Services
- An RDS server uses RemoteApp
	- A feature that enables a client to run an application without loading a remote desktop on the client computer
	- The program appears to be just another program in a window running on the local computer
- A RemoteApp program is started by clients in the following ways:
	- From an icon on the client’s desktop 
	- From the client’s Start menu
	- As a link on a website via Remote Desktop Web Access
	- As an .rdp (remote desktop protocol) file
---

## Installing Remote Desktop Services
---
- When you install the Remote Desktop Services role, you also need to install the RDS Licensing role service
	- To manage the number of terminal server user licenses you have obtained from Microsoft
- The RDS Licensing role service can be installed when you install the Remote Desktop Services role
- Licenses can be purchased either per user account or by client device
- When you install the RDS role, you implement Network Level Authentication (NLA)
	- NLA enables authentication to take place before the RDS connection is established
	- Designed to eliminate man-in-the-middle attacks
- Another element to consider before you install the RDS role is who will be allowed to access the RDS server
	- Create groups of user accounts in advance so that you can add these groups during the installation
- If operating in an Active Directory environment
	- Consider creating a domain local group, such as RDS Users
	- Next, create different global groups of users, such as a global group for each department that will access the RDS server
	- Add the appropriate user accounts for each department’s global group
	- Finally, add the global groups to the single domain local group
---

## Built-in Remote Desktop Services
---
- The installation of a full scale Remote Desktop Services may cause a high demand on system resources
	- Remote Desktop Role and features  
- For all Windows Servers (and some Windows 10 editions), there are built-in Remote Desktop services
	- With limited number of connections
	- With simplified configuration options
	- Run on the same Remote Desktop Protocol
---

## Accessing an RDS Server from a Client 
---
- Remote Desktop Services client computers can sign in using the Remote Desktop Connection (RDC) client
	- The RDC client is already installed in Windows Vista through Windows 10 and in Windows Server 2016
- The general steps to start RDC client in Windows 10 or Windows Server 2016 are as follows:
	- Click Start and click the Windows Accessories folder
	- Click Remote Desktop Connection
	- Enter the name of the computer to access and click Connect
	- Provide the username and password and click OK
---
