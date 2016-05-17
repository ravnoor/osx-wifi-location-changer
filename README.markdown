#Mac OSX Wi-Fi Location Changer

* Automatically changes the Mac OSX network location when Wi-Fi connection SSID changes
* Allows having different IP settings depending on the Wi-Fi SSID

Based on http://tech.inhelsinki.nl/locationchanger/ <br>
Forked from https://github.com/rimar/wifi-location-changer/

Mountain Lion compatible

##Configuration

Edit locationchanger and change/add locations to be set:

	# LOCATIONS
	Location_McGill="wpa.mcgill.ca"
	Location_EduRoam="wpa.mcgill.ca"
	Location_Home="openwrt/5"

*That's the exact names as they appear under "Location" in OSX's System Preferences -> Network*

Edit locationchanger and add/edit SSIDS to be detected:

	# SSIDS
	SSID_McGill=wpa.mcgill.ca
	SSID_Home=openwrt/5
	SSID_EduRoam=eduroam

Edit/Add SSID -> LOCATION mapping to list:

	# SSID -> LOCATION mapping
	case $SSID in
		$SSID_McGill ) LOCATION="$Location_McGill";;
		$SSID_Home          ) LOCATION="$Location_Home";;
		$SSID_EduRoam  ) LOCATION="$Location_EduRoam";;
		# ... add more here

##Installation

Execute:

	./install

... or do it manually:

Copy these files:

	cp locationchanger /usr/local/bin
	cp LocationChanger.plist ~/Library/LaunchAgents/

Should you place the locationchanger script to another location, make sure you edit the path in LocationChanger.plist too.

Make locationchanger script executable:

	chmod +x /usr/local/bin/locationchanger

Load LocationChanger.plist as a launchd daemon:

	launchctl load ~/Library/LaunchAgents/LocationChanger.plist

##Logfile

Logfile location can be adjusted in locationchanger:

	exec &>/usr/local/var/log/locationchanger.log

See log in action:

	tail -f /usr/local/var/log/locationchanger.log
