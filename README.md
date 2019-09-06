Composite Driver for iSmartGate management in Hubitat
=======

This is a dirty hack of the composite drivers for GoGoGate drivers by mgroeninger to give iSmartGate management in Hubitat.  Features are:
* Parent driver installs for iSmartGate device endpoint itself  This allows:
    * Multiple door devices to detected/installed for a single iSmartGate (up to the supported three)
    * The lights to be controlled
    * Minimizes http requests to the device for polling
* Child devices present doors as both door controls and switch controls, making Alexa integration simplier
* Child devices DO NOT report temperature and battery readings for each sensor as I have removed this as I use hardwired sensors without temp/batt support which was causing issues creating the child devices.

NOTE: I have also hardcoded this to use only door 1 & 2 of the iSmartGate - search for the line "    for (i in 1..2) {" (line 192 in my file) and change the "2" to be the total number of doors (up to 3 maximum) you have configured.

Installation info is similar to below but use iSmartGate versions of the files

Installation
1. Add the child device driver to Drivers Code on your Hubitat hub from https://raw.githubusercontent.com/mgroeninger/Hubitat-gogogate2/master/GoGoGate_child_driver.groovy
2. Add the parent device driver to Drivers Code on your Hubitat hub from https://raw.githubusercontent.com/mgroeninger/Hubitat-gogogate2/master/GoGoGate_parent_driver.groovy
3. Create a Virtual Device (under devices) of type "GoGoGate 2 Parent"
4. Fill in the ip address of your GoGoGate2 device, as well as the username and password you use to access it and save the preferences
5. Optionally, change the child device labels to name you would like to use 

Credits/Development Progression:
* Started with basic composite plugin framework from https://github.com/dpark/Hubitat-Composite-Driver
* Relied heavily on https://github.com/bmergner/bcsmart/tree/Sensor-Update for polling logic, URIs and the parse function
* Used log output control from https://github.com/stephack/Hubitat/blob/master/drivers/Lifx%20Group%20of%20Groups/Lifx%20GoG.groovy
