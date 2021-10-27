---
title: Main
taxonomy:
    category: docs
---
### [Main Module] Tardis Node-Red System Control
---
### Function
##### displays active NodeID 
- each __k9node__ has 2 names or NodeIDs
	- "Generated Name" based on module type and MAC address to create a unique name
		- eg. D1m_078598 {WeMos D1 mini module [D1m_] + last 6 bytes of MAC address [078598] }
		- internally this is used to uniquely reference the Object
	- "Friendly Name" configured to provide a more readable name
		- this is used in Most Menus
		- this is a property of the Node Object

##### UI displays data from a single Active __k9node__
- pulldown menu from ActiveNode display indicates all active __k9nodes__
- Controls Multiple Remote __k9node__ 
- Control Remote __k9node__  Actuators [motors, LEDs, relays]
- Monitor Remote __k9node__  Sensors [lights, switches, temperature, humidity]
- Review __k9node__  State properties
- Review __k9node__  Pin States
- Configure pins for PWM control
- displays temperature and analog input voltage
- set calibration factor for temperature

##### sends, receives & processes __MQTT__ messages
- Processes __MQTT__ topic data received from __k9node__ 

##### send commands to __k9node__ 
- change OLED display [status, pin states, message, cycle through all]
- enable debug mode
- send node or pin status
- get analog voltage
- RESET/reboot __k9node__

---

### Node-Red Flow
![TARDIS Node-RED flow graphic](/user/images/tardis/2018-08-09_16-01-02-main.png)

---

### Browser UI
![](/user/images/tardis/chrome_2018-08-15_11-47-26-main-ui.png)