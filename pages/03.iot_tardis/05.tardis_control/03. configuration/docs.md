---
title: Configuration
taxonomy:
    category: docs
---
### [Configuration] Tardis Node-Red System Control 
---
### Function
##### Configure or Update a __k9node__
- Select Active __k9node__
- Set a "Friendly Name" for __k9node__ for easy recognition
- Configure pins for input/output/pullups
- Configure pins for PWM [ on/off, duty cycle, frequency]
- save Selections to a Flow Context 
- configuration is sent on Button press using selections from Flow Context
- File operations to/from __k9node__
	- read/write files
	- manipulate Objects in __k9node__
		- Objects: Node, Pins, Access Point, MQTT, Timers
		- write Object to __k9node__
		- command __k9node__ to save active Object internally to become active on reboot
		- delete Objects
		- list files on __k9node__
		- write a payload to __k9node__
- Display screen for File Payloads

---
### Flow
![](/user/images/tardis/2018-08-09_15-54-40-configuration.png)

---
### Browser UI
![](/user/images/tardis/chrome_2018-08-15_11-49-48-configure-ui.png)