___

## Microsoft's Commitment to Security
---
- Areas where Microsoft has decided to make a significant investment 

###### Isolation and Resiliency 
- Concept -> Split a computer into smaller separate pieces so if one piece is compromised/malfunctions, other entities in the system not affected
- Implementation -> Firewall, Object level access control, etc.

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