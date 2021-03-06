# mpradio
Morrolinux's Pirate radio (PiFmRDS implementation with Bluetooth and mp3 support) for all Raspberry Pi models

Exclusively tested on Minimal Raspbian (ARM)

# Known issues
- The first bluetooth connection after boot is known to fail after few seconds. All subsequent connections will work just fine.
- Due to a design flaw in BCM43438 WIFI/BT chipset, you might need to disable WiFi if you experience BT audio stuttering on Pi Zero W and Pi 3: https://github.com/raspberrypi/linux/issues/1402

# installation
` git clone https://github.com/morrolinux/mpradio.git mpradio-master `

` cd mpradio-master/install `

` sudo ./install.sh `

# configuration
By default, mpradio will always be running automatically after boot once installed. No additional configuration is needed.
However, you can change the FM streaming frequency (which is otherwise defaulted to 88.8) by placing a file named pirateradio.config in the root of a USB key (which of course, will need to stay plugged for the settings to be permanent)

pirateradio.config example:
```
[PIRATERADIO]
frequency=105.3
```

# update 
` rm -rf mpradio-master/ ` 
and then:

installation steps

# uninstallation / removal
` ./install.sh remove `

# Debugging / Troubleshooting
mpradio is launched as a service (via systemd) after boot completed

check whether the service is running or not: 

` $ sudo systemctl status mpradio `

start or stop the service:

` $ sudo systemctl [start/stop] mpradio `

As for Bluetooth:

Bluetooth connection logs are under ` /var/log/bluetooth_dev `

if you are having issues with bluetooth audio pairing, please also check if simple-agent service is running:

` $ sudo systemctl status simple-agent `

if you are having issues with bluetooth not connecting once it's paired, please check weather bluealsa is running or not:

` $ sudo systemctl status bluealsa `


A simple schematic of how things work together:

![Alt text](/doc/mpradio_schematic.png?raw=true "mpradio schematic")
