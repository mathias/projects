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

The Pi will prompt you to create a user and set its password. Log in as that user.

Use `nmcli` to set up the wifi connection to the real house wifi for the time being.

```
nmcli dev status
nmcli radio wifi on
nmcli dev wifi list # find your network name
sudo nmcli dev wifi connect $YOUR_WIFI password "$PASSWORD"
```

Verify it is working with `ping google.com`

Update the Pi and set some initial config:

```
sudo apt-get update && sudo apt-get upgrade -y
sudo raspi-config
``

In raspi-config:
* Advanced - Resize filesystem (just in case it hsan't done it)
* Update
* Interface Options - SSH - Enable

"Finish" and it should drop back at the CLI. Run `sudo reboot` to pick up any new kernels that were installed in the `apt-get upgrade` earlier.

When it reboots, log in again.

```
ssh-keygen
sudo apt-get install curl
curl https://github.com/mathias.keys > .ssh/authorized_keys
```

At this point I should be able to `ssh mathias@<IP>` from my laptop and connect to the Pi remotely over SSH.

Preserve my sanity: `sudo apt-get install vim git`

## Wireless router setup

TODO

## Physical assembly

3D print a case for easier mounting of the Raspberry Pi Zero 2W: https://www.printables.com/model/34849-raspberry-pi-zero-slim-case-with-mounting-tabs

Solder the 40-pin GPIO header to the Raspberry Pi Zero 2W -- we'll use it to communicate with the solar charger PCB later.

## Errata

### Power usage research

Used a little USB power monitor to see how many watts each dev board used at idle and (if possible) running stress-ng from s-tui. (`s-tui` installed with `sudo apt install s-tui` and run with sudo to stress test.)

| SBC                      | Idle watts (with wifi on) | Idle watts (with ethernet)                          | s-tui stress test watts     |
| ---                      | ---                       | ---                                                 | ---                         |
| Pi Zero 2W               | 1.5 watts                 | N/A                                                 | 3.3 watts                   |
| RPi 3                    | N/A                       | 2.2 watts                                           |                             |
| Mango Pi MQ Pro (RISC-V) |                           |                                                     |                             |
| Milk V Duo               | N/A no wifi               | 1.2 watts (don't have ethernet expansion board yet) | N/A can't install currently |


## License

This work is licensed under [CC BY-NC-SA 4.0](http://creativecommons.org/licenses/by-nc-sa/4.0/).
