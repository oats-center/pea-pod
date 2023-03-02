# **Introduction**

![PODs Logo 3 Small](https://user-images.githubusercontent.com/126691160/222211216-1fea15bd-3a58-41ff-aba7-03c593b22b7b.jpeg)

This repository is intended to serve as a build guide for the pea-POD, a small Raspberry-Pi based server and LoRaWAN gateway configured to help individuals establish their own IoT (Internet of Things) network. The use case discussed throughout this guide will primarily target weather data collection and agricultural applicaitons, however this architecture could extend to connecting any number of LoRaWAN enabled devices. 

Benefits of the pea-POD, over other weather stations or similar systems, that will be highlighted in more depth in other areas of the guide are its:

- Low-cost
- Lack of subscriptions
- Open source nature that is not dependent upon manufacturers
- Increased data privacy and ownership (data is stored locally and not in the cloud)
- Ability to operate without an internet connection (locally stored and processed data can be viewed by connecting to the Pi's local network)

All of the work has been done by members of the OATS (Open Ag Tech and Systems) research group at Purdue University, and is a part of the larger POD (Purdue OATS DataStation) iniative to share the benefits of LoRaWAN with farmers and others with an interest in data collection and IoT. Each element within this design leverages either off the shelf hardware or open source software. This was intentional, as it helps the pea-POD retain a low cost and approachability. Regardless of experience level or technical background, by following this guide step-by-step readers should be able to establish their own LoRaWAN network and begin collecting data that can translate into improved insights.

For those who have no coding or computer science background this project may seem intimidating, and issues may occur along the way for which this manual does not include a solution. Each component of this system has been chosen for the existing documentation provided by the manufacturers and the amount of community support. This means that with persistence and a problem-solving mindset nearly anything can be solved with online searching. For those with domain expertise, this system can be a jumping off point. If there is a sensor that you want to add, other data that you want to pull in, or an all togehter different approach that you would like to take then this can be a strong base to build from.Ultimately this is a flexible and use case dependent system where several options will be presented, so choose what's best for you! For example; if you have internet access at the site of deployment and want real time data, then implement the Step-5 Cloudflare Tunnel option. 

Below is a diagram describing how the pea-POD system operates:
![LoRaWAN Architecture Diagram](https://user-images.githubusercontent.com/126691160/222313637-d0eff0ab-7047-464b-85d1-eb215a521e0c.jpeg)

### Important Links
- [Explanation of LoRaWAN from The Things Network](https://www.thethingsnetwork.org/docs/lorawan/)

- [PODs Github Page](https://github.com/oats-center/pod)

### Hardware
*THESE LINKS WERE ACTIVE AND AVAILABLE AT THE TIME OF PUBLISHING BUT MAY BE OUT OF STOCK AT THE TIME OF YOUR ACCESS.*

*PLEASE ENSURE THAT ANY PURCHASED HARDWARE IS INTENDED FOR YOUR REGION. LOCALLY THIS MEANS THE UNITED STATES MARKET, POWER SUPPLIES MEANT FOR US OUTLETS, AND THE US RADIO FREQUENCY EXPECTATION OF 915 MHz FOR LoRa TRANSMISSION.*

- [RAK Wireless Wisgate Developer Gateway with Raspberry-Pi Included](https://store.rakwireless.com/products/rak7244-lpwan-developer-gateway?variant=40632122933446)

- [Similar RAK Gateway with Raspberry-Pi Included](https://store.rakwireless.com/products/rak7248?variant=39942866927814)

- [Weatherproof Case for Gateway](https://store.rakwireless.com/products/outdoor-enclosure-kit-h?variant=37912840863942)

- [Recommended Antenna](https://store.rakwireless.com/products/5-8dbi-fiber-glass-antenna?variant=39942855033030)

- [Enclosure Bracket](https://store.rakwireless.com/products/pilot-gateway-pro-enclosure-holders)