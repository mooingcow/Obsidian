
# 10 Android Forensics Part 1
---

## Introduction to Android Forensics
---
- deals with extracting, recovering, and analysing data present on an Android device 
- due to open nature of the Android operating system
	- forensic techniques apply to any device that runs Android Operating Systems (OS)
---

## Challenges of Mobile Forensics
---
- the wide range of operating systems and device models
- preventing Data Alterations on mobile devices
- inherent security features
- legal issues
---

## Seizure and Isolation
---
###### seizure
1. note location of mobile
2. take picture of the location
3. [[Chapter 2 - Understanding Computer Investigations#^efb39a|chain of custody]] 
4. take pictures of the crime scene before starting any progress
		- original state of the mobile device
		- brand
		- model
		- serial number
		- IMEI number or operating system version
5. request for pin, pattern, passwords, SIM pin
6. check for any Unified Endpoint Management solutions
7. note the status of the device
	- whether it’s powered off or on
	- if it is powered on then, check the battery status, network status
	- check where the screen is locked
8. search/request for the SIM and if any cables are located around
---
###### isolation techniques (on)
1. activate airplane mode
2. check and manually disable:
	- “hotspots” or any GPS locations
	- Wi-Fi and Bluetooth toggles
3. do not remove the SIM or SD card 
4. connect the phone to a power bank
5. place the phone, adapter, and charger into the Faraday bag (if possible)
---
###### isolation techniques (off)
**note:** do not turn on the device
1. place it in an evidence bag or box
2. place the phone, adapter, and charger into the Faraday bag (if possible)
3. Bring it back to Forensic Lab
4. write-protect the SD card & remove the SIM card
5. do an acquisition of SIM and SD card.
6. if necessary to turn it on, apply the above isolation techniques
---
###### forensic acquisition
- the process of acquiring the original evidence while maintaining its integrity
	- AKA imaging
- can be done on-site (at the scene) or off-site (in the lab)
---
###### hashing
- done after acquisition of device
- used to prove the integrity of the evidence
- MD5 or SHA are widely used algorithms to calculate the hash values
- should be documented as well to maintain record of the digital evidence
---

## Gathering Information on Device Accessibility
---
###### factors for data collection on android
- android version
- device security
	- pattern
	- PIN
	- password
	- fingerprint
	- face recognition mechanism
	- bluetooth device lock & unlock
- device accessibility
	- non-root access
	- root access
- mode of transfers
	- depends on availability & device status
	- modes:
		- USB connectivity
		- bluetooth: 
			- by utilising Android Debug Bridge (ADB) via bluetooth connection
		- wireless: 
			- mobile device & acquisition machine must be connected to same wifi network
			- acquisition performed using android device bridge via WiFi
---

## Prerequisites
---
- usually done before/during acquisition

###### media transfer protocol (MTP)
- allows media files to be transferred automatically to and from portable device
- ensured for uninterrupted device acquisition

###### enabling USB debugging
- a developer option which enables analysis machine to establish connection with the device via android debug bridge (ADB)
- ADB acts as a bridge between computer and the mobile phone
	- for computer to communicate with the phone
- to work with ADB, USB debugging options should be enabled on the phone

###### enable stay awake / increase screen time
- enabling stay awake and charging the device will make the device stay awake 
- device doesn't get locked
- usually found under settings / developer options
---

## Types of Acquisitions
---
![](https://i.imgur.com/80mJu3M.png)
___
###### advance logical
- combines both logical and file system extraction methods

###### manual
- the examiner uses the UI of the phone to browse and investigate
- no special tools or techniques required
- manual extraction of chat messages 
	- screenshot 
	- export to external media
- **however**, only files and data visible through the normal UI can be found
- data extracted through other methods can be verified using this
- very easily to modify data on the device

###### brute force
 - offensive techniques: 
 - password, pattern, or pin cracking
 - rooting the device
---

## Operating Modes of Android
---
###### operating modes
- android safe mode
- recovery mode 
- fastboot mode

###### android safe mode
- safe mode builds a clean and secure environment
- third-party apps are disabled and greyed out
- troubleshoot smartphone’s problems:
	- restarting itself
	- lagging
	- freezing
	- battery issues
	- data disappearing

###### android recovery mode
- android-based, lightweight runtime environment 
- separate from and parallel to the main Android operating system
- two kinds of recoveries
	- stock recovery
	- custom recovery
- in recovery mode, you will get some advanced options
- several custom recovery images available
	- ClockworkModRecovery 
	- TeamWinRecovery Project

###### android fastboot mode
- fastboot is a tool/protocol that comes with android SDK (software developer kit) package
- used to re-flash partitions on android device
- an alternative to recovery mode for doing installations and updates
- fastboot mode can be used to unlock the bootloader for certain android device models
---

## Rooting Android Phone
---
- let users of android phones gain root user privilege on an android phone
- android is based on linux 
	- gaining root access is same as gaining root user access on linux os
- main reason for rooting is to gain access to those parts of the system that are normally not accessible
- most public root tools will result in a permanent root
	- changes persist even after rebooting the device.
- as for temporary root
	- the changes are lost once the device reboots
- temporary roots always preferred over permanent for forensic acquisition

**note:** it easily modifies data on the device
___


# Android Forensics Part 2
---
## Smartphone Market Share
---
- android is most widely used

![](https://i.imgur.com/UszDx2w.png)
___

## Android Operating System
---
- a non-proprietary, open standard mobile operating system based on a modified version of the linux kernel
- developed by the Open Handset Alliance (OHA)
	- in charge of the Android smartphone operating system
	- created by Google and includes key members such as China Mobile, HTC, Intel, Motorola, NTT DoCoMo, Sprint, and T-Mobile USA
	- a group of more than 50 mobile technology companies working together 
---

## Android Architecture
---
###### architecture
- linux kernel
- hardware abstraction layer (HAL)
- android runtime (ART) & native C/C++ libraries 
- java api framework
- system apps

![](https://i.imgur.com/7epuvjo.png)

###### linux kernel
- core functionalities of android are managed by the linux kernel
	- process management
	- memory management
	- security
	- networking

![](https://i.imgur.com/4GuqliN.png)

###### hardware abstraction layer (HAL)
- allows the higher level, Java API framework, to work with mobile device's hardware with help of standard interfaces
- can be done due to multiple library modules
	- which provide interfaces for different types of hardware components
	- e.g. bluetooth or camera

![](https://i.imgur.com/OvaiPao.png)

###### android runtime (ART)
- since Android 5.0, each application runs in its own process and with its own instance of the Android Runtime (ART)
- allows multiple virtual machines to run on low-memory devices by executing DEX (Dalvik Executable) files
- prior to version 5.0, Dalvik used to be Android Runtime, so applications developed for Dalvik should work when running with ART

###### native C/C++ libraries
- core android system components and services are built from native code
	- including HAL and ART 
- require native libraries written in C and C++

![](https://i.imgur.com/5s3KwAM.png)

###### java api framework
- allows developers to create applications using modular system components and services 
	- **view system** allows to build application's user interface
		- includes lists, grids, text boxes, buttons
	- **resource manager** provides access to non-code components of an application
		- localized strings, graphics and layout files
	- **notification manager** allows applications to display custom alerts
	- **activity manager** manages the lifecycle of applications, and arranges them in the back stack in the order in which each activity is opened
	- **content providers** allows applications to access other applications data, and share their own

![](https://i.imgur.com/D65rqnE.png)

###### application layer
- consists of apps
	- which are programs that users directly interact with
- system & user installed apps

![](https://i.imgur.com/C9z9iUM.png)

##### system apps
- pre-installed on the phone 
	- default browser
	- email client
	- contacts
- generally cannot be uninstalled or changed by the user
	- read-only on production devices 
	- some devices offer the ability to disable these applications
- if a system application is disabled
	- the app and all of its data remain on the device on the system partition 
	- the app icon is simply hidden from the user.
	- these apps can usually be found in the **/system** partition
	- beginning in Android 4.4, apps installed in **/system/priv-app/** are treated as privileged applications 
		- are granted permissions with protection-level (signatureOrSystem) to privileged apps

##### user installed apps
- are downloaded and installed by the user from various distribution platforms 
	- e.g. Google Play
- Google Play is the official app store for the Android operating system
	- where users can browse and download apps
- apps are present under the **/data** partition
___

## Android Security
---
- android runs on linux kernel
	- linux kernel provides android security features
- security features and offerings achieve 3 things:
	- protect user data
	- protect system resources
	- ensure that one application cannot access the data of another application
---
###### user-based permissions model
- android OS has implemented permission model for individual apps
- applications must declare a list of permissions they require in a file called manifest.xml
- when a user installs the application, Android presents permission list to the user so that they can view the list to allow or disallow the installation
- cannot install an android application with few permissions
	- either accept all the permissions or decline to install it
---
###### application sandboxing
- android makes use of linux user-based protection model
- every android app is assigned is a UID and is run as a different process
- an application cannot access data of other application
- if an app tries to do something malicious, can do so within its context and permission assigned by the OS
---
###### selinux in android
- From Android 4.3, SELinux(Security Enhanced Linux) is supported 
- SE android uses MAC (Mandatory Access Control) 
	- ensures app runs in an isolated environment
- with SELinuxAndroid, if a user installs the malicious app, malware cannot access the OS and corrupt the device
---
###### application signing
- android apps are signed by the developer/owner 
	- to determine the author of the app
- key store and private key which is used during signing need to be protected 
	- for pushing a new update to the application
---
###### secure interposes communication
- sandboxing is obtained between the processes using the UID assigned
- the Binder framework provides the capabilities required to organise all types of communication between various processes
- all communications between the processes using the Binder framework occur through the Linux kernel driver
	- /dev/binder
---


# Android Forensic Part 3
---
## File Systems
---
- no singularly defined file system for android
- common android file systems can be classified into 3 main categories
	- flash memory file systems
	- media-based file systems
	- pseudo file systems
---
###### flash memory file systems
- a type of non-volatile memory that erases data in units called blocks and rewrites data at the byte level
- examples:
	- Extended File Allocation Table (exFAT)
	- Flash Friendly File System (F2FS )
	- Journal Flash File System version 2 (JFFS2)
	- Yet Another Flash File System version 2 (YAFFS2)
	- Robust File System (RFS)
---
###### media-based file systems
- EXTendedfile system (EXT2/EXT3/EXT4)
- File Allocation Table (FAT, FAT12, FAT16 & FAT32)
- Virtual File Allocation Table (VFAT)
---
###### pseudo file systems
- virtual entries that the file system itself makes up on processes or functions
- example:
	- /proc on many operating sytems is a process information file system which dynamically generates directories for every process
- control group (cgroup)
- rootfs, procfs
- Ysfs
- tmpfs
---
##### partitions
- android uses more than one file system and multiple partitions
- partitions are represented by directories
- may be other partitions which differ in each model such as sdcard, sd-ext

![](https://i.imgur.com/BdVEuBz.png)
![](https://i.imgur.com/Jr3aiJp.png)
![](https://i.imgur.com/vPrb8IC.png)
___

## Android File Hierarchy
---
###### d
- a symbolic link to /sys/kernel/debug
- is used to mount the debugfs file system and to debug kernel

###### data
- partition that contains the data of each application
- most of the data belonging to a user is stored in this folder
	- contacts
	- SMS
	- dialed numbers
- has significant importance from a forensic point of view as it holds valuable data
---

## Ways to Store Data
---
- android devices store a lot of sensitive data through the use of apps
- various sources of data on android
	- apps that come along with Android
	- apps installed by the manufacturer
	- apps installed by a wireless carrier
	- apps installed by the user
- ways to store data locally in an android app
	- shared preferences
	- internal storage
	- external storage
	- SQLite database
	- network

###### shared preferences
- store data in key values pairs of data types in the .xml format
- save user preferences data of the current application 
	- user account name and passwords
	- settings
- typically stored in the application’s /data/data/<package_name>/shared_prefs
	
###### internal storage
- typically located in the application’s /data/data subdirectory
- data stored here is private and cannot be accessed by other applications 
	- unless they have root access
- internal data for each of the app is stored in respective folders
- usually, **shared_pref**, **lib**, **cache**, and **database** folders are created for most of the applications
	- shared_prefs - XML file of shared preferences contains data in a key-value pair
	- lib - custom library files required by app
	- files - developer-saved files
	- cache - files cached by app
	- databases - SQLite and journal files

###### external storage
- files can also be stored by the apps in external storage.
- can be removable media (SD card) or non-removable storage that comes with the phone
- SD cards are usually formatted with the FAT32 filesystem
	- can be stored as other filesystems
	- such as EXT3 and EXT4
- data stored in SD Card can be accessed by other applications
	- provided the requesting apps have the necessary permissions

###### SQLite database
- SQLite is a popular database format present in many mobile systems
- SQLite files used by the apps are generally stored at /data/data/\<ApplicationPackageName\>/databases

###### network
- network used to store and retrieve data on web-based services
- to do network operations, the classes in the java.net.* and android.net.* packages can be used
---
