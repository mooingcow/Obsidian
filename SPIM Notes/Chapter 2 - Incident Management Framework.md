--- 

## Cyber Incident Response Life Cycle
---
![](https://i.imgur.com/Fdu32Kr.png)

###### Preparation
- Prevent incidents by ensuring that systems, networks, and applications are **sufficiently secure *in advance***
	- Designing system securely
	- Implementing defense mechanisms
	- Proactively looking for threats
###### Detection
- Collecting and processing data from system sources (SEIM, IDPSs, antivirus software, and log analysers)
	- Classification of cyber incidents by types
	- Prioritising cyber incidents 
	- Mananging incidents investigation
	- Incident documentation
- **Signs of Incidents**
	- Precursor --> A sign that an incident may occur in the future
	- Indication --> A sign that an incident may have occured or may be occuring now 
		- ![](https://i.imgur.com/vZq7eGY.png)
		- ![](https://i.imgur.com/0uCGQif.png)
###### Analysis
- Inspecting alerts, raw events, application and system logs
	- Working quickly to analyse and validate each incident, following a pre-defined process and documenting each step taken
	- Identifying the attacker and targets
	- Assessing the risk to business processes
	- Escalating to relevant personnel for further analysis
	- Analyse if it is a targeted attack or an in-the-wild threat
- **Analysis Steps**
	- Correlation
		- Identify if the detected activity is a characteristic of an intrusion attempt
	- Structural Analysis
		- Identify if the detected activity is a characteristic of a known intrusion path
	- Intrusion Path Analysis
		- Identify if the intended target is vulnerable to the detected activity
	- Behaviour Analysis
		- Identify if the detected ability is permitted by security policy
###### Containment/Eradication
- Contain the threat
	- Prevent threat from spreading further
	- Prevent data leakage to the attacker (block communication, disable accounts…)
- Elimination of incident components
	- Clean infected machines
	- Disable breached accounts
- Evidence should be collected according to procedures that meet all applicable laws and regulations
- If the alert is of a known issue act of predefined knowledge base and decision support.
###### Recovery
- Restore systems to normal operation
- Revert any limitations that were used for isolation (firewall)
- Confirm that the systems are functioning normally
	- If needed, restoring systems and/or files from clean backups
###### Post Incident Activity (AR)
- AR meetings with all involved parties after a major incident
	- Chain of events (events and times)
	- Findings – what actually happened (unauthorized access)
	- Conclusions – what is the problem that allowed it (open port, weak password…)
	-  Recommendations
		- What needs to be done (action items. close ports, stronger password…
		- Proactive updates (security policy update, training, new product)
- Updating the knowledge base with the specific incident details for next time handling
- Recognise security weaknesses and threats
- Identifying and mitigating all vulnerabilities that were exploited