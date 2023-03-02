# **Overview**
This section will detail what is needed to setup, power on, connect to, and configure the RAK Wireless Developer gateway and its Raspberry-Pi. This is the basis of the entire pea-POD project and proper setup will necessary as it is the basis for every other step. The following instructions are copied from the [RAK Quickstart Guide](https://github.com/adamschreck/pea-pod/files/10867195/RAK.Quickstart.Guide.pdf), but has been adapted to further clarify steps.

# **Steps**

## General

ENSURE THAT YOU HAVE COMPLETED THESE STEPS BEFORE POWERING ON THE GATEWAY OR ELSE DAMAGE MAY OCCUR TO ITS INTERNAL HARDWARE.

### Survey Package Contents

1. Check to make sure you have obtained all of the following. Some components can be swapped out ***before beginning*** for various purposes. A micro SD card with a higher GB capacity can be used for increased storage. Higher power antennas can be connected to increase the range that the gateway can be from a sensor. Antennas or power supplies could also appear different if you are using a weatherproof case.

![rak package contents](https://user-images.githubusercontent.com/126691160/222323617-5eeedf1d-1d76-4ca4-8dfe-a4e911899a76.jpeg)

### Attach Antennas

2. Connect the GPS antenna and LoRa antenna (identified in the figure above) to the terminals of the gateway by screwing until snug. Below is a diagram that identifies which terminal is coordinated with what antenna, it is crucial that these or properly connected so that the gateway with power on and operate correctly.

![RAK Terminals](https://user-images.githubusercontent.com/126691160/222323691-f4fc421a-c4c4-4f9a-a436-9708bee55f37.jpeg)

### Format SD Card

3. Format, or burn, the most up-to-date firmware onto the micro SD card. To access the most up-to-date firmware and learn how to burn the firmware image onto the SD card follow [this link](https://docs.rakwireless.com/Knowledge-Hub/Learn/WisGate-Developer-Gateway-Firmware-Burning/). The function of the firmware is to structure the computer and provide it basic instructions about how to operate and communicate with other softwares.

### Insert SD Card

4. With step 3 completed the SD card can now be inserted into the SD card slot of the computer. This slot is labeled in the same diagram as the antenna terminals. To insert the SD card a pair of tweezers or other fine tool may be required to delicately place it without damaging the computer. 

### Power On

5. With steps 1-4 completed the power cord can be inserted into its place, if using the provided supply then it will be the usb-c slot on the side of the case. After plugging in or connecting to power two small LED lights should illuminate.

## Connecting to the Pi

Before you can begin setting up your Pi and gateway you must establish a connection between your computer and the Pi. There are two options that you have to perform this, you can connect wirelessly via the default local network of the Pi (also called Wi-Fi AP Mode) or through a wired ethernet connectiion between your computer and the Pi. Both options have positives and negatives.

In the next section, after Connecting to the Pi, the use of terminal and ssh (Secure Shell) will be discussed for you to essentially log into your Pi. In the following sets of instructions for Chirpstack, Grafana, and others your Pi will require a conncetion to the internet to be able to download the necessary software. Facilitating this internet connection begins here in this step with how you connect to the Pi, and it is important to understand the tradeoffs and make a decision on how you will establish your connection. 

For the wireless or Wi-Fi AP mode, you will be connecting to the local network of Pi, but this means that your personal computer will no longer be connected to your home internet. In later steps you will have to connect the Pi to your home internet, which will disable the the Pi's ability to broadcast its  own local network. This will also change the Pi's IP address that you will need to ssh to or log in with. With access to your home internet's router you can overcome this issue. If you intend on using your gateway and Pi without internet long term, then it may be best to use the ethernet connection as it will not disable the local network mode. All of this can also be reversed if you decide to chnage plans, and how to do that will be shown below. 

Today not all laptops have ethernet ports, and thus not every user will have the ability to connect in this way. But if you do, then your laptop can remain connected to your home internet and still be connected via wire to the Pi.

The steps below will show the Wi-Fi AP mode, but in depth details of connecting over ethernet are available [here](https://github.com/adamschreck/pea-pod/files/10867195/RAK.Quickstart.Guide.pdf)

###Locate and connect to network

1. Similar to how one may go about setting up a printer at home, the first step is to locate and connect to the local network of the device. To do this open your personal computer's network settings, which is wherever you would go to connect to a new Wi-Fi. In the case of a printer the network may be called something like "HP-ENVY5000", but in this case the default network name will appear in your Wi-Fi network list as "Rakwireless_XXXX" with the last 4 XXXX digits representing the MAC address (an identifier) of your gateway/Pi. After locating and selecting the network, you will be prompted to input the password. The default password for the local network is ***rakwireless***. An example can be seen in the image below.

![Screen Shot 2023-03-01 at 9 56 29 PM](https://user-images.githubusercontent.com/126691160/222512913-850ad311-5929-466b-bcb9-e09d09c00f9f.png)
