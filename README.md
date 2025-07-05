# SeLNA
An affordable and easy-to-make filtered LNA.

## Getting a board to modify
It's much easier to modify and repurpose a factory LNA pcb than to fully make your own.
We are going to focus on modifying a double-filtered chinese ADS-B LNA, as they are reasonably priced and simple enough to modify. As a bonus you can get a version with a robust, aluminium enclosure, that contains the same PCB.
Search "ADS-B LNA" on AliExpress and you are likely to find it in the top results.

![](pictures/ADS-B_LNA.jpg)

## Other components
You'll also need SAW filters of your choice (I'm using a TA0700A for S-Band); if you want to also power the LNA with bias tee, you will also want a 1210 SMT inductor (180-220nH works fine for L and S-band) and a poly fuse (200mA) - Soldering supplies like decent flux and solder of your choice are necessary. I recommend using some UV soldermask for the bias-t modification and conformal coating the board after the changes have been made.

## Disassembly & prep
If you have one with an enclosure, remove all the screws you can see (4x countersunk M2.5 to remove the lid, 4x M2.5 for the SMAs, and 4x M2 to remove the board).

![](pictures/inside.jpg)

The next part will be tricky, you need to both melt the solder and unscrew the VCC pass-trough at once. After that you can remove the SMAs by melting the solder and carefully pulling them out. The PCB should now be free; you can clean it up with some isopropyl alcohol and move on to the next step.

## Replacing the filters
With the board removed and cleaned, you can now preheat it to 80-90°C. Once it's warm, you can add flux near the SAWs and start heating up the area around them with hot air - I set mine to 320°C. Once the solder is liquid, remove the old filters carefully, and use a strip of solder wick and a soldering iron to remove the old lead-free solder from the pads. Clean up any residue left behind with isopropyl and q-tips to prepare for the new filters. You'll notice, that the new SAWs have different (in this case, smaller) footprint than old ones. As long as you center them on the pads so that the proper contacts are made, it will still work fine. I usually solder them by hand - starting with wetting the larger ground pad with some solder, placing the filter on it while the solder is liquid and then individually solder the rest of the pads.

![](pictures/filter_swap.jpg)

## Adding a bias tee (optional)
You can skip this part if you wish to power the LNA with an external power supply.
There's no good way of performing this modification - it'll be sketchy no matter how you do it. Start with wicking the solder off the SMA ground pad on the output side, then clean up the surrounding area with isopropyl alcohol. I recommend covering the pad with UV soldermask, but kapton tape will work too. Solder the bias inductor to the pad, making sure to leave yourself space for the SMA pin. Then add a poly fuse to the VCC pad, and connect it to your bias inductor.

![](pictures/fused_bias_tee.jpg)

## Finishing touches
If you chose not to add a bias tee, make sure to screw the VCC pass-trough back in and solder it in place. Put some conformal coating on the backside of PCB, and leave the front of the PCB bare for now. Place the board back into the enclosure, then mount and solder the SMAs back on.

## Verifying your work
Start with basic continuity tests, and make sure that there are no obvious shorts on the RF or VCC paths. After this is confirmed, you can supply power to your LNA for the first time. Close the lid and make sure that the PCB screws are in, then sweep it with a VNA to see how it performs.
I'm using the LiteVNA64 with a DC block on port 1, and a 30dB attenuator & bias tee on port 2.

![](pictures/test_setup.jpg)

This isn't a VNA guide, but make sure to do your calibrations with the VNA disconnected, but with any blocks, filters, injectors, or other components still attached. 

Here are some results from a variety of LNAs I made using these steps-

S-band with TA0700a filters:

![](pictures/2250-S11.bmp)
![](pictures/2250-S21.bmp)

L-band with TA2727AA3112 filters:

![](pictures/S11-1702-5.bmp)
![](pictures/1702_5-S21.bmp)

L-band with TA1583A filters - version without the enclosure:

![](pictures/TA1583A-S11.bmp)
![](pictures/TA1583A-S21-MARK.bmp)

After verifying your LNA performance, you can put a layer of conformal coating on the front of PCB. I also recommend plugging the empty threaded hole for the VCC pass-trough with a M2.5 screw.
