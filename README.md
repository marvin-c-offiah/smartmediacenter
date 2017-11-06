# SmartMediaCenter

A mobile client-server architecture for controlling your home cinema

## Hardware setup
You have an environment with the following hardware equipment:
* Ideally, a low-energy single-board computer like a [Raspberry Pi](https://www.raspberrypi.org/). Or otherwise: Just a computer that can act as a server. Let's call it the **Service Host**. It is permanently on-line and accessible from the internet through proper NAT-settings on your home network's router. Make sure your router itself is accessible through a static IP address. Alternatively, you can set it up to use a Dynamic DNS server. Find some free ones [here](https://www.noip.com/free), [here](https://www.dnsdynamic.org/) or [here](http://www.dyndnss.net/updater.php). The Service Host needs to be able to wake up the following host:
* Any personal Desktop computer, called the **Player Host** that can be woken up in some form by the Service Host. Typically, that's via Wake-on-LAN or some similar technology. So to make things easy, the Player Host must be connected with the Sevice Host via an *Ethernet LAN wire*. The Player Host must also have internet access and be able to play back audio and video multimedia content on its hardware. For reasons still to uncover, it should also have a *Bluetooth Low Energy (BLE) device* (USB-dongle or internal) permanently activated. It is extended by the following output periphery *permanently connected* to it:
* Speakers
* Headphones (optional)
* A projector (very important!). What would a proper home cinema be without a projector? Right. Just any projector that serves your standards will do. As long as it can be connected to the Player Host's graphics card to display its output, whether via VGA, DMI, HDMI, DP or whatever. But *most importantly*: It must be possible for the projector to be switched on and off by the Player Host! It might be hard to imagine how. This could be possible, if the projector, too, has an Ethernet LAN port and supports Wake-on-LAN, as it is expected by the Player Host. But this already forces the Player Host to have at least two Ethernet LAN ports (remember, one already taken for connecting to the Service Host). Also, Ethernet-enabled projectors are not that common, not to talk of them supporting Wake-on-LAN. Anyway, modern marvels have made it possible to gap bridges like these. Which brings us to the final equipment:
* A Naran [MicroBot Push](https://prota.info/). This miracle worker serves as a robotic finger that can push buttons anywhere you place it. It can be controlled via Bluetooth Low Energy device. That's why the Player Host should have a BLE device, while the MicroBot Push gets placed right on top of your projectors on-button. The Player Host will switch the projector on or off all by itself, when needed!
* A mobile device with any OS of your choice. Just needs to have mobile internet and a modern web-browser installed. Of course, it's your router's DNS address you're going to type into the browser. And *very important*: The mobile device must have its *GPS activated permanently*.

## Software components

### SmartMediaCenter Player
The player component of SmartMediaCenter. Accessed through RMI by the SMC Service. Hosted on its own host that is woken up or set asleep by the SMC Service host, as required.

### SmartMediaCenter Service
The service component of SmartMediaCenter, providing a GWT-RPC-based access service for mobile web clients to the SMC through Servlets on a Tomcat webserver serving compiled JavaScript web pages as a GUI. The component is meant to be hosted on a permanently accessible host with very low energy consumption, like as Raspberry Pi. Besides providing the mentioned service to a mobile web-client, this component controls the current playback configuration and the state of media playback on the SMC Player component host via RMI. For this purpose, it also wakes up or sets asleep the SMC Player host, as required.

## Key concept: *Virtual Channels*
