# **Overview**
This section will detail what is needed to setup, power on, connect to, and configure the RAK Wireless Developer gateway and its Raspberry-Pi. This is the basis of the entire pea-POD project and proper setup will necessary as it is the basis for every other step. The following instructions include content copied from the [RAK Quickstart Guide](https://github.com/adamschreck/pea-pod/files/10867195/RAK.Quickstart.Guide.pdf), but has been adapted to further clarify steps.

# **Steps**

## General

ENSURE THAT YOU HAVE COMPLETED THESE STEPS BEFORE POWERING ON THE GATEWAY OR ELSE DAMAGE MAY OCCUR TO ITS INTERNAL HARDWARE.

### Survey Package Contents

1. Check to make sure you have obtained all of the following. Some components can be swapped out ***before beginning*** for various purposes. A micro-SD card with a higher GB capacity can be used for increased storage. Higher power antennas can be connected to increase the range that the gateway can be from a sensor. Antennas or power supplies could also appear different if you are using a weatherproof case.

![rak package contents](https://user-images.githubusercontent.com/126691160/222323617-5eeedf1d-1d76-4ca4-8dfe-a4e911899a76.jpeg)

### Attach Antennas

2. Connect the GPS antenna and LoRa antenna (identified in the figure above) to the terminals of the gateway by screwing until snug. Below is a diagram that identifies which terminal is coordinated with what antenna, it is crucial that these or properly connected so that the gateway with power on and operate correctly.

![RAK Terminals](https://user-images.githubusercontent.com/126691160/222323691-f4fc421a-c4c4-4f9a-a436-9708bee55f37.jpeg)

### Format SD Card

3. Format, or burn, the most up-to-date firmware onto the micro-SD card. To access the most up-to-date firmware and learn how to burn the firmware image onto the SD card follow [this link](https://docs.rakwireless.com/Knowledge-Hub/Learn/WisGate-Developer-Gateway-Firmware-Burning/). The function of the firmware is to structure the computer and provide it basic instructions about how to operate and communicate with other software.

### Insert SD Card

4. With step 3 completed the SD card can now be inserted into the SD card slot of the computer. This slot is labeled in the same diagram as the antenna terminals. To insert the SD card a pair of tweezers or another fine tool may be required to delicately place it without damaging the computer. 

### Power On

5. With steps 1-4 completed the power cord can be inserted into its place, if using the provided supply then it will be the usb-c slot on the side of the case. After plugging in or connecting to power two small LED lights should illuminate.

## Connecting to the Pi

Before you can begin setting up your Pi and gateway you must establish a connection between your computer and the Pi. There are two options that you have to perform this, you can connect wirelessly via the default local network of the Pi (also called Wi-Fi AP Mode) or through a wired ethernet connection between your computer and the Pi. Both options have positives and negatives.

In the next section, after Connecting to the Pi, the use of Terminal and SSH (Secure Shell) will be discussed for you to essentially log into your Pi. In the following sets of instructions for Chirpstack, Grafana, and others your Pi will require a connection to the internet to be able to download the necessary software. Facilitating this internet connection begins here in this step with how you connect to the Pi, and it is important to understand the tradeoffs and make a decision on how you will establish your connection. 

For the wireless or Wi-Fi AP mode, you will be connecting to the local network of Pi, but this means that your personal computer will no longer be connected to your home internet. In later steps you will have to connect the Pi to your home internet, which will disable the Pi's ability to broadcast its own local network. This will also change the Pi's IP address that you will need to SSH to or log in with. With access to your home internet's router, you can overcome this issue. If you intend on using your gateway and Pi without internet long term, then it may be best to use the ethernet connection as it will not disable the local network mode. All of this can also be reversed if you decide to change plans, and how to do that will be shown below. 

Today not all laptops have ethernet ports, and thus not every user will have the ability to connect in this way. But if you do, then your laptop can remain connected to your home internet and still be connected via wire to the Pi.

The steps below will show the Wi-Fi AP mode, but in-depth details of connecting over ethernet are available [here](https://github.com/adamschreck/pea-pod/files/10867195/RAK.Quickstart.Guide.pdf)

### Locate and connect to network

1. Similar to how one may go about setting up a printer at home, the first step is to locate and connect to the local network of the device. To do this open your personal computer's network settings, which is wherever you would go to connect to a new Wi-Fi. In the case of a printer the network may be called something like `HP-ENVY5000`, but in this case the default network name will appear in your Wi-Fi network list as `Rakwireless_XXXX` with the last 4 XXXX digits representing the MAC address (an identifier) of your gateway/Pi. After locating and selecting the network, you will be prompted to input the password. The default password for the local network is ***rakwireless***. An example can be seen in the image below.

![Screen Shot 2023-03-01 at 9 56 29 PM](https://user-images.githubusercontent.com/126691160/222512913-850ad311-5929-466b-bcb9-e09d09c00f9f.png)

### Open Terminal

2. Terminal is essentially a way to interface with the backend of your computer. For windows users access Terminal information from [Microsoft](https://learn.microsoft.com/en-us/windows/terminal/) or look to RAK's explanation in the [Quickstart Guide](https://github.com/adamschreck/pea-pod/files/10867195/RAK.Quickstart.Guide.pdf). 

    For Linux: Follow the Mac process with the exception of the Terminal command of `sudo -i`

    For Mac OS: launch the Terminal application from Spotlight by hitting `Command` + `Spacebar` and typing Terminal, and then return. 

![9 Medium](https://user-images.githubusercontent.com/126691160/222528230-f432d86c-2c19-485e-830a-ee336a40c086.jpeg)

Once Terminal has launched for Mac OS, enter root mode (allows you to take on the role of an administrator on your Mac) type `sudo -i` in the window then click `enter`

This should prompt you to have to input your computer's password and click `enter`. Below is an image depicting how your terminal should appear.

![sudo-mac](https://user-images.githubusercontent.com/126691160/222524088-6bd4fbb8-5153-49df-b127-66dcebe35fab.jpeg)

### SSH into Pi

3. Type `ssh pi@192.168.230.1` (the default IP address of the Pi) in the terminal window then click `enter`. This should prompt you to have to input your Pi's password, the default password is ***raspberry***. Type `raspberry` in the window then click `enter`. After this you will be logged into your Pi for the first time, CONGRATS! The image below depicts how your terminal window should appear after this step.

![Screen Shot 2023-03-02 at 2 05 21 PM](https://user-images.githubusercontent.com/126691160/222528120-b7df3366-1502-491c-9ca2-47ce95905113.png)

## Configuring Gateway Settings

### Login to the Pi's User Interface

1. In your Terminal window type `sudo gateway-config` then click `enter`. This will launch the Pi's User Interface shown below. You can navigate through the different sections using your keyboard's arrow keys and by clicking `enter`. The image below will later be referred to as the ***main menu***.

![config-options](https://user-images.githubusercontent.com/126691160/222538235-df61a6e5-3b84-4563-8105-c09ecbecda86.png)

The sections coordinate to these actions:

- Set pi password - used to set/change the password of the gateway.
- Setup RAK Gateway Channel Plan - used to configure the frequency, on which the gateway will operate, and the LoRaWAN Server which the gateway will work with.
- Restart packet-forwarder - used to restart the LoRa packet forwarder.
- Edit packet-forwarder config - used to open the global_conf.json file, to edit LoRaWAN parameters manually.
- Configure WIFI - used to configure the Wi-Fi settings in order to connect to a network.
- Configure LAN - used to configure the Ethernet adapter settings.

### Set Pi Password

2. Select and enter the `1 Set pi password` option. Follow the on-screen prompt shown below to set a new password for logging onto your Pi. This will replace the default password ***raspberry***. BE SURE TO TAKE NOTE OF THE PASSWORD YOU CREATE; IT IS NECESSARY TO LOGIN TO YOUR Pi AND CANNOT BE RETRIEVED OR RESET LATER

![Screen Shot 2023-03-02 at 2 36 36 PM](https://user-images.githubusercontent.com/126691160/222538504-a0f50d5a-d1e4-4445-bdd9-e9901233e0c7.png)

### Setup RAK Gateway Channel Plan 

3. From the main menu, select and enter the `2 Setup RAK Gateway Channel Plan` option. Then select the `2 Server is ChirpStack` option shown below.

![chirpstack](https://user-images.githubusercontent.com/126691160/222550248-ffed52e2-1a9a-4025-8bc1-2d1fa0da428d.png)

You will then be prompted with two options `1 ChirpStack Channel-plan configuration` and `2 ChirpStack ADR configure`.

![chirpstack_channel](https://user-images.githubusercontent.com/126691160/222551572-20419394-0c6c-4678-a5f7-8485f80f87ae.png)

For now, select `1 ChirpStack Channel-plan configuration`. The screen below will be prompted.

![chirpstack-channel-plan](https://user-images.githubusercontent.com/126691160/222556831-9fdc9d86-8cd9-4ce5-98f0-e0416dd86e8e.png)

This will allow you to select your regional frequency band, here in the US LoRa uses 915 MHz, so if you are in the US select option `10 US_902_928`. The screen below will be prompted and ask for you to assign the IP address for Chirpstack. The default IP that you should enter is `127.0.0.1` then select `OK` to return to the ***ChirpStack Channel-plan configuration**

![loraserver_ip](https://user-images.githubusercontent.com/126691160/222552326-b1439149-6579-4f66-b3e0-b85d55bb5c4a.png)

Now select `2 ChirpStack ADR configure`. This option allows you to choose whether or not you want your network server, responsible for managing your network, to use an Adaptive Data Rate (ADR). An ADR is beneficial in many cases because it allows your network to change the data rate at which packets are sent. Meaning, it can adjust to be a higher or lower data rate depending on adverse conditions like a large distance between your sensor and gateway causing low packet acceptance. Within this screen select `1 Enable ADR` then select `OK` and navigate back to the main menu.

![adr_settings](https://user-images.githubusercontent.com/126691160/222553729-8bb7683f-47df-4a7f-8b19-865c88b0cd14.png)

### Setup Home Internet

THIS STEP WILL RESULT IN CHANGING THE IP ADDRESS OF THE Pi AND HOW YOU LOGIN, IF YOU NEED TO RETURN TO THE ORIGINAL DESCRIPTION OF WHAT THIS WILL DO FOLLOW [THIS LINK](https://github.com/adamschreck/pea-pod/blob/main/Step-1%20Gateway%20and%20Computer%20Setup/Step-1%20Instructions.md#connecting-to-the-pi)

1. Begin by navigating from main menu down to `5 Configure WIFI` and click `Enter`. This will prompt the screen below.

![wifi-ssid](https://user-images.githubusercontent.com/126691160/222596823-6c189999-78a5-442c-a5e9-015b190e31a6.png)

Within the ***Configure wifi*** menu the sections coordinate to these actions:

- Enable AP Mode/Disable Client Mode - the gateway will work in Wi-Fi Access Point mode after rebooting, while the Wi-Fi Client Mode will be disabled (this is the default mode).
- Enable Client Mode/Disable AP Mode - the gateway will work in Wi-Fi Client mode after rebooting, while Wi-Fi AP mode will be disabled.
- Modify SSID and pwd for AP Mode - used to modify the SSID and password of the Wi-Fi AP. Only works if the Wi-Fi AP mode is enabled.
- Add New SSID for Client - this is used if you want to connect to a new Wi-Fi Network. Only works in Wi-Fi Client mode.
- Change Wi-Fi Country - this is used to modify the resident country to match Wi-Fi standards.

2. To enable Wi-Fi Client Mode (your Pi being a client of your home internet's router), you have to disable AP mode first. Do this by choosing `2 Enable Client Mode/Disable AP Mode`. Once this is disabled, you can now connect to your home internet's Wi-Fi Network by choosing `4 Add New SSID for Client.`

Begin by choosing your local region, for example `US - United States` then select `OK`

![region](https://user-images.githubusercontent.com/126691160/222606382-9a1256f6-e28c-4a56-abf7-5680212fa176.png)

Now enter the SSID (service set identifier) of your home internet. The SSID being your network name, for example `xfinitywifi`. MAKE SURE TO INPUT THE CORRECT WIFI SSID AND PASSWORD, AS ENTERING EVEN ONE INCORRENT CHARACTER WILL IMPACT YOUR ABILITY TO SSH INTO YOUR Pi. Select `OK`.

![set-wifi](https://user-images.githubusercontent.com/126691160/222606572-86336899-d8a6-47a1-8478-0b96124503d8.png)

Now type your home internet's password. If there is none then leave this field empty. Select `OK`.

![set-password](https://user-images.githubusercontent.com/126691160/222606628-1f08560b-96fd-4162-84af-45e61cb77384.png)

## Exit and Reboot

1. From the main menu select `Quit` to exit the Pi's user interface and return to the Terminal window. 

2. Lastly, reboot the gateway by typing `sudo reboot` in the command line then `enter`. This is a necessary step in order to enact and save the changes that you have made. By rebooting you will also become logged out of your Pi, to reestablish your connection you will need to follow the steps of the section below.

## Logging Back into Gateway

After completing all of the above steps your Pi will no longer broadcast its local network, originally appearing as some variation of `Rakwireless_XXXX` in your network list, it will no longer be visible here. Instead, your Pi is now a client or resident living on your home internet's router. To be able to SSH or login to your Pi you will need to determine the address of where it is currently living, specifically what its new address is on your router. This address will change as you add and remove devices from your home internet, so you should re-visit these steps if in the future the IP address that you would login with no longer works. 

1. Reconnect your personal computer to your home internet.

2. Identify your home internet's IP address. If you are unfamiliar with this, your router will likely have its IP address printed on its side. If this is not the case, you can find this information from any device connected to that internet network. Specifically you can go to your mobile phone's settings, if you need more information you can look to these links: 

[How to find IP address on Iphone](https://www.howtogeek.com/796854/iphone-ip-address/)

[Steps to find IP addresses on Iphone, Android, macOS, or Windows devices](https://help.joinposter.com/en/articles/5403165-how-to-check-ip-address-of-the-local-network-on-ios-android-and-windows-devices)

3. While connected to your home internet, you can launch your preferred browser and enter your home internet's IP address in the top bar and click `enter`. This should prompt a page similar to the one shown below. After navigating to this page, you can login to your router simply with your home internet's SSID as the username and your regular internet password.

![Screen Shot 2023-03-02 at 10 33 54 PM](https://user-images.githubusercontent.com/126691160/222747624-2dec4c9a-24a4-46c6-ba7e-b0460ff93cd9.png)

4. From here you will need to locate what can be referred to as the DHCP Client Table. This table is list of all of the devices connected to your home internet and other important information. Each router is different, so take note of the brand of router that you have consider searching something similar to `How to find client table on linksys router` and look for articles similar to [this](https://www.linksys.com/gb/support-article/?articleNum=316202). You should be able to locate a table that appears like the one seen below. Here you can see the device `rak-gateway` and its IP address on your network, in this instance being `10.0.0.145`.

![Screen Shot 2023-03-02 at 10 39 36 PM](https://user-images.githubusercontent.com/126691160/222747746-953eb865-59ea-4b68-b61d-f293e17a98ef.png)

5. Now return to your Terminal window and follow the same procedure as mentioned in the [original section](https://github.com/adamschreck/pea-pod/blob/main/Step-1%20Gateway%20and%20Computer%20Setup/Step-1%20Instructions.md#ssh-into-pi) of logging into your Pi. Specifically typing ssh pi@ then your Pi's IP address. In this case the command would be `ssh pi@10.0.0.145` and enter the password that you set up for your Pi. Once you have reached the screen shown below you have logged back in, and officially completed the `Step-1 Gateway and Computer Setup`!

![Screen Shot 2023-03-03 at 11 48 26 AM](https://user-images.githubusercontent.com/126691160/222778897-bf607d00-a510-4f31-9698-addf72bef2ef.png)
