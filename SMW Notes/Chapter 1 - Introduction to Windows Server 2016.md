___

## Microsoft's Commitment to Security
---
- Areas where Microsoft has decided to make a significant investment 

###### Isolation and Resiliency 
- Concept -> Split a computer into smaller separate pieces so if one piece is compromised/malfunctions, other entities in the system not affected
- Implementation -> Windows Firewall, Windows Defender, Object level access control, etc.

###### Updating
- Concept -> Primary way to protect against security vulnerabilities
- Implementation:
	- System Center Configuration Manager (SCCM)
		- Formerly know as System Management Server (SMS)
	- Windows Update Troubleshooter
	- Windows Software Update Services (WSUS)

###### Quality
- Use of quality standards and processes
- Use fo best practices in all phases of software developments
- Development of new internal tools that automatically check code for common errors
- Through testing of software before its release

###### Access Control and Authentication
- Passwords
- Smart Cards
- Public Key Infrastructure (PKI)
- Internet Protocol Security (IPsec)
- Active Directory Rights Management Services (AD RMS)
---

## Trustworthy Computing
---
- Development Emphasis: Security over Features
- A way to ensure safe and reliable computing

###### Requirements of trustworthy computing:
- Computers need to be reliable
- Software that operates on those machines must be equally reliable
- Service components have to be dependable

###### Goals of trustworthy computing:
- Security 
- Privacy
- Business Integrity

###### Means to achieve trustworthy computing
- Security by design, by default, and by deployment
- Privacy/fair information principles
- Availability, manageability, and accuracy
- Usability, responsiveness, and transparency 
---

## Trusted Cloud
---
- Trustworthy Computing expanding to the Trusted Cloud Initiative

###### Foundational Principles
- Security 
- Privacy 
- Compliance/Transparency
---

## Secure Code
---
###### Implement and Maintain Security
- Train Windows Engineers in:
	- Writing secure code
	- Specialised testing techniques
	- Threat modelling
- Writing documentation with security in mind
---

## Common Language Runtime
---
- Runtime Environment for the .NET Framework
- Manages the running of .NET programs regardless of the programming language they were written in 

###### Goals for Design of Common Language Runtime
- Simplify the development environment
- Get a simpler and safer deployment:
	- Get rid of the concept of registry (Using XML configuration files instead)
	- Use zero-impact installation
---

## Using Windows Server 2016 with Client Systems
---
- Client Workstation OS most compatible with Windows Server 2016:
	- Windows versions 7, 8, 8.1, and 10
	- Windows 10 most compatible in terms of client management

###### Client
- A computer that accesses resources on another computer via a network

###### Workstation
- A computer that has its own central processing unit (CPU) and can be used as a stand-alone or network computer

###### Total Cost of Ownership
- Overall goal of Microsoft is to achieve a lower total cost of ownership (TCO)
- TCO is the full cost of owning a network, inlcuding:
	- Hardware & Software
	- Training
	- Maintenance
	- User support costs

###### Domain 
- A grouping of network objects, such as computers, servers, and user accounts, that provides for easier management
- Computers and users in a domain can be managed to determine what resources they can access

###### Active Directory
- Database of: 
	- Computers
	- Users
	- Groups of users
	- Shared printers
	- Shared folders
	- Other network resources

###### Advantages of using Windows Server 2016 and Windows 7-10
- Enhanced capabilities to recover from many types of network communications problems
- Computer code for more efficient network communications
- More network diagnostic capabilities
- Computer code for better use of the network communications protocols
- Continuing upgrades for Windows PowerShell commands and scripts in both Windows Server 2016 and Windows 7 through 10

###### Linux Integration Services (LIS)
- Windows Server 2016 supports Linux through Linux Integration Services (LIS)
	- Enables Linux clients to access a Linux VM in Hyper-V
- New Capabilities:
	- New software for enhanced desktop graphics performance on Linux clients 
	- Improved backup support functions 
	- Creation of kernel dumps for Linux VMs
	- Better control of available RAM in Linux VMs
---

## Windows Server 2016 Features
---
###### Server Manager
- Enable the server administrator to manage critical configuration features from inside one tool
- Functions:
	- Configure a server from the beginning
	- View computer configuration information.
	- Change server roles and system properties
	- Configure networking
	- Configure Remote Desktop
	- Configure security, including the firewall
	- Add and remove features
	- Run diagnostics
	- Manage storage and backups
	- Manage multiple servers from one place

###### Security
- Essential level of security automatically implemented when new features or components added in Windows Server 2016
	- Known as security by default
- Other security features: 
	- File and folder permissions
	- Security policies
	- Encryption of data
	- Event auditing
	- Various authentication methods
	- Server management and monitoring tools

###### Enhanced Web Services
- Microsoft Internet Information Services (IIS)
	- Transforms Windows Server 2016 into a versatile Web server
- IIS has been designed to:
	- Include over 40 modules
	- Intended to enable IIS to have a lower attack surface
	- Provide easier application of IIS patches
	- Make it easier for network programmers to write network applications and configure applications for the Web

###### Windows Server Core and Nano Server
- Windows Server Core
	- A minimum server configuration
	- Designed to function in a fashion similar to traditional UNIX and Linux servers
	- Does not provide the following:
		- A graphical interface, just a command line
		- Graphical tools to configure the server
		- Extra services that you do not need
		- A mouse pointer on the screen
		- Windows Mail, Microsoft Word, search windows, and other software
- Windows Nano Server
	- A new installation option in Windows Server 2016
	- Smaller footprint than Server Core
	- Provides a basic foundation for server computing
	- Intended to be faster and need less maintenance
	- Microsoft views Nano Server as a platform on which to run a (an):
		- DNS or DHCP server
		- Applications server, such as from the cloud
		- Web server
		- Database or file server

###### Windows PowerShell
- A command-line interface that offers a shell
	- Customised environment for executing commands and scripts
		- Scripts are files that contain commands to be run by a computer OS
- Can perform the following tasks with PowerShell:
	- Work with files and folders
	- Manage disk storage
	- Manage network tasks
	- Set up local and network printing options
	- Install, list, and remove software applications
	- View information about the local computer, including user accounts
	- Manage services and processes
	- Lock a computer or log off
	- Manage IIS Web services
- Windows PowerShell offers over 130 command-line tools, also called cmdlets

###### Reliability 
- The operating system kernel runs in privileged mode
	- Protects it from problems created by a malfunctioning program or process
- The kernel consists of the core programs and the computer code of the operating system
- Privileged mode gives the operating system kernel an extra level of security from intruders
	- Prevents system crashes due to poorly written applications
- Process
	- A computer program or portion of a program that is currently running
- Protected process
	- One for which outside influences are restricted
---

## Planning a Windows Server 2016 Networking Model
---
###### Network
- A communications system enabling computer users to share computer equipment, application software, and data, voice, and video transmissions
- Contains computers joined by communications cabling or sometimes by wireless devices

###### Workstation or client network operating system
- Enables individual computer to access a network, and in some cases to share resources

###### Peer-to-peer networking
- Focuses on spreading network resource administration among server and nonserver members of a network
- Uses workstations to share resources such as files and printers and to connect to resources on other computers
	- No special computer is needed to enable workstations to communicate and share resources
- Can be effective for very small networks
	- Does not requires server setup nor Active Directory services
- Disadvantages:
	- Management of network resources is decentralized
	- As the network increases in size, administration becomes more difficult
	- Lack of security of resources

###### Server-based networking
- Centralizes the network administration on one or more servers
- Server
	- A single computer that provides extensive multiuser access to network resources
	- Can handle hundreds of users at once
		- Fast response when delivering the shared resource
		- Less network congestion when multiple workstations access that resource
- Advantages
	- Users only need to log on once to gain access to network resources
	- Security is stronger
	- All members can share computer files
	- Printers and other resources can be shared
	- All members can have e-mail and send messages to other office members through an e-mail server
	- Software applications can be stored and shared in a central location
	- Important databases can be managed and secured from one computer
	- All computers can be backed up more easily
	- Computer resource sharing can be arranged to reflect the work patterns of groups within an organization
	- The server administrator can save time when installing software upgrades
---

## Protocols for the Windows Server 2016 Networking Model
---
- A protocol consists of guidelines for the following:
	- How data is formatted into discrete units called packets and frames
	- How packets and frames are transmitted across one or more networks
	- How packets and frames are interpreted at the receiving end
- Packets and frames
	- Units of data transmitted from a sending computer to a receiving computer
- Windows Server 2016 and its clients primarily use the Transmission Control Protocol/Internet Protocol (TCP/IP)
	- A suite of protocols and utilities that support communication across LANs and the Internet
- Local area network (LAN)
	- A network of computers in relatively close proximity

###### Transmission Control Protocol
- Provides for reliable end-to-end delivery of data by controlling data flow
	- Computer agree on a “window” for data transmission that includes the number of bytes to be sent
	- Window is constantly adjusted to account for existing network traffic
- TCP is also considered a connection-oriented communication
	- Ensures that packets are delivered, that they are delivered in the right sequence, and that their contents are accurate

###### Address Resolution Protocol
- Used to acquire the physical addresses associated with a computer’s network interface card (NIC)
- Every NIC has a physical address, or media access control (MAC) address
- For computers to communicate with each other
	- They must know the MAC addresses of each other’s network interface cards
- Proper communications using TCP/IP rely on both IP addresses and MAC addresses
- Every computer running Windows Server 2016 has an ARP cache
	- Contains recently resolved MAC addresses as well as statically assigned values in the ARP cache
	- arp –a command shows the contents of ARP cache

###### Automated Address Configuration
- Automatic Private IP Addressing (APIPA)
	- Used to automatically configure the TCP/IP settings for a computer without using a DHCP server
	- Computer automatically assigns itself an IP address from the reserved range of 169.254.0.1 to 169.254.255.254 and a subnet mask of 255.255.0.0
	- Appropriate for small organizations that have only one network segment and do not need to access another network or the Internet
	- Automatic configuration can be disabled through the Windows Server 2016 Registry
		- Registry is a database used to store information about the configuration, program setup, devices, drivers, and other data important to the setup of Windows OSs
- Dynamic Addressing Through a DHCP Server
	- Common for medium-sized and large networks
	- Must first install and configure a DHCP server on the network
	- In addition to assigning the IP address, the DHCP server can also assign the subnet mask, default gateway, DNS server, and other IP settings
	- Using a DHCP server can save you a great deal of administrative effort
---
