___

## Managing Updates
---
- Patch management
	- Method for keeping computers up to date with new software releases
- Security patch management: 
	- Patch management with a focus on reducing security vulnerabilities; essential for secure IT management and operations

###### Microsoft Update and Automatic Updates
- For consumers and small businesses (fewer than 50 computers)
- Updates can be installed with minimal or no user interaction
- Uses Internet connection to search for downloads from Microsoft Update website
- No need to understand the technical details of the security update
- Users should ensure they do not have applications that could be affected by the updates
- **Price:** Free for licensed users

###### Windows Server Update Services (WSUS)
- For medium or large businesses
- Administrators can manage update settings and control the distribution of updates
- Administrators can test updates on selected computers before deploying to the rest of the network
- Updates can be downloaded once from Microsoft Update Website and stored on local server (free up Internet bandwidth)
- Does not support deployment of non-Microsoft updates
- **Price:** Free for licensed users

###### Microsoft Endpoint Manager
- Comprises many configuration tools
	- Microsoft System Centre Configuration Manager (SCCM)
- Supports management and distribution of Microsoft and non-Microsoft software updates and applications
- Supports various types of endpoints : Windows / Non-Windows platforms.
- WSUS is part of it.
- Advanced administrator control features
- **Price:** Charges apply
---

## Windows Server Update Services (WSUS)
---
###### Advantages
- System administrator controls the updates to be applied
- Clients can be configured to get updates from a local WSUS server instead of downloading them from Microsoft’s site, reducing network traffic
	- WSUS is a means to provide updates to computers that don’t have Internet access

###### Requirements
- Assuming that WSUS clients are synchronizing with the server every eight hours for a rollup of 30,000 clients.
- Processor: 1.4 gigahertz (GHz) x64 processor (2 Ghz or faster is recommended)
- Memory: additional 2 GB of RAM
- Available disk space: 40 GB
- *Applies To: Windows Server 2019, Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012*

###### Features
- Administrator must approve updates before WSUS clients can install them
- WSUS clients can be controlled by Group Policy to connect to WSUS Server to check for updates
- After updating, WSUS clients will notify WSUS Server
	- WSUS Server can maintain update status of all clients

###### Operations 
- Synchronisation: 
	- WSUS Server need Internet access to Microsoft Update server to get information about security updates
	- Initial synchronisation may take a while depending on the selection choices
	- New updates can be: 
		- Automatically approve new versions of previously approved updates
		- Do not automatically approve new versions of approved updates
			- Better in a testing environment, otherwise testers may miss testing it
- Logs: 
	- Synchronization log: keeps following information:
		- Time of the last and next scheduled synchronization
		- Success and Failure notification
		- Update packages that have been downloaded and/or updated since the last synchronization, or that failed synchronization
		- Whether synchronization was a Manual or Automatic
	- Approval log: keeps track of the content that has been approved or not approved

###### Policy Options
![](https://i.imgur.com/anffJe9.png)

###### Computer Groups
- Pilot/Test Group: 
	- Some clients can be put into a “test” computer group
	- Administrator approves new security updates for the “test” group
	- Administrators test the results before allowing other computers to apply the updates
- Update Group: 
	- Servers with the same roles can be put into the same group
	- They can receive relevant updates at the same time.
---

## Patch Management Process
---
###### Five-Stage Approach
1. Receive Microsoft Security Release Communications
2. Evaluate Risk
3. Evaluate Mitigation
4. Deploy Updates
	- 6 steps  
5. Monitor Systems

###### 1. Receive Microsoft Security Release Communications
- Microsoft sends out a notification if there is issue affecting customers’ security
- If security changes are required, a security update is released.
- Patch Tuesday
	- Security updates and the corresponding security bulletin normally released on the second Tuesday and sometimes fourth of the month.
- "Exploit Wednesday"
	- This term was coined as many exploitation events were seen shortly after the release of a patch
- Since 2015, Microsoft releases security updates to home PCs, tablets, and phones as soon as they are ready, while enterprise customers will stay on the monthly update cycle
	- Urgent updates will be released immediately
- Ways of receiving information about updates:
	- Email: Security Notification Service Comprehensive Edition 
		- Update installers are never attached to the email
	- RSS: Comprehensive Alerts
	- Twitter
	- Security Update Portal 

###### 2. Evaluate Risk
1. Does the vulnerability apply to the organization? 
	- System admin should have an up to date inventory list of all IT assets of the organization.
2. Does the vulnerability represent a high risk to the organization?

- Deployment of a security update has a cost: 
	- Costs of testing the updates
	- Costs of ‘deploying’ the updates
	- Support costs in case of any negative result after the update 
		- Example: important application does not work properly after update

**Severity Ratings:**
- ***Critical:*** 
	- A vulnerability whose exploitation could enable the propagation of an Internet worm with little or no user action.
- ***Important:*** 
	- A vulnerability whose exploitation could result in compromise of the confidentiality, integrity, or availability of users’ data, or of the integrity or availability of processing resources.
- ***Moderate:***
	- A vulnerability whose exploitation is mitigated to a significant degree by factors such as default configuration, auditing, or difficulty of exploitation. 
- ***Low:*** 
	- A vulnerability whose exploitation is extremely difficult, or whose impact is minimal.

###### 3. Evaluate Mitigation
- While administrators are evaluating security updates, some short-term security control may be applied.
	- Example: adjust firewall policies, or restrict a port only to a specific subnet instead of the whole network.
- Microsoft may provide some suggested mitigation or workarounds in their security advisories if the security update can not be applied immediately
- Mitigations and workarounds are meant for **short-term use**, they do not replace security updates

###### 4. Deploy Updates
| Step | Action |
| --- | ---|
| 1. Plan the deployment | Determine which updates need to be rolled out quickly and which ones can be subjected to a more thorough testing process <br> <br>  Deployment Schedule - do some computer groups need the updates more urgently? By which date or time, must all computers be updated? |
| 2. Determine whether the security update is ready for download | If there is no security update available, Microsoft would advise the appropriate actions to take to protect the computer systems <br> <br> *Mitigations and Workarounds* |
| 3. Obtain the required update files | Security update files can be obtained from: <br> - Microsoft security guide <br> - Microsoft deployment tools, e.g. Microsoft Update, Windows Update, WSUS, or Endpoint Manager <br> - Microsoft Download Center <br> - Microsoft Update Catalog service
| 4. Create the update package | If security updates need to be customised | 
| 5. Test the package | - Ensure that business-critical systems will continue to run successfully after the security update has been deployed <br> - Ensure the package can be ‘uninstalled’ or there is a way to roll back <br> - Ensure the system can be  restarted properly <br> - Ensure the update is effective <br> <br> Updates can be tested in: <br> i. Test Enviroment <br> &emsp; - Test lab with computers mirroring the actual environment <br> &emsp; - Extra overhead incurred <br> ii. Pilot Environment <br> &emsp; - Test on selected production computers <br> &emsp; - Authentic <br> &emsp; - Can test the deployment plan too <br> &emsp; - Extra risk incurred
| 6. Rolling out the dpeloyment | - Carry out the deployment of the update to the computers that need it <br> - Compliant to  the Standard Patch Deployment Timeline | 

######  5. Monitor Systems
- Determine which systems successfully deployed the update and which systems did not.
	- WSUS , EndPoint Manager features
- Possible reasons why update was not successfully deployed:
	- The computer is offline
	- The computer is being rebuilt or reimaged
	- The computer has insufficient disk space
	- The computer is not communicating with the update server
	- The required update client software is not running on the computer
	- The computer is missing some dependent software
---

## Post-Deployment Review
--- 
- Conducted after the deploymet
- Review includes: 
	- Review organisation’s performance during the incident
	- Discuss changes to the service windows
	- Assess the total incident damage and cost (if any)
	- Update the existing baseline for the environment
--- 

## Common Fixes for Windows Update Errors
---
- Checking the disk storage
	- The system may not have sufficient disk storage to support the download and installation requirement
- Windows Update Catalog
	- Download the specific update package from Windows Update Catalog Web Site and install the update locally
- Windows Update Troubleshooter
	- A free tool from Microsoft which can fix most of the common Windows updates errors
---
