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
2. AS validates the request as coming from a valid user and generates a TGT and another message encrypted with the user's secret key
3. User decrypts the message and generates more messages, before sending it and the TGT to the TGS
4. TGS decrypts TGT and validates it, and generates a ST and another encrypted message, which is sent back to the user
5. User decrypts the message and creates an authenticator message, and sends ST and authenticator message to the service
6. Service creates its own authenticator message and sends it back to the user 
	- Allows user and service to mutually authenticate 
	- Distribute a symmetric service session key

###### Detailed Workflow
1. User sends a request
	- ![](https://i.imgur.com/yChtDTi.png)
2. AS retrieves client secret key after verifying the userid and sends back the following: 
	- ![](https://i.imgur.com/QQdk0u2.png)
	- ![](https://i.imgur.com/E0qvwZ3.png)
3. (a) Client decrypts the first message using the client secret key, which is a hash of:
	- ![](https://i.imgur.com/AtAtStx.png)
3. (b) Client generates 2 new messages, and sends it + TGT to the TGS
	- ![](https://i.imgur.com/ykGG4wD.png)
4. (a) TGS decrypts TGT using the TGS secret key, and uses the TGS session key to decrypt the authenticator message, before validating the authenticator message against the TGT
	- Note: Kerberos allows for delay of less than 2 minutes for the timestamp
	- TGS also checks the TGS cache to see if the authenticator can be found inside (provides replay protection); else authenticator is stored inside
	- ![](https://i.imgur.com/3povn5I.png)
4. (b)  ST is generated with another encrypted message and sent back to the user
	- ![](https://i.imgur.com/xGwLLbb.png)
5. User decrypts the message and obtains the Service Session Key, to encrypt the authenticator message and sends it + ST to the service
	- ![](https://i.imgur.com/nhUUJls.png)
6. (a) Service decrypts ST using service secret key, and uses service session key to decrypt the authenticator message before validating the authenticator message against the ST
	- Note: Kerberos allows for delay of less than 2 minutes for the timestamp
	- Service also checks the service cache to see if the authenticator can be found inside (provides replay protection); else authenticator is stored inside
	- ![](https://i.imgur.com/o1wQaJf.png)
6. (b) Service sends user a service authenticator message, encrypted by the service session key
	- ![](https://i.imgur.com/pLSdVix.png)
6. (c) The user will decrypt the authenticator and verify that the service name is correct (expected service) 
	- Note: Kerberos allows for delay of less than 2 minutes for the timestamp
	- User also checks the user cache to see if the encrypted service ticket can be found inside; else service ticket is stored inside for future use
	- ![](https://i.imgur.com/HWffPWW.png)



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