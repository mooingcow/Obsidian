
# 08 Crime and Incident Scene Processing
---

## Identifying Digital Evidence
---
###### digital evidence
- any info stored/transmitted in digital form
- diff between document evi and digital evi
    - document evi always visible on its face
- US court accept digital evi as physical evi
    - treated as tangible object

- scientific working group on digital evi (SWGDE) set standards for recovering , preserving and examining digital evi

###### tasks performed with digital evidence
- identify digital info/artifacts that can be used as evi
- collect/preserve/document evi
- analyse/identify/organise evi
- rebuild evi or repeat situation to verify that results can be reproduced reliably

![](https://i.imgur.com/PumUMSF.png)
- systematic approach for collecting digital devices and processing criminal/incident scene
---

## Rules of Evidence
---
###### good practices
- consistent practices help verify work and enhance credibility 
    - handle evi consistently
- comply with state's rules of evi or federal rules of evi
    - eg. security and accountability control for evi
- evi submitted in criminal case can be used in civil suit (vice versa)
- keep current on latest rulings and directives on collecting, processing, storing and admitting digital evi

###### other rules
- digital evi diff from phy since changed more easily
    - only way to detect changes by comparing hashes
- most courts interpret comp records as hearsay evi
    - hearsay is second hand/indirect evi
        - evi of statement made other than by a witness
- digital records admissible if business record
---
#### Computer Records
###### types
- computer generated or
- computer stored

###### computer generated records
- data maintained by system & not created by human
	- eg. log files

###### computer stored records
- data created by human saved on comp
	- eg. spreadsheet/word doc

###### rules
- computer and digital records must be shown to be authentic and trustworthy to admit into court
    - comp gen records authentic if program creating it is functioning correctly
        - no bugs
        - exception to hearsay rule
- collect evi according to proper steps to ensure its authentic

###### challenges
- when attorneys challenge digital evi, they raise issue whether computer generated records are altered or damaged
- one test to prove computer stored records authenticity is demonstrating that a specific person created them
    - eg. file metadata to see author
    - HOWEVER records recovered from slack space/unallocated disk space usually dont identify author
- process of establishing digital evi's trustworthiness originated from **best evidence rule**

###### best evidence rule
- to prove content of written doc/recording/photo, the orignal is required
- allow duplicate when its produced by same impression as original
	- not always possible to produce orig
	- eg. when cannot use original evidence
		- network servers - cannot remove from network to acquire evidence since will cause harm to business/owner (innocent)
- data can be admitted in court as long as bit-stream copies of data created and maintained
    - though not best evidence
---
#### Properties
- admissible
- authentic
- complete
- reliable
- believable
---

## Collecting Evidence in Private-Sector Incident Scenes
---
- use inventory db to understand what hardware/software needed to analyse policy violation
- corporate policy statement abt misuse of digital assets
    - allow corporate investigators to conduct **covert surveillance**
        - survelliance on someone w/o person noticing it
    - access company systems w/o warrant
- companies must display warning banner and publish policy
    - state that they reserve the right to inspect computing assets at will
- corporate investigators should know what circumstance they can examine employee's computer
    - every organisation must have well-defined process describing this
- if inves finds employee **guilty** of a crime
    - employer can file criminal complaint with police
    - investigator should immediately report to corporate management
- employers interested in enforcing company policy, not seek and prosecute employees
    - corporate investigators protect company's assets
- if discover evidence of crime during company policy inves.
    - determine whether incident meets elements of law
    - inform management of incident
    - stop inves. to ensure dont violate 4th amendment restrictions on obtaining evidence
    - work with corporate attorney on how to respond to police request for more info
---

## Processing Law Enforcement Crime Scenes
---
- familiar with crminal rules of search and seizure
    - understand how search warrant works and how to process
- law enforcement officer can search and seize evidence only with **probable cause**
    - reasonable grounds to believe that person has committed crime
		- to justify making search/preferring charge
    - refers to standard specifying whether police officer has right to make arrest, conduct search or obtain warrant for arrest
- with probable cause, officer can obtain search warrant from judge
    - authorise search and seizure of specific evidence
- 4th amendment states that only warrants describing place to be searched and persons/things to be seized can be issued
---

## Concepts and Terms in Warrants
---
###### innocent info
- unrelated info
	- often included in info u looking for
	- sort info to obtain what u need
- eg. enron case - by use of accounting loopholes and poor financial reporting

###### limiting phrase
- judges often issue **limiting phrase** to warrant
    - allow police to separate innocent info from evi
    - warrant must list items to be seized

###### plain view doctrine
- objects falling in plain view of officer is subject to seizure w/o warrant
	- can be introduced as evi
- **criteria to met:**
	1. officer is legally allowed to be where he/she is
	2. ordinary sense must not be enhanced by advanced tech
	3. discovery must be by chance
- **HOWEVER**, plain view's doctrine rejected in digital forensics
	- eg. if examiner finds extra info relating to diff crime, must get extra warrant/expansion of existing warrant to continue search for said crime
---

## Preparing for a Search
---
###### tasks
- get answer from victim/informant
	- manager/coworker of person of interest to inves.
	- police assigned to case
	- law enforcement witness
---
#### steps
- identify nature of case
- identify type of os or digital evidence
- determine whether you can seize computers/devices
- use extra technical expertise 
- determine tools needed

###### identify nature of case
- private or public sector
- dictates how u proceed and types of assets/resources to use

###### identify type of os or digital evidence
- for law enforcement
	- difficult since crime scene not controlled
- identify os/device by estimating size of drive on suspect computer
	- how many devices to process at scene
- determine os/hardware involved

###### determine whether u can seize computers/devices
- type of case and location of evi
	- can u remove the evi?
- law enforcement investigation need warrant to remove computers from scene and transport to lab
	- if removing comps will harm business, shouldnt be taken offsite
- extra complications
	- file stored off-site accessed remotely
	- availability of cloud storage - cannot locate physically
		- stored on drives with multiple subscribers
- determine resources needed to acquire evi and tools to speed data acquisition if not allowed to take computers

###### use extra technical expertise
- specialised help to process incident/scene
	- specialists in
		- OS
		- RAID servers
		- db
- educate specialists in inves. techniques too prevent evi damage

###### determine tools needed
- after info gathering on incident/scene
- create **initial resp field kit**
	- lightweight and easy to transport
	- ![](https://i.imgur.com/W2oPuOK.png)
- create **extensive resp field kit**
	- all tools u can take to field
	- extract only items needed when at scene
	- ![](https://i.imgur.com/hdLFGXw.png)
---

## Preparing to Acquire Digital Evidence
---
- depends on nature of case and alleged crime
- ask supervisor/senior
    - need take entire comp and all peripherals in immediate area?
    - how to protect comp and media during transportation to lab?
    - computer powered on when arrive?
        - data might be lost if machine powered down
    - is suspect in immediate area?
        - sometimes company dw employee to know inves. is happening
    - did suspect damage/destroy computer/peripherals?
    - need to seperate suspect from computer?
---

## Processing Incident or Crime Scene
---
###### General Guidelines
- keep journal to document activities
- secure scene
    - professional and courteous to onlookers
    - remove unrelated people
- video and record area around computer
    - return belongings to orignal locations
    - pay attention to details
- sketch incident/scene
- check state of computers asap
- dont cut power to running system unless is older windows 9x or MS-DOS system
    - might lose essential network activity records w/o proper shutdown
- save data from current apps as safe as possible
- record all active windows/shell sessions
- note everything u do from live suspect computer
- close apps and shutdown computer
- bag and tag evi
    - assign 1 person to collect and log all evi
        - min num of people handling evi
        - ensure integrity
    - tag all evi with current date time, serial nums or unique features, make and model, and name of person collecting it
    - 2 separate logs of collected evi
        - verification and audit purpose
    - maintain constant control of collected evi and crime scene
- look for related info
    - password, pin, bank account
- collect documentation and media related
    - hardware/software/backups/doc/manuals
---
###### Processing Data Centers with RAID Systems
##### sparse acquisition
- technique for extracting evi from large systems
- only extract related data
- **disadvantage:**
	- dont recover data in free/slack space
---
###### Technical Advisor
- can help
    - list tools needed to process incident
    - guide where to locate data and help extract log records
        - or other evi from large RAID servers
    - create search warrant by itemising what u need for warrant
- responsibilities
    - know all aspects of seized system
    - direct investigator handling sensitive material
    - help secure scene
    - document planning strategy
    - conduct ad hoc trainings on tech and components seized and searched
    - document activities
    - conduct search and seizure
---

## Documenting Evidence in Lab
---
- record activities and findings
    - maintain journal
    - serves as reference for methods used to process evi
- goal to reproduce same results when another investigator repeat steps
---
###### Processing and Handling Digital Evidence
- maintain integrity of evi in lab
- steps to create img files
    1. copy all files to large drive
    2. use forensics tool to analyse evi
    3. run md5 or sha1 hashing algo on img files
    4. secure original media in evi locker
---
###### Storing Digital Evidence
- media used to store evi depends on how long you need to keep it
- cd, dvd, dvd-r, dvd+r, dvd-rw
    - ideal
    - capacity
        - up to 17 gb
    - lifespan
        - 2 to 5 years
- magnetic tapes - 4mm DAT
    - capacity
        - 40 to 72 gb
    - lifespan
        - 30 years
    - costs
        - drive
            - $400 to $800
        - tape
            - $40
- super digital linear tape (super DLT or SDLT)
    - designed for large RAID data backups
    - can store > 1tb
    - smaller SDLT drives can connect to workstation through SCSI card

- dont rely on media storage method to preserve evi
    - make 2 copies of every img to prevent 2 imgs
---
###### Evidence Retention and Media Storage Needs
- maintain [[Chapter 2 - Understanding Computer Investigations#^efb39a|chain of custody]] for digital evi
    - restrict access to lab & evi storage area
- lab should have sign in roster for all visitors
    - maintain logs for period based on legal requirements
- might need to retain evi indefinitely
    - check with local prosecuting attorney's office or state laws to ensure you in compliance

![](https://i.imgur.com/cvhbJSG.png)

---
###### Documenting Evidence
- create/use evi custody form
	- identify evi
	- identifies who handled evi
	- lists date and times evi handled
- extra info
	- section listing md5 and sha1 hashes
- include detailed info to reference
- evi bags also include labels or evi forms to document evi
    - use antistatic bags for electronic components
---
###### Obtaining Digital Hash
##### rules
- cant predict hash val of file or device
- no 2 hash vals can be same
- hash change if anything in file change

##### hash functions
- cyclic redundancy check (crc)
    - math algorithm that determines whether file's contents changed
    - not forensic hashing algo
- message digest 5 (md5)
    - math formula that translates file into hex val or hash val
    - hash changes if bit or byte changes
    - verify non tampered file
- secure algo ver 1 (sha1)
    - newer hash algo
	- not secure now
---
## Reviewing a Case
---
- general tasks to perform
    - identify case requirements
    - plan inves.
    - conduct inves.
    - complete case report
    - critique case

![](https://i.imgur.com/qFwuWTR.png)

---

## Samples
---
###### Sample Civil Investigation
- most cases in corporate environment considered low level investigations
    - or non criminal cases
- common activities and practices
    - recover specific evi
        - eg. outlook
    - covert surveillance
        - must be well defined in company policy
        - risk of civil or criminal liability
    - sniffing tools for data transmissions
        - eg. wireshark

###### Sample Criminal Investigation
- comp crimes eg
    - fraud
    - check fraud
    - homicides
    - etc
- need search warrant to seize evi
    - limited area
---

## Summary
---
![](https://i.imgur.com/cI9dYMb.png)
![](https://i.imgur.com/hovlrXl.png)
![](https://i.imgur.com/Gw0xFZ2.png)
