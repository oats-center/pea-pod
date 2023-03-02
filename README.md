# **Introduction**

![PODs Logo 3 Small](https://user-images.githubusercontent.com/126691160/222211216-1fea15bd-3a58-41ff-aba7-03c593b22b7b.jpeg)

This repository is intended to serve as a build guide for the pea-POD, a small Raspberry-Pi based server and LoRaWAN gateway configured to help individuals establish their own IoT (Internet of Things) network. The use case discussed throughout this guide will primarily target weather data collection and agricultural applicaitons, however this architecture could extend to connecting any number of LoRaWAN enabled devices. 

Benefits of the pea-POD, over other weather stations or similar systems, that will be highlighted in more depth in other areas of the guide are its:

- Low-cost
- Lack of subscriptions
- Open source nature that is not dependent upon manufacturers
- Increased data privacy and ownership (data is stored locally and not in the cloud)
- Ability to operate without an internet connection (locally stored and processed data can be viewed by connecting to the Pi's local network)

All of the work has been done by members of the OATS (Open Ag Tech and Systems) research group at Purdue University, and is a part of the larger POD (Purdue OATS DataStation) iniative to share the benefits of LoRaWAN with farmers and others with an interest in data collection and IoT. Each element within this design leverages either off the shelf hardware or open source software. This was intentional, as it helps the pea-POD retain a low cost and high approachability. Regardless of experience level or technical background, by following this guide step-by-step readers should be able to establish their own LoRaWAN network and begin collecting data that can translate into improved insights.

Prerequisites for completing this project:

1. A Windows/Mac OS/Linux personal computer (many of the photos and explanations shown will be geared toward Mac OS, while it may appear different for you the information is still applicable for Windows and Linux machines)

2. Internet access at the time of configuration

3. The necessary hardware, this guide will detail the RAK7244 Wisgate Developer Gateway

4. A mechanism to plug a micro SD card into your computer (likely through some sort of dongle or micro SD to SD card adapter)

4. Awareness of what LoRaWAN is (see [What is LoRaWAN?.pdf](https://github.com/adamschreck/pea-pod/files/10872800/What.is.LoRaWAN.pdf) or [Explanation of LoRaWAN from The Things Network](https://www.thethingsnetwork.org/docs/lorawan/) for a rudimentary explanation)

5. A general idea of what terminal and terminal commands are (very little to no coding experience will be required and all necessary terminal commands will be included in the instructions)

6. Surface level understanding of IP addresses (see [this link](https://www.wpbeginner.com/glossary/ip-address/) for more information) and the ability to 

For those who have no coding or computer science background this project may seem intimidating, and issues may occur along the way for which this manual does not include a solution. Each component of this system has been chosen for the existing documentation provided by the manufacturers and the amount of community support. This means that with persistence and a problem-solving mindset nearly anything can be solved with online searching. For those with domain expertise, this system can be a jumping off point. If there is a sensor that you want to add, other data that you want to pull in, or an all togehter different approach that you would like to take then this can be a strong base to build from. Ultimately this is a flexible and use case dependent system where several options will be presented, so choose what's best for you! For example: if you have internet access at the site of deployment and want real time data, then implement the Step-5 Cloudflare Tunnel option. 

Below is a diagram describing how the pea-POD architecture operates:

![LoRaWAN Architecture Diagram](https://user-images.githubusercontent.com/126691160/222314712-d92d4ce6-192b-450c-a3b9-abc11066ab1f.jpeg)

### Important Links
- [Explanation of LoRaWAN from The Things Network](https://www.thethingsnetwork.org/docs/lorawan/)

- [PODs Github Page](https://github.com/oats-center/pod)

### Hardware
*THESE LINKS WERE ACTIVE AND AVAILABLE AT THE TIME OF PUBLISHING BUT MAY BE OUT OF STOCK AT THE TIME OF YOUR ACCESS.*

*PLEASE ENSURE THAT ANY PURCHASED HARDWARE IS INTENDED FOR YOUR REGION. LOCALLY THIS MEANS THE UNITED STATES MARKET, POWER SUPPLIES MEANT FOR US OUTLETS, AND THE US RADIO FREQUENCY EXPECTATION OF 915 MHz FOR LoRa TRANSMISSION.*

- [RAK Wireless Wisgate Developer Gateway with Raspberry-Pi Included](https://store.rakwireless.com/products/rak7244-lpwan-developer-gateway?variant=40632122933446)

- [Similar RAK Gateway with Raspberry-Pi Included](https://store.rakwireless.com/products/rak7248?variant=39942866927814)

- [Weatherproof Case for Gateway](https://store.rakwireless.com/products/outdoor-enclosure-kit-h?variant=37912840863942)

- [Recommended Antenna if in Weatherproof Case](https://store.rakwireless.com/products/5-8dbi-fiber-glass-antenna?variant=39942855033030)

- [Gateway Enclosure Bracket](https://store.rakwireless.com/products/pilot-gateway-pro-enclosure-holders)