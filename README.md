# SmartMediaCenter

A mobile client-server architecture for controlling your home cinema

# The idea
You have a home cinema with the following hardware equipment:
* Ideally, a low-energy single-board computer like a Raspberry Pi. Or otherwise: Just a computer that can act as a server. Let's call it the **Service Host**. It is permanently on-line and accessible from the internet through proper NAT-settings on your home network's router. Make sure your router itself is accessible through a static IP address. Alternatively, you can set it up to use a Dynamic DNS server. Find some free ones [here](https://www.noip.com/free), [here](https://www.dnsdynamic.org/) or [here](http://www.dyndnss.net/updater.php). The Service Host needs to be able to wake up the following host:
* Any personal Desktop computer, called the **Player Host** that can be woken up in some form by the Service Host. Typically, that's via Wake-on-LAN or some similar technology. The Player Host must have internet access and be able to play back audio and video multimedia content by its hardware. It is extended by the following periphery permanently connected to it:
* Speakers
* Headphones (optional)
* A projector (very important)

# The components
## SmartMediaCenter Player
The player component of SmartMediaCenter. Accessed through RMI by the SMC Service. Hosted on its own host that is woken up or set asleep by the SMC Service host, as required.


## SmartMediaCenter Service
The service component of SmartMediaCenter, providing a GWT-RPC-based access service for mobile web clients to the SMC through Servlets on a Tomcat webserver serving compiled JavaScript web pages as a GUI. The component is meant to be hosted on a permanently accessible host with very low energy consumption, like as Raspberry Pi. Besides providing the mentioned service to a mobile web-client, this component controls the current playback configuration and the state of media playback on the SMC Player component host via RMI. For this purpose, it also wakes up or sets asleep the SMC Player host, as required.


