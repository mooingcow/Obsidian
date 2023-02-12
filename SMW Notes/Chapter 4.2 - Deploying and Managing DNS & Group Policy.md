___

## Introduction to Group Policy
---
- Enables standardisation of the working environment of clients and servers by setting policies in Active Directory
- Group Policy:
	- Can be set for a site, domain, OU, or local computer
	- Cannot be set for non-OU folder containers
	- Settings are stored in Group Policy Objects
	- GPOs can be local or non-local
	- Can be set up to affect user accounts or computers
- When GPOs are updated, old policies are removed or updated for all clients
---

## Using Security Policies
---
###### Account Policies
- Security measures set up in a Group Policy that applies to all accounts or to all accounts in a container 
- The account policy options affect three main areas:
	1. Password Security
		- Require that all passwords have a minimum length
		- Enforce password history
		- Maximum password age (password expiration period)
		- Minimum password age (prevent reusing of old passwords)
		- Minimum password length
		- Passwords must meet complexity requirements
		- Store password using reversible encryption
	2. Account Lockout
		- Bar access to an account (including the true account owner) after a number of unsuccessful tries
		- The lockout can be set to release after a specified period of time or by intervention from the server administrator
		- Common policy is to lockout after 5 to 10 unsuccessful logon attempts
			- Administrator can set lockout to release after a designated time
	3. Kerberos Security
		- Involves the use of tickets that are exchanged between the client who requests logon and network services access and the server or Active Directory that grants access
		- Each DC is a key distribution center
		- Once a user is authenticated, the Kerberos ticket-granting service grants a permanent ticket (called a service ticket) to that computer
			- A service ticket is good for the duration of the logon session
		- Enhancements on Windows Server 2016 and Windows 10: 
			- The use of Advanced Encryption Standard (AES) encryption
			- When Active Directory is installed, the account policies enable Kerberos
			- When Active Directory is not installed, the default authentication is through Windows NT LAN Manager version 2 (NTLMv2)
		- Options available for configuring Kerberos:
			- Enforce user logon restrictions
			- Maximum lifetime for service ticket
			- Maximum lifetime for user ticket
			- Maximum lifetime for user ticket renewal
			- Maximum tolerance for computer clock synchronization

###### Audit Policies
- Events that can be audited are as follows:
	- Account logon (and logoff) events
	- Account management
	- Directory service access
	- Logon (and logoff) events at the local computer
	- Object access
	- Policy change
	- Privilege use
	- Process tracking
	- System events

###### User Rights
- Enable an account or group to perform predefined tasks
	- The most basic right is the ability to access a server
	- More advanced rights give privileges to create accounts and manage server functions
- Two general categories of rights:	
	1. Privileges – generally relate to the ability to manage server or Active Directory functions
		- Add workstations to domain
		- Back up files and directories
		- Change the system time
		- Create permanent shared objects
		- Generate security audits
		- Load and unload device drivers
		- Perform volume maintenance tasks
		- Shut down the system
	2. Logon rights – are related to how accounts, computers, and services are accessed
		- Access this computer from the network
		- Allow logon locally
		- Allow logon through Remote Desktop Services
		- Deny access to this computer from the network
		- Deny logon as a service
		- Deny logon locally
		- Deny logon through Remote Desktop Services
---

## Policy Application Order
---
- Policies can be applied at Domain level, at OU level, etc
	- Any settings that do not conflict with other settings will be applied

###### LSDOU
- Local
- Site
- Domain 
- OU
- ***Enforced***
	- Enforced setting is like a big fat man that cannot be moved
	- Once applied, **cannot be overwritten**
		- E.g. Local setting is enforced -> will not be overwritten by domain or OU policy
	- Applies to child containers (unless **blocked**)
		- Blocking GPO prevents inheritence of GPO

- Settings that conflict will be applied (until the last setting -> it become the effective setting)
	- **UNLESS:** setting is enforced (see above)

###### Resultant Set of Policy (RSoP)
- Used to make the implementation and troubleshooting of group policies much simpler for an administrator
- Can query the existing policies that are in place and then provide reports and the results of policy changes
- RSoP supports two modes: planning and logging
- Available within GMPC & Command line interface

###### GPRESULT 
- Command to be run on the workstation to check its current accepted and active GPOs
---
