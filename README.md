# Brig's Mister Crash Course
Got a lot of buds buying in to [Mister FPGA](https://www.retrorgb.com/mister.html) retro gaming system, particularly buying the kit found at [MisterAddons](https://misteraddons.com/products/mister-bundles). This doc aims to get you set up really fast; not by holding your hand, but by pointing you to some resources so you aren't searching for hours.

# Should I Buy a Mister?
Mister is an expensive piece of enthusiast hardware and isn't for everyone. Here's some reasons *I* bought a Mister and how the Mister provides value to me:

* I don't have many original consoles,
    * The Mister has support for many, many consoles, arcade systems, and legacy computer platforms.
* I don't have the time, money, or expertise to get all the consoles I want modded to support both RGB and HDMI out,
    * The Mister can output analog (RGBs, etc) and digital (HDMI) video formats for all the cores it supports.
* I don't have an OSSC, splitters, or other hardware required to play my systems using a CRT and capture them for streaming on Twitch,
    * Mister can output to CRT and HDMI at the same time, with independent settings. I can send pure clean digital signal to my viewers via a common capture card (Elgato in my case), while I enjoy the game at much better display latency / authenticity on a CRT.
* I play games that can be very sensitive to input latency,
    * Mister can poll USB controllers at 1000hz vs 125hz on Windows. This lessens the chance of a polling mismatch randomly delaying my inputs by an additional frame.
    * Mister supports special adapters called "SNAC" that give you a accurately behaving port for the console you're playing. I have one for NES, and SNES. They aren't subject to USB polling, they are polled identically to the real systems. I could plug in a Nintendo Zapper or Super Scope 6 and it would work fine.
    * Analog output to CRT has much less latency compared to an LCD screen. Here's a comparison showing my CRT two frames ahead of my 144hz low latency gaming LCD:
    ![Latency Comparison](/pics/latency.png)
* I value accuracy,
    * Mister is hardware replication via FPGA, similar to how SuperNT handles SNES. This isn't traditional emulation. This is extremely accurate hardware replication that matches up to the real hardware down to the clock cycles. Games work nearly exactly the same as real hardware, including all slow downs and other bugginess you'd see on the real console.
* I value my money,
    * I primarily wanted an option for SNES games. SuperNT was out of stock, and combined with a flash cart just as expensive. It also didn't support all the other systems or simultaneous CRT out. Mister was a no brainer in comparison.

If none of the above really matters that much to you, then save your cash and use Retroarch (see [Runahead Latency Reduction](https://www.libretro.com/index.php/retroarch-1-7-2%E2%80%8A-%E2%80%8Aachieving-better-latency-than-original-hardware-through-new-runahead-method/#:~:text=Once%20the%20game%20is%20running,you%20want%20to%20run%20ahead.)). For most people and games, it's likely just fine.

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

### Streaming Settings
A lot of you are probably reading this guide because I sent it to you on Twitch, meaning a lot of you are streamers. Just wanted to include some common settings I set that help with quality:

#### System Video Settings
* In **Scripts > ini_settings**, set `video_mode` to match your display resolution (assuming you're using a TV or monitor).
* In **Scripts > ini_settings**, set `vscale_mode` to `Use integer scale only`. This will give you some bars, but will precisely size your content to fit your display/capture pixels vertically. This does not handle horizontally, more on that in the Game Core Settings below!
* In **Scripts > ini_settings**, you have a few options for `vsync_adjust`:
  * If you are playing an LCD:
    * Set it to `Low lag`. This will be the best feeling to play, but may cause capture card glitches when swapping between cores. If this happens you can usually fix it by a quick deactivate/activate of your capture card in OBS. If not, try the next option.
    * Set it to `Match core frequency`. Your capture card may like this better, but you'll have more input latency. If this doesn't work, then use `Match display frequency` and have even more input latency, but it should at least be playable.
  * If you are playing on CRT and capturing the HDMI out for stream:
    * Same priority as above, just set it to whatever looks best and makes your capture card happy. The CRT output will be unaffected by this setting generally.
* In **Scripts > ini_settings**, set `hdmi_limit` to match your stream color space / capture card settings color space. In general you'll be using Rec 709, so this should be set to `On` to match.

#### Game Core Settings
After changing these settings, be sure to open the menu, press RIGHT to go to the second menu page, and select `Save Settings` so they will persist! Some of these settings may require you to load a ROM to adjust them!

* Almost all cores need to have `Autosave` ticked to `On`. This is set to `Off` by default for some users that have Misters in arcade cabinets that are on 24/7 doing sdcard writes, it can wear the card out. If you don't have this on, you run the risk of losing save data if you forget to save backup ram!
* Set `Scale filter` (usually on the second menu page, press right to see it) to `Custom`, then select a filter below that setting to apply to your HDMI output. Normally this is done to apply scanline filters, but for streaming you want to apply `Interpolation Sharp` on nearly all cores.
  * For SNES, there's a special `SNES Interpolation (Sharp)` filter, use it instead for SNES core because it handles a SNES edge case,
  * **Why should I use this, I can't see it doing anything?**
    * The effect is subtle. Playing the games at proper aspect ratios does not output square pixels, the HDMI output makes them fit to the nearest pixels. If you have the `vscale_mode` set to `Use integer scaling only` in INI settings above, this fixes it vertically but doesn't do anything for horizontally. If you really get up close and personal to the display, you'll notice some pixels appear wider than others. This may not seem like much of a problem, but on games that use small repeating patterns (think bricks in Mario, or the dungeons in Zelda 2), scrolling the screen sideways causes a horrible looking "shimmer" or moire effect. Turning on interpolation causes the pixel edges to be interpolated (i.e., faded softly into the pixel next to it) when a pixel edge doesn't align properly to the display resolution. The result? All pixels look to be the same size, shimmer/moire disappears. The sacrifice? A slight sharpness decrease in some horizontal edges. It's worth it, trust me.

### Fin
You should be set to play some games over HDMI. I will add more info here later regarding CRT, latency settings, etc.
