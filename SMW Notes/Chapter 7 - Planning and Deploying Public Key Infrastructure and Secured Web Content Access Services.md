___

## Defining Certifcate Rquirements 
---
- Microsoft Windows Server enables secure data access based on the use of digital certificates
- Certificates allow users or systems to prove to others that they are who they say they are
- Before you can use digital certificates, you need to design a Public Key Infrastructure (PKI)

###### Example:
- To protect exchanging messages from eavesdropping attack with Asynchronous Encryption Algorithm
	- A key-pair is associated with an individual party.
	- Each individual party will keep its private key as a secret but share out its public key to everyone.
	- Messages being encrypted with the public key can only be decrypted by the corresponding private key. 
	- A digital signed message with the individual private key can only be verified by its corresponding public key.
- There is one problem
	- How can we obtain a genuine public key of a particular party before we can establish a secure communication channel with the party ?
- Public Key Infrastructure (PKI) 
	- Refers to a technology that includes a series of features relating to authentication and encryption.
	- Based on a system of certificates, each certificate contains a public key and the name of the subject.
	- Allows an organization to publish, use, renew, and/or revoke certificates and enroll clients.

- Certificates may be required if you are using any of the following applications:
	- Digital signatures
	- Secured e-mail
	- Secured HTTP communication (HTTPS/SSL)
	- Internet authentication 
	- Software code signing
	- IP security
	- Smart card logon
	- Encrypted file system
	- 802.1x authentication
---

## Certificate Authority
---
- Entity that issues digital certificates to other parties
- Root CA can issue certificates to subordinate or intermediate or issuing CAs
	- Issuing CAs can issue certificates to users or clients

###### Hierarchies
- Rooted Trust Model
	- Root CA has a self-signed certificate, and it issues a certificate to all direct subordinate CAs
	- CAs can be online or offline; allowing flexibility in deploying and managing PKI
	- Each CA serves a single role within the hierarchy and is not dependent on other CAs; more scalable and easier to administer than other hierarchies 
		- Possible to add a new CA to a hierarchy
	- Hierarchy can either be 2-tier or 3-tier hierarchy
		- All CAs are either a root or subordinate, never both
	- Each CA is reponsible for processing requests, issuing certificates, and publishing CRLs
	- Each CA can be managed independently
	- ![](https://i.imgur.com/sH3lz3K.png)
- Cross-Certification Trust Model
	- All CAs are self signed
		- Trust relationships between CAs are based on cross-certificates
			- Certificates issued by one CA will be trusted by computers from another CA hierarchy [cross hierarchy trust ]
			- Cross-Certificates do not need to be bidirectional
				- Meaning, cross certification can be established even if only one CA recognizes the other's certificates, and that it is not required for both CAs to issue and recognize each other's certificates for a cross-certification to be established
	- **Advantages:**
		- Low cost 
			- Organisations can establish trust relationships with other organizations that may not be in their same hierarchy or domain, without the need for a dedicated PKI infrastructure
		- Flexibility
			- Cross-certificates can be easily revoked and reissued, allowing for greater flexibility in managing trust relationships
	- **Disadvantages**
		- Greater administrative overhead
			- Requires more management and maintenance efforts, as well as careful planning to ensure that the appropriate certificates are being used and managed effectively
		- Increase risk of unauthorised access to internal resources
			- Creates additional pathways for attackers to gain access to systems or data if the cross certificate is compromised or falls into the wrong hands
	- ![](https://i.imgur.com/NbQkPsx.png)
- Hybrid Trust Model

###### Third-Party CAs
- Useful when an organisation conducts most of its business with external customers and clients
- **Examples:**
		- DigiCert
		- GlobalSign
		- GoDaddy
- **Advantages:**
	- Customers have a greater degree of confidence because they trust the third party CA
	- Organisation can take advantage of third party CA's understanding of technical, legal, and business issues with certificate use
- **Disadvantages:**
	- High per-certificate cost
	- Allow less flexibility in managing certificates
	- Auto-enrollment is not possible

###### Roles
- Standalone CA
	- Rudimentary CA
	- Intermediate CA
- Enterprise CA
	- Basic-Security CA
	- Medium-Security CA
	- High-Security CA

###### Installing Certificate Authority Roles
- Root CA is installed first
	- Followed by intermediate CAs
	- Finally the issuing CAs
- **Root CA:**
	- CA that is at the top of the certification hierarchy
	- Must be trusted unconditionally by all clients in an organisation
	- Enterprise Root CA stores its information in AD
		- Server that hosts CA service must be joined to a domain
	- Storing the root CA offline is much more secure
- **Intermediate CA:**
	- CA subordinate to a root CA
- **Issuing CA:**
	- Issues certificates to users and computers
---

## Selecting a Certificate Enrollment and Renewal Method
---
- Depends on:
	- Types of certificates that you intend to use 
	- Number and type of clients that you enroll
- Two types: 
	- Manual: 
		- If administrative approval is required
		- Most useful for issuing and renewing computer and IPSec certificates
	- Automatic
		- If no approval is necessary
		- Can improve administrative control over certificates

###### Methods for Auto-Enrollment
- Certificate Auto-Enrollment and Renewal: 
	- Based on a combination of Group Policy settings and certificate templates
	- Group Policy can be used to configure certificate template settings for certificate enrollment, and certificate templates can be configured with the appropriate settings for automatic renewal
- Certificate Request Wizard and Certificate Renewal Wizard: 
	- These wizards are used to request and renew certificates 
	- They can be run by end-users or administrators from the Certificate Management console.
	- Users can initiate the certificate request or renewal process themselves, without requiring direct intervention from an administrator
	- Still subject to Group Policy settings and certificate templates
	- Request must still be approved by a CA or administrator before the certificate is issued
- Web Enrollment Support Pages: 
	- Web pages provided by the CA that allow users to request and download certificates without needing to install any software
- Smart Card Enrollment Station: 
	- A specialised device that can be used to enroll users for smart card certificates
	- The enrollment station is typically connected to the CA and can be used to automate the enrollment process for large numbers of users
---

## Configuring Certificate Template
---
- Certificate Services provides certificate templates to simplify the process of requesting and issuing certificates 
- Each template contains the rules and settings
	- Can serve a single purpose or multiple purposes
- Certificate templates are available only on **Enterprise** Root and Subordinate CAs
	- Stored in Active Directory
	- Available to every enterprise CA in the forest
- Certificate Templates MMC snap-in provides administrators with the capability to:
	- Create additional templates by duplicating and modifying existing templates
	- Modify template properties 
	- Configure policies applied to certificate enrollment, issuance, and application
	- Allow the autoenrollment of certificates
	- Configure ACLs on certificate templates
- Issuance of certificate requests can be controlled in three ways:
	- Configuring permissions on the template from the Security tab
	- Preventing the CA from issuing that certificate type by deleting the template
	- Configuring the permissions on the CA
- Restrict permissions on your CAs to prevent unauthorised access
- Configure the discretionary access control list (DACL) for each template
---

## Configuring Archival and Recovery of Keys
---
- CA can be configured to archive private keys of certificates at the time of issuance; enables to recover the key should it be lost
- Only highly trusted individuals should be granted the privilege of archiving and recovering keys
- Certificate Services does not archive private keys by default
- Key recovery methods: 
	- Key recovery agent, certutil tool, and krt.exe
---

## Deploying and Revoking Certificate for Users, Computers and CAs
---
- Possible to automate the deployment of certificates by configuring Group Policy
- Manual approval should be required for:
	- All certificates that are needed to perform network administration or software development 
	- All certificates issued to joint venture partners

###### Conditions to auto-enroll certificates
- Client computer must be integrated into Active DIrectory
- Users require the Read, Enroll, and Auto-Enroll permissions

###### Reasons for revoking a certificate
- Certificate is compromised 
- Termination of the account to whom the certificate was issued

###### Certificate Revocation Lists (CRL)
- All certificates have specified lifetimes
- In some situations, there is need to invalidate or revoke a certificate before it has reached the end of its lifetime
- Revoked certificates are published in the certificate revocation list (CRL)
	- CRLs are valid only for a limited time, PKI clients need to retrieve a new CRL periodically
	- Must define the CRL location along with the access path before deploying certificates

###### OCSP (Online Certificate Status Protocol)
- An Internet protocol used for obtaining the revocation status of an X.509 digital certificate
- It complements (not replaces) the operations of CRLs [it can supersede, though]

###### OCSP Responder
- A server typically run by the certificate issuer which returns a signed response on the status of a particular issued certificate
- Possible response:
	- Good, Revoked or Unknown
	- No response
		- Issuer does not implement the responder service
---

## Secured Web Access
---
- Issues for non-secured web access:
	- How to authenticate the identity of the remote server
		- E.g.  Hackers may setup phishing site to mislead clients to submit  confidential information / even pay for an non-existing service. 
	- How to ensure the transferred content is not tampered or intercepted by unauthorized parties.
	- For Enterprise servers, they need a solution to authenticate the identity of the remote clients that trying to access to its services.  

###### Deploying and Managing SSL Certificates
- Need to install IIS in a highly secured and locked configuration
- Secure Sockets Layer (SSL)
	- Public key–based security protocol
- SSL process uses:
	- Certificates for authentication
	- Encryption for message integrity and confidentiality
- Requires installation of valid server certificate to establish encrypted communications using SSL
- Certificate-based SSL features in IIS consist of:
	- A server certificate
	- A client certificate – (optional)
	- Various digital keys
- Ways to obtain certificates:
	- Created using Certificate Services
	- Obtained from trusted third-party CA
---

## HTTPS
---
- A technology that encrypts individual messages in Web communications rather than establishing a secure channel
- Popular e-commerce technology and is used for secure online shopping
- Communicates on port 443
- SSL-secured URLs begin with https:// 
---

## Configuration of the Web Server for SSL Certificates
---
- Use SSL encryption only for sensitive information
	- Encrypted transmissions can significantly reduce transmission rates and server performance
- Server certificates provide a way for users to confirm the identity of the Web site
	- A server certificate contains:
		- Organization name affiliated with the server content
		- Name of the organization that issued the certificate
		- A public key that is used to establish an encrypted connection

###### Self-Issued Certificate
- Considerations when deciding to issue your own server certificates:
	- Microsoft Certificate Services can accommodate different certificate formats and provide for auditing and logging of certificate-related activity
	- Evaluate the cost of each certificate
	- Keep the learning curve in mind
	- Evaluate the willingness of outside vendors' clients to trust your organization as a certificate supplier

###### Publicly Issued Certificate
- Used when a user suspects your self-issued certificates
- Certificate can be obtained from a mutually trusted, third-party CA, e.g., VeriSign, GlobalSign or Thawte
- Wait time: Several days to several months
- Must be renewed on a regular basis

- General rules about any type of Web certificates:
	- Each Web site can have only one server certificate assigned to it
	- One certificate can be assigned to multiple Web sites
	- You can assign multiple IP addresses per Web site
	- You can assign multiple SSL ports per Web site
---

## Configuration of the Client for SSL Certificates
---
- Typical client certificate contains following items of information:
	- Identity of the user
	- Identity of the certification authority
	- A public key used for establishing encrypted communications
	- Validation information, such as an expiration date and serial number
- To protect your Web content from unauthorised access you must do one of the following:
	- Use Basic, Digest, or Integrated Windows authentication, in addition to requiring a client certificate
	- Create a Windows account mapping for client certificates
---

## Certificate Renewal
---
- Security and renewal requirements for certificates should be based on following factors:
	- Value of the network resources protected by the CA trust chain
	- Degree to which you trust your certificate users
	- Amount of administrative effort that you are willing to devote to certificate renewal and CA renewal
	- Business value of the certificate
![](https://i.imgur.com/L3qU2AF.png)
