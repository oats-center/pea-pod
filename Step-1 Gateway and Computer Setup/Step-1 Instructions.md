# **Overview**
This section will detail what is needed to setup, power on, connect to, and configure the RAK Wireless Developer gateway and its Raspberry-Pi. This is the basis of the entire pea-POD project and proper setup will necessary as it is the basis for every other step. The following instructions include content copied from the [RAK Quickstart Guide](https://github.com/adamschreck/pea-pod/files/10867195/RAK.Quickstart.Guide.pdf), but has been adapted to further clarify steps.

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

### Locate and connect to network

1. Similar to how one may go about setting up a printer at home, the first step is to locate and connect to the local network of the device. To do this open your personal computer's network settings, which is wherever you would go to connect to a new Wi-Fi. In the case of a printer the network may be called something like "HP-ENVY5000", but in this case the default network name will appear in your Wi-Fi network list as "Rakwireless_XXXX" with the last 4 XXXX digits representing the MAC address (an identifier) of your gateway/Pi. After locating and selecting the network, you will be prompted to input the password. The default password for the local network is ***rakwireless***. An example can be seen in the image below.

![Screen Shot 2023-03-01 at 9 56 29 PM](https://user-images.githubusercontent.com/126691160/222512913-850ad311-5929-466b-bcb9-e09d09c00f9f.png)

### Open Terminal

2. Terminal is essentially a way to interface with the backend of your computer. For windows users access Terminal information from [Microsoft](https://learn.microsoft.com/en-us/windows/terminal/) or look to RAK's explanation in the [Quickstart Guide](https://github.com/adamschreck/pea-pod/files/10867195/RAK.Quickstart.Guide.pdf). 

    For Linux: Follow the Mac process with the exception of the Terminal command of `sudo -i`

    For Mac OS: launch the Terminal application from Spotlight by hitting `Command` + `Spacebar` and typing Terminal, and then return. 

![9 Medium](https://user-images.githubusercontent.com/126691160/222528230-f432d86c-2c19-485e-830a-ee336a40c086.jpeg)

Once Terminal has lauched for Mac OS, enter root mode (allows you to take on the role of an administrator on your Mac) type `sudo -i` in the window then click `enter`

This should prompt you to have to input your computer's password and click `enter`. Below is an image depicting how your terminal should appear.

![sudo-mac](https://user-images.githubusercontent.com/126691160/222524088-6bd4fbb8-5153-49df-b127-66dcebe35fab.jpeg)

### SSH into Pi

3. Type `ssh pi@192.168.230.1` (the default IP address of the Pi) in the terminal window then click `enter`. This should prompt you to have to input your Pi's password, the default password is ***raspberry***. Type `raspberry` in the window then click `enter`. After this you will be logged into your Pi for the first time, CONGRATS! The image below depicts how your terminal window should appear after this step.

![Screen Shot 2023-03-02 at 2 05 21 PM](https://user-images.githubusercontent.com/126691160/222528120-b7df3366-1502-491c-9ca2-47ce95905113.png)

## Configuring Gateway Settings

### Login to the Pi's User Interface

1. In your Terminal window type `sudo gateway-config` then click `enter`. This will lauch the Pi's User Interface shown below. You can navigate through the different sections using your keyboard's arrow keys and by clicking `enter`. The image below will later be refered to as the main menu.

![config-options](https://user-images.githubusercontent.com/126691160/222538235-df61a6e5-3b84-4563-8105-c09ecbecda86.png)

The sections coordinate to these actions:

- Set pi password - used to set/change the password of the gateway.
- Setup RAK Gateway Channel Plan - used to configure the frequency, on which the gateway will operate, and the LoRaWAN Server which the gateway will work with.
- Restart packet-forwarder - used to restart the LoRa packet forwarder.
- Edit packet-forwarder config - used to open the global_conf.json file, to edit LoRaWAN parameters manually.
- Configure WIFI - used to configure the Wi-Fi settings in order to connect to a network.
- Configure LAN - used to configure the Ethernet adapter settings.

### Set Pi Password

2. Select and enter the `1 Set pi password` option. Follow the on screen prompt shown below to set a new password for logging onto your Pi. This will replace the default password ***raspberry***. BE SURE TO TAKE NOTE OF THE PASSWORD YOU CREATE, IT IS NECESSARY TO LOGIN TO YOUR Pi AND CANNOT BE RETRIEVED OR RESET LATER

![Screen Shot 2023-03-02 at 2 36 36 PM](https://user-images.githubusercontent.com/126691160/222538504-a0f50d5a-d1e4-4445-bdd9-e9901233e0c7.png)

### Setup RAK Gateway Channel Plan 

3. From the main menu, select and enter the `2 Setup RAK Gateway Channel Plan` option. Then select the `2 Server is ChirpStack` option shown below.

![chirpstack](https://user-images.githubusercontent.com/126691160/222550248-ffed52e2-1a9a-4025-8bc1-2d1fa0da428d.png)

You will then be prompted with two options `1 ChirpStack Channel-plan configuration` and `2 ChirpStack ADR configure`.

![chirpstack_channel](https://user-images.githubusercontent.com/126691160/222551572-20419394-0c6c-4678-a5f7-8485f80f87ae.png)

For now select `1 ChirpStack Channel-plan configuration`. The screen below will be prompted.

![chirpstack-channel-plan](https://user-images.githubusercontent.com/126691160/222556831-9fdc9d86-8cd9-4ce5-98f0-e0416dd86e8e.png)

This will allow you to select your regional frequency band, here in the US LoRa uses 915 MhZ, so if you are in the US select option `10 US_902_928`. The screen below will be prompted and ask for you to assign the IP address for Chirpstack. The default IP that you should enter is `127.0.0.1` then select `OK` to return to the ***ChirpStack Channel-plan configuration**

![loraserver_ip](https://user-images.githubusercontent.com/126691160/222552326-b1439149-6579-4f66-b3e0-b85d55bb5c4a.png)

Now select `2 ChirpStack ADR configure`. This option allows you to choose whether or not you want your network server, responsible for managing your network, to use an Adaptive Data Rate (ADR). An ADR is beneficial in many cases because it allows your network to change the data rate at which packets are sent. Meaning, it can adjust to be a higher or lower data rate depending on adverse conditions like a large distance between your sensor and gateway causing low packet acceptance. Within this screen select `1 Enable ADR` then select `OK` and navigate back to the main menu.

![adr_settings](https://user-images.githubusercontent.com/126691160/222553729-8bb7683f-47df-4a7f-8b19-865c88b0cd14.png)

### Setup Home Internet

THIS STEP WILL RESULT IN CHANGING THE IP ADDRESS OF THE Pi AND HOW YOU LOGIN, IF YOU NEED TO RETURN TO THE ORIGINAL DESCRIPTION FOLLOW [THIS LINK](https://github.com/adamschreck/pea-pod/blob/main/Step-1%20Gateway%20and%20Computer%20Setup/Step-1%20Instructions.md#connecting-to-the-pi)

1. Begin by navigating from main menu down to `4 Add New SSID for Client`

![wifi-ssid](https://user-images.githubusercontent.com/126691160/222596823-6c189999-78a5-442c-a5e9-015b190e31a6.png)
