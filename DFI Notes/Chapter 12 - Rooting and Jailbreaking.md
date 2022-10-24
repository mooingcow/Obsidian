
# 12 Rooting and Jailbreaking
---

## Rooting & Jailbreaking
---
- popular mobile devices come with restrictions
	- limit application installation
	- limited access privileges to device
	- code signing 
	- one of the most important security mechanisms in iOS
	- all binaries and libraries must be signed by a trusted authority code signing app 
	- assures users that it is from a known source and the app hasn't been modified since it was last signed
---
###### rooting in android
- to unlock the operating system so you can 
	- install unapproved apps
	- deleted unwanted bloatware
	- update the OS
	- replace the firmware
	- customize anything 
- allow user to gain “root” user privileges
	- no restriction on system settings after rooted
- android allows **sideloading** without rooting by default. 
	- **sideloading**: installing app from non-android market
		- i.e. download apk files from website
---
###### jailbreaking in iOS
- requires modification of OS settings
- a form of privilege escalation via hardware / software exploits
- enable installation of 3rd party apps
- phone will work with App Store / can still make call after jailbroken
---

## Motivation for End Users
---
- more application sources
- access unauthorised applications
	- pirated software & Firefox in iPhone
- remove vendor-installed bloatware
	- improve performance
	- increase available memory (RAM/ROM)
- access restricted hardware resources
	- i.e. bluetooth on Kindle Fire (tablet from Amazon)
	- perform system tweaking
---

## Warnings
---
- to escape control, need to run 3rd party tools
	- are these tools secure?
- voiding of warranty
- error and performance issues (not tested)
	- could cause phones become unstable
- dont root or jailbreak your everyday devices
	- needed for day to day operations
- check organisation’s security policy on permitted activities with corporate devices
	- e.g. EULA (end-user license agreement) violation
---

## Tools
---
###### iOS
- JailbreakMe
- Redsn0w
- Evasi0n
---
###### android
- ADB (old school)
	- Need drivers, scripts, SU apk
- z4root (from Android 2.3)
- SuperOneClick (need adb)
- flashing recovery & custom ROM
- motochopper (Android 4.32)

##### steps
- vary significantly due to differences in hardware
- generally involve:
	- flash recovery
		- enter recovery to backup device and load new OS
	- flash boot (fastboot)
		- used to flash images such as recoveries, bootloaders, and kernels to Android device
	- local privilege escalation (su)
	- ADB privilege escalation
		- android debug bridge (ADB) lets you communicate to Android device from PC using command line.
- will also need:
	- allow unsigned software 
		- i.e. sideloading
	- enable USB debugging
		- developer mode in Android that allows newly programmed apps to be copied via USB to the device for testing
- once rooted, ADB can yield a rootshell when local privilege escalation request (su) is requested
---
