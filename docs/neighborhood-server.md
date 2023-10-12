# Neighborhood Server

See https://github.com/mathias/projects/issues/3 and previous work described in the [README section on the Solar Webserver project](https://github.com/mathias/projects#solar-webserver-project).

Since the READMe might change or the Issue may get closed, here's a restatement of what the goals are:

I intend to build a "solar ebook library" and neighborhood server for my yard. The hardware will be:

* 1 spare UPS battery (unbranded), 9Ah.
* 1 [MPPT Solar Charger for intelligent devices](https://www.tindie.com/products/globoy/mppt-solar-charger-for-intelligent-devices/) 
* 1 [Renogy 50 watt solar panel](https://www.renogy.com/50-watt-12-volt-monocrystalline-solar-panel/)
* 1 GL.iNet GL-AR300M16-Ext travel router
* 1 Raspberry Pi Zero 2W -- originally I was going to use a Raspberry Pi 3 connected via ethernet, but I had concerns about power usage and still wanted multicore to run web applications rather than just serve static files
  * A "high endurance" micro SD card with sufficient storage. I wanted to avoid having the SD card "wear out"
* Terminal blocks: Glarks 70Pcs set
* Outdoor junction box with hinged cover (waterproof/dustproof) -- to fit the UPS battery

## Raspberry Pi setup

Download Raspbian 64-bit Lite and flash it using something like Popsicle USB Flasher or the Raspberry Pi Imager onto the microSD card. Connect the Raspberry Pi Zero 2W to a monitor and keyboard for initial setup. (Micro HDMI cable to monitor's HDMI.) Connect the Raspberry Pi Zero 2W to USB power to boot it.

The Raspberry Pi will generate SSH keys, resize the disk to fill the space, and then reboot.





## Wireless router setup

## Physical assembly

3D print a case for easier mounting of the Raspberry Pi Zero 2W: https://www.printables.com/model/34849-raspberry-pi-zero-slim-case-with-mounting-tabs

Solder the 40-pin GPIO header to the Raspberry Pi Zero 2W -- we'll use it to communicate with the solar charger PCB later.



## License

This work is licensed under [CC BY-NC-SA 4.0](http://creativecommons.org/licenses/by-nc-sa/4.0/).
