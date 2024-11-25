# Neighborhood Server

See https://github.com/mathias/projects/issues/3 and previous work described in the [README section on the Solar Webserver project](https://github.com/mathias/projects#solar-webserver-project).

Here's a restatement of what the goals are:

I intend to build a "solar ebook library" and neighborhood server for my yard. The hardware will be:

* 1 spare UPS battery (unbranded), 12VDC 9Ah.
* 1 [MPPT Solar Charger for intelligent devices](https://www.tindie.com/products/globoy/mppt-solar-charger-for-intelligent-devices/) 
* 1 [Renogy 50 watt solar panel](https://www.renogy.com/50-watt-12-volt-monocrystalline-solar-panel/)
* 1 [GL.iNet GL-AR300M16-Ext travel router](https://www.gl-inet.com/products/gl-ar300m/)
* 1 [Raspberry Pi Zero 2W](https://www.raspberrypi.com/products/raspberry-pi-zero-2-w/) -- originally I was going to use a Raspberry Pi 3 connected via ethernet, but I had concerns about power usage and still wanted multicore to run web applications rather than just serve static files
  * A "high endurance" micro SD card with sufficient storage. I wanted to avoid having the SD card "wear out"
* Terminal blocks: Glarks 70Pcs set
* Outdoor junction box with hinged cover (waterproof/dustproof) -- to fit the UPS battery

Some other future plans for the software that will be served by the webserver, besides an ebook library:

* A static site landing page that explains the server, links to various places on the server, and explains the no-log-retention policies of this particular server.
* A wiki engine for community bulletin-board and information sharing
* Possibly a neighborhood calendar. Prior art: https://gancia.org/
* A tool lending library app (may just be a page on the wiki?)
* Real time chat like Rocket chat?

## Raspberry Pi setup

Download Raspbian 64-bit Lite and flash it using something like Popsicle USB Flasher or the Raspberry Pi Imager onto the microSD card. Connect the Raspberry Pi Zero 2W to a monitor and keyboard for initial setup. (Micro HDMI cable to monitor's HDMI.) Connect the Raspberry Pi Zero 2W to USB power to boot it.

The Raspberry Pi will generate SSH keys, resize the disk to fill the space, and then reboot.

The Pi will prompt you to create a user and set its password. Log in as that user.

Use `nmcli` to set up the wifi connection to a real wifi network that is connected to the internet, for the time being.

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
```

It should pick up at least Linux kernel 6.1.x or later, and whatever Pi firmware goes with that kernel.

In raspi-config:
* Advanced - Resize filesystem (just in case it hasn't done it)
* Update
* Interface Options - SSH - Enable

"Finish" and it should drop back at the CLI.

One more thing -- we want to turn on I2C so that we can communicate with the MakerPower board. Edit `/boot/config.txt` and uncomment this line:

```
#dtparam=i2c_arm=on
```

Run `sudo reboot` to pick up any new kernels that were installed in the `apt-get upgrade` earlier.

When it reboots, log in again.

```
ssh-keygen
sudo apt-get install curl
curl https://github.com/mathias.keys > .ssh/authorized_keys
```

At this point I should be able to `ssh mathias@<IP>` from my laptop and connect to the Pi remotely over SSH.

Tools needed for setting up the basic webserver: `sudo apt-get install vim git`

During development I also installed the following for more tooling: `sudo apt install htop tmux` and ran the setup script from https://rustup.rs

#### Server setup

```
sudo apt remove apache2
sudo apt autoremove
```

Install Caddy per instructions: https://caddyserver.com/docs/install#debian-ubuntu-raspbian

Then edit `sudo vim /etc/caddy/Caddyfile` enable:
```
  reverse_proxy localhost:3000
```

```
sudo systemctl reload caddy
```

TODO: This may not be the server we end up using! Nginx needs config, though.

### Verify GPIO with Rust

Cross-compile https://github.com/mathias/pi-makerpower-gpio and copy the executable to the Raspberry Pi. Verify the I2C connections and alert pin are connected to the MakerPower board, then run it. (Compiling on the pi device takes too long.)

TODO: finish the converters for `pi-makerpower-gpio` so that we get actual values for voltages, etc.

## Wireless router setup

TODO

## Physical assembly

3D print a case for easier mounting of the Raspberry Pi Zero 2W: https://www.printables.com/model/34849-raspberry-pi-zero-slim-case-with-mounting-tabs

Solder the 40-pin GPIO header to the Raspberry Pi Zero 2W -- we'll use it to communicate with the solar charger PCB later.

Connect the MakerPower to GPIO based on this guide: https://github.com/danjulio/MPPT-Solar-Charger/blob/master/hardware/connection_diagrams.pdf

##  Server setup

TODO

## Errata

### Power usage research

Used a little USB power monitor to see how many watts each dev board used at idle and (if possible) running stress-ng from s-tui. (`s-tui` installed with `sudo apt install s-tui` and run with sudo to stress test.)

| SBC                           | Idle watts (with wifi on) | Idle watts (with ethernet)              | s-tui stress test watts     |
| ---                           | ---                       | ---                                     | ---                         |
| Pi Zero 2W                    | 1.5 watts                 | N/A                                     | 3.3 watts                   |
| RPi 3                         | N/A                       | 2.2 watts                               |                             |
| Mango Pi MQ Pro (RISC-V)      |                           |                                         |                             |
| Milk V Duo                    | N/A no wifi               | 1.2 watts (seems suspiciously high now) | N/A can't install currently |
| Milk V Duo (w/ carrier board) | N/A no wifi               | 0.3-0.4 watts                           | N/A can't install currently |


Wireless access point power draw:
* GL.iNet GL-AR300M16-Ext travel router: 1.6-2.2 watts.
  * This will likely be responsible for higher draw than the Raspberry Pi and limit our battery life.

### Self-documenting hardware + software
This project should implement the ["RNote self-documenting" idea](https://github.com/mathias/projects/issues/3#issuecomment-1802555070) where the webserver contains a download link for an archive of all 3D design files, all firmware, and a doc on how to compile the firmware and how to build the hardware. (A copy of this guide and other guides written.)

## License

This work is licensed under [CC BY-NC-SA 4.0](http://creativecommons.org/licenses/by-nc-sa/4.0/).
