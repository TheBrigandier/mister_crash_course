# Brig's Mister Crash Course
Got a lot of buds buying in to [Mister FPGA](https://www.retrorgb.com/mister.html) retro gaming system, particularly buying the kit found at [MisterAddons](https://misteraddons.com/products/mister-bundles). This doc aims to get you set up really fast; not by holding your hand, but by pointing you to some resources so you aren't searching for hours.

# Should I Buy a Mister?
Mister is an expensive piece of enthusiast hardware. Because I am handy with the tech, people reach out to me asking for justification or to argue why they think X is better or why they think Mister is a waste. For those people that might be absolutely true. Here's some reasons *I* bought a Mister and how the Mister provides value:

* I don't have many consoles,
    * The Mister has support for many, many consoles, arcade systems, and legacy computer platforms.
* I sure don't have many consoles with RGB mod or HDMI outs,
    * The Mister can output analog (CRT) and digital (HDMI) video formats.
* I don't have an OSSC, splitters, etc to get an RGB modded console into my CRT and capture card for streaming at the same time,
    * Mister can output to CRT and HDMI at the same time, with independent settings. I can send pure clean digital signal to my viewers, while I enjoy the game at much display latency on a CRT.
* I play games that can be very sensitive to input latency,
    * Mister can poll USB controllers at 1000hz vs 125hz on Windows. This lessens the chance of a polling mismatch randomly delaying my inputs by an additional frame.
    * Mister supports special adapters called "SNAC" that give you a true port for the console you're playing. I have one for NES, and SNES. They aren't subject to USB polling, they are polled identically to the real systems. I could plug in a Nintendo Zapper or Super Scope 6 and it would work fine.
* I value accuracy,
    * Mister is hardware replication via FPGA, similar to how SuperNT handles SNES. This isn't traditional emulation. This is extremely accurate hardware replication that matches up to the real hardware down to the clock cycles. Games work exactly the same as real hardware, including all slow downs and other bugginess you'd see on the real console.

If none of the above really matters that much to you, then save your cash and use Retroarch. For most people and games, it's likely just fine.

## What to Buy
On the [MisterAddons Shop Page](https://misteraddons.com/products/mister-bundles), they have fully built out Mister bundles, with the option between `Standard I/O` and `Digital I/O`. 99.9% of you are going to want `Standard I/O`, as it connects to both HDMI and CRT at the same time (great for streaming). The `Digital I/O` option is for people who may want to add additional unknown hardware to the system later on as it doesn't use as many expansion pins, leaving them available to you for whatever reason you may have.

tl;dr, If you aren't sure, buy the `Standard I/O` option.

Also, if you don't have ethernet near where you want to place the Mister, make sure to buy a [Wifi Adapter](https://misteraddons.com/products/wifi-adapter)! It's well worth the $9.

## First Time Setup
So you've got your Mister and you're ready to start. Let's get that bad boy prepped.

### SD Card Setup
Mister comes with an 8GB SD card; however, that can be pretty tight if you plan on loading it up with full romsets for various systems. If you'd like to use a larger SD card, check out [Mr. Fusion](https://github.com/MiSTer-devel/mr-fusion). Just follow steps 1 through 4, then come back here when your SD card is completed.

NOTE: The Mister has TWO SD card slots. One on top, one in the middle. The one on top is for old computers you're replicating to use as a hard drive, the one used by Mister is the one in the middle.

### Getting Mister Internet Access
Pretty straight forward here, plug in an ethernet cable. If you don't have ethernet, you will need the Wifi Adapter mentioned in the what to buy section above. You may need to reboot Mister after plugging these in.

For WiFi setup, when you turn on the Mister you'll find a menu with a `Scripts` option. You should see a Wifi Setup script you can run there to find your network and enter password (you will need to plug in a USB keyboard for this).

### Updating / System BIOS Files
Your Mister card image will come with an `update` script in the Scripts menu, but I would suggest using [update_all](https://github.com/theypsilon/Update_All_MiSTer) instead. This script will fetch all your updates, optional system cores, all BIOS files needed, and several arcade games.

Follow the guide above to put it on your SD card and run it on your Mister. After it completes your Mister should be ready to start uploading games.

### Roms and Romsets
Roms can be placed into your SD card's `/Games/<systemname>/` directories, based on the system the roms are for.

User "Ghostware" on Archive.org has curated many sets: https://archive.org/search.php?query=creator%3A%22Ghostware%22

#### NeoGeo
A very specific set is needed and can be found here: https://archive.org/download/multipacks/ as `Darksoft Neo Geo 2020-05-12.7z`. You'll also need to download the [romsets.xml](https://github.com/MiSTer-devel/NeoGeo_MiSTer/blob/master/releases/romsets.xml) file and place it into `/Games/NeoGeo` as well.

### Remote Access
If your Mister can be permanently on your network, I would HIGHLY recommend enabling SSH for management and file transfers. This can be done by going to the Scripts menu and running the `ssh_on` script.

Once complete, you can connect using an SSH client (like PuTTY); or, you can use an SCP client like [WinSCP](https://winscp.net/eng/download.php) to connect and do file transfers.

When connecting in this way, your usual SD card content will be in `/media/fat/` directory.

### Fin
You should be set to play some games over HDMI. I will add more info here later regarding CRT, latency settings, etc.
