___

## Kerberos
---
3 parties: 
- Client (Usually user)
- Resource (Files on a File Server)
- Key Distribution Centre (DC)

NOTE: KDC does not communicate with the resource (provider). Authentication workload handled by the client

Kerberos Workflow
1. Client is trying to login, so it constructs an authenticator

###### Terminology
- Kerberos Realm
	- Domain/group of systems that Kerberos has the authority to authenticate a user to a service
	- Can have multiple realms, can be interconnected
- Principal
	- Found within a realm
	- A unique identity (for a user or service)
- KDC
	- Supplies tickets and generates temporary session keys
	- Consists of 2 servers
		- Authentication Server(AS)
			- Confirms that a known (valid) user is making an access request 
			- Issues Ticket Granting Tickets (TGT)
		- Ticket Granting Server (TGS)
			- Confirms that a user is making a request to a known service
			- Issues Service Tickets (ST)
- Messages
	- Authenticators
		- Record containing information recently generated using the session key known only to the client and the server
		- Allow the user to authenticate to the service, and the service to authenticate to the user 
			- Mutual Authentication 
	- Tickets
		- Contain most of the information
			- Client's identity
			- Service ID
			- Session Key
			- Timestamp
			- Time Validity
		- Encrypted using the server's secret key

###### High Level Workflow
1. User sends a request to access a service to the AS
2. AS validates the request as coming from a valid user
3. Generates a TGT and another message encrypted with the user's secret key
4. User decrypts the message and generates more messages, before sending it and the TGT to the TGS
5. TGS decrypts TGT and validates it, and generates a ST
6. ST and another encrypted message is sent back to the user
7. User decrypts the message and creates an authenticator message 
8. User sends ST and authenticator message to the service
9. Service creates its own authenticator message and sends it back to the user 
	- Allows user and service to mutually authenticate 
	- Distribute a symmetric service session key

###### Detailed Workflow
1. User sends a request
	- 

## NTLM v2
---
###### NTLM Applications
- No Kerberos trust between forests
- Authentication is attempted by IP
	- Kerberos requires a domain name environment 
- If the systems are not in the same domain
- If the firewall is blocking Kerberos ports

###### Workflow
- Uses a challenge, response algorithm
	- Passwords not transmitted
1. User tries to login at the client device
2. Client hashes the password 
3. Client sends a login request
4. DC generates a random string (challenge) and sends it to the client
5. Client will **encrypt** the challenge with the hash of password (response) and send the userid, challenge, and response back to the DC
6. DC will use the user's password hash (based on the userid), and encrypt the challenge 
7. If encrypted challenge = client response, then the user is authenticated. 
8. DC sends a session key to the client, encrypted with the hash of the user's password