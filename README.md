# @mathias 's public project archive

I wanted to have permalinks to point to, and be able to log various Issues towards, any projects I am working on in my free time. These could be software or hardware -- really anything I am tinkering with.

Keeping all the links and specs in one place should also help me in the future to remember what I've got and how I planned to use it.

## Solar garage

Hardware:
* 2 [Renogy 100 watt solar panels](https://www.renogy.com/100-watt-12-volt-monocrystalline-solar-panel-compact-design/)
* 1 [Renogy 40A MPPT charge controller](https://www.renogy.com/rover-li-40-amp-mppt-solar-charge-controller/)
* 1 [Renogy cable kit, 20ft](https://www.amazon.com/Renogy-Accessory-Systems-Kit-Connector/dp/B091KTG9WX/) (includes Z-brackets)
* 1 [Renogy Deep Cycle AGM Battery 12 Volt 200Ah](https://www.renogy.com/deep-cycle-agm-battery-12-volt-200ah/)
* 1 [Renogy 2000W 12V Pure Sine Wave Inverter](https://www.renogy.com/2000w-12v-pure-sine-wave-inverter/)

Planning to grow to double the panels and another battery, eventually.

### Project log
* 2023-03-14 heavy (130lb!) battery was delivered.

**Current status**: Waiting on me.

## Solar webserver project
* 1 spare UPS battery (unbranded), 9Ah.
* 1 [MPPT Solar Charger for intelligent devices](https://www.tindie.com/products/globoy/mppt-solar-charger-for-intelligent-devices/) 
* 1 [Renogy 50 watt solar panel](https://www.renogy.com/50-watt-12-volt-monocrystalline-solar-panel/)
* 1 GL.iNet GL-AR300M16-Ext travel router

### Misc parts
* Terminal blocks: Glarks 70Pcs set
* Outdor junction box with hinged cover (waterproof/dustproof) -- to fit the UPS battery.

Inspired by getting the spare UPS battery which didn't fit my UPS. I could not return it, so why not move my "personal cloud" Raspberry Pi to solar power and a battery? I don't use the RPi much at night anyways.


### Project log
* 2023-09-12 - Renogy solar panel is here
* 2023-10-01 - First time charging the battery, now that I had terminal blocks and crimping tools to step down the 12AWG solar cables to smaller wires that can be inserted into the MPPT charger.
* 2023-10-02 - travel router is here, can begin flashing it with OpenWRT and documenting the setup steps for that.

### References
- [Low Tech Magazine's solar-powered ARM webserver](https://homebrewserver.club/low-tech-website-howto.html)

## Low-power ARM NAS (Network Attached Storage)

I am using a [RockPro64 board](https://www.pine64.org/rockpro64/), a SATA riser, and a [hot swap SATA cage](https://www.rosewill.com/rosewill-rsv-sata-cage-34-hard-disk-drive-cage/p/9SIA072GJ92556) to build a small, low-power NAS box.



## License

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.
