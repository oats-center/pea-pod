# **Overview**

Possible sensors to be used with any LoRaWAN network include a variety of options in both type of measurement and brand. While not specifically identified as LoRaWAN sensors, if properly wired and configured with a LoRaWAN specific sensor node, many options become available. This makes this set of instructions very situation and use case dependent, and thus may not offer the same sort of assitance as other sections. 

When planning the sensors that you will use in your data pipeline consider what information is important to your use case. If you are wanting to collect weather information then the sensors below may be appropriate. If not, or if there are additional data points that you want to collect, then with some searching you can likely find the right sensors for you. One place to start would be to purchase the [Dragino LSN50-V2 Sensor Node](https://www.digikey.com/en/products/detail/seeed-technology-co.,-ltd/113990820/16652879?utm_adgroup=RF%20Receiver%2C%20Transmitter%2C%20and%20Transceiver%20Finished%20Units&utm_source=google&utm_medium=cpc&utm_campaign=Shopping_Product_RF%2FIF%20and%20RFID_NEW&utm_term=&utm_content=RF%20Receiver%2C%20Transmitter%2C%20and%20Transceiver%20Finished%20Units&gclid=CjwKCAiAu5agBhBzEiwAdiR5tJAdWvo_F1_0obLfVvfQeP2EDNY0Y6JR-78-ETDYIk84oDZ6JDbiYRoCjG0QAvD_BwE) as it is one of the most widely available and widely documented LoRaWAN sensor nodes on the market. This build guide will not detail any projects with this specific sensor node. However, with this and other sensors and nodes that you source you can research and find CODEC's on various community forums such as the [Chirpstack Community for Devices](https://forum.chirpstack.io/c/devices/8) and [The Things Network Community for Devices](https://www.thethingsnetwork.org/forum/c/nodes/7).

This set of instructions, like most of this entire build guide, is focused on creating the LoRaWAN network not specific devices or use cases. Thus, this is primarily intended to explain the steps necessary to set up the PODs kit devices on Chirpstack. The same steps are generally applicable to other sensors and nodes. These steps are not intended to explain the wiring of sensors and sensor nodes or other intricacies. The instructions below will pull information directly from the [original POD build guide](https://github.com/oats-center/pod/blob/main/build-guide.md).

For demonstration purposes a selection of five sensors was made to accompany the original PODs kit when deployed. These sensors were selected to be able to measure metrics felt to be valuable for most operational decisions; including rainfall, temperature, soil moisture, relative humidity, sunlight, and location. In the majority of installations three sensors, the Davis rain gauge tipping bucket, Vegetronix soil moisture sensor, and TEWA thermistor, were wired to a singular Digital Matter SensorNode. One Tektelic Agricultural Surface Sensor was provided with the ability to sense soil moisture and temperature, ambient humidity and environmental temperature, and light detection and measurement. Two Digital Matter Oyster GPS trackers were included with the intent to track assets or machine activity through a field. The entire sensor suite is shown below in the figure and described in greater detail in the table below.

# **Hardware**

![Sensors](https://user-images.githubusercontent.com/126691160/223175236-9b394e6f-4a9f-421d-9531-d138eb80b908.jpg)

| ID     | Description | Component Name | Manufacturer | Approximate Per Unit Cost | URL |
| -------| ----------- | -------------- | ------------ | ------------------------- | ----------- |
| 1 | Sensor Node | SensorNode LoRaWAN | Digital Matter | $133.48 | [link](https://www.restotracker.com/product/sensornode-lorawan/) |
| 2 | Rain gauge | Davis AeroCone Rain Gauge with Mountable Base | Davis Instruments | $97.5 | [link](https://www.scientificsales.com/6466-Davis-AeroCone-Rain-Gauge-with-Mountable-Base-p/6466.htm) |
| 3 | Soil Moisture Sensor | Soil Moisture Sensor - 2 meter cable | Vegetronix | $48.95 | [link](https://www.vegetronix.com/Products/VH400/) |
| 4 | Air Temperature Sensor | NTC Thermistor 10k Probe | TEWA Sensors LLC | $4.20 | [link](https://www.digikey.com/en/products/detail/tewa-sensors-llc/TT02-10KC3-T105-1500/8549162) |
| 5 | Oyster (GPS) | Oyster LoRaWAN | Digital Matter | $121.50 | [link](https://www.restotracker.com/product/oyster-lorawan/) |
| 6 | Tektelic Ag Sensor (VWC, light, air temp, humdity) | Agricultural Surface Sensor | TEKTELIC Communications Inc. | $136.05 | [link](https://www.digikey.com/en/products/detail/tektelic-communications-inc/T0005982/13168751) |

# **Steps**

## Creating Device Profiles

### Create device profile: Digital Matter Oyster

Create a device profile by selecting "Device-profiles" from the left panel menu, and hitting `+ CREATE`.
Please use these settings:

GENERAL tab:

- Device-profile name: `Digital Matters Oyster`
- Network-server: Choose `POD Network Server`
- LoRaWAN MAC version: `1.0.4`
- LoRaWAN Regional Parameters revision: `A`
- ADR Algorithm: `Default ADR algorithm (LoRa only)`
- Max EIRP: `17`
- Uplink interval: `3600`

JOIN (OTAA / ABP) tab:

- Select "Device supports OTAA"

CODEC tab:

- Payload codec: `Custom JavaScript codec functions`
- Copy and past the code [from here](https://raw.githubusercontent.com/oats-center/pod/master/codecs/digital_matters_oyster.js) input the "Decode" textbox.
- Leave the "Encode" textbox as the default.

Hit `CREATE DEVICE-PROFILE`

### Create device profile: Rain Guage (DM SensorNode)

Create a device profile by selecting "Device-profiles" from the left panel menu, and hitting `+ CREATE`.
Please use these settings:

GENERAL tab:

- Device-profile name: `Rain Gauge (DM SensorNode)`
- Network-server: Choose `POD Network Server`
- LoRaWAN MAC version: `1.0.4`
- LoRaWAN Regional Parameters revision: `A`
- ADR Algorithm: `Default ADR algorithm (LoRa only)`
- Max EIRP: `20`
- Uplink interval: `3600`

JOIN (OTAA / ABP) tab:

- Select "Device supports OTAA"

CODEC tab:

- Payload codec: `Custom JavaScript codec functions`
- Copy and past the code [from here](https://raw.githubusercontent.com/oats-center/pod/master/codecs/digital_matters_sensor_node_rain_soil_temp.js) input the "Decode" textbox.
- Leave the "Encode" textbox as the default.

Hit `CREATE DEVICE-PROFILE`

### Create device profile: Tektelic Ag Sensor

Create a device profile by selecting "Device-profiles" from the left panel menu, and hitting `+ CREATE`.
Please use these settings:

GENERAL tab:

- Device-profile name: `Tektelic Ag Sensor`
- Network-server: Choose `POD Network Server`
- LoRaWAN MAC version: `1.0.4`
- LoRaWAN Regional Parameters revision: `A`
- ADR Algorithm: `Default ADR algorithm (LoRa only)`
- Max EIRP: `23`
- Uplink interval: `3600`

JOIN (OTAA / ABP) tab:

- Select "Device supports OTAA"

CODEC tab:

- Payload codec: `Custom JavaScript codec functions`
- Copy and past the code [from here](https://raw.githubusercontent.com/oats-center/pod/master/codecs/tektelic_ag_sensor.js) input the "Decode" textbox.
- Leave the "Encode" textbox as the default.

Hit `CREATE DEVICE-PROFILE`

## Creating your POD application

Applications in Chirpstack hold a set of devices to communicate with.
They also control how the received device data is set to integrated systems, like Thingsboard.

To create an application, go to Applications from the left panel menu, and select `+ CREATE`.
Please use these settings:

- Application name: `POD-Kit`
- Application description: `POD Kit Sensors`
- Service-profile: `POD Profile`

Select `CREATE APPLCATION`

Add Thingsboard integration
- Go to the Integrations tab within `POD-Kit`
- Under Thingsboard.io click `ADD`
- For the thingsboard.io server use `http://thingsboard:9090`
- Click `Update Integration` 

## Adding Devices

### Add device: Tektelic Ag Sensor

You will need the physical device and its EUI and application key of the Ag Sensor.
This is usually in printed as a label in the box.

To create a device, start on the relevant application page and select `+ CREATE`.
Please use these settings:

- Device name: `Surface-Ag-XXXX` (where XXXX is the last four digital of the device ID, which makes it easier to locate later.)
- Device description: `Tektelic Ag Sensor`
- Device EUI: From the manufactures label
- Device profile: `Tektelic Ag Sensor`

Client `Create`

- Application key: From the manufactures label

With the device added into Chirpstack, use the provided magnet to turn on the device as described in the device manual.
After a few moments, the "Last seen" column should show a time or `a few seconds ago` that indicates the devices connected.

You can configure the sensor for a different sample rate by sending it a LoRaWAN downlink.
The device manual provides more details.
By default, the device will:

- Send battery voltage once per day,
- Send ambient temperature once per 15 mins,
- Send ambient relative humidity once per 15 mins,
- Send ambient soil moisture once per 15 mins,
- Send ambient soil temperature once per 15 mins,
- Send ambient light once per 15 mins,

### Add device: Digital Matters Oyster

You will need the physical device and its EUI, network key, and the application key of the Oyster.
This can be found on a label in the Oyster box as well as easily copy and pasted from the Digital Matters oyster configuration tool.

#### Configure the Oyster

1. Install the [Digital Matters configuration tool](https://support.digitalmatter.com/support/solutions/articles/16000069244-oyster-lorawan-config-app)
2. Connect the Digital Matters debug cable to Oyster and to your computer.
3. Start the configuration tool, and select the COM port associated with the debug cable.
4. Download the [Oyster configuration](https://raw.githubusercontent.com/oats-center/pod/main/digital-matter-parameters/oyster), load it into the configuration app, and adjust as needed.
5. Check the `Program Parameters` checkbox.
6. Plug the debug cable into the Oyster.
7. Insert batteries.
8. Wait until the new parameters have been installed.
9. Open the `DevEUI List` screen and copy the device EUI and both network and session keys to a safe place.

To create the device within Chirpstack, go to the relevant application page and select `+ CREATE`.
Please use these settings:

- Device name: `Oyster-XXXX` (where XXXX is the last four digital of the device ID, which makes it easier to locate later.)
- Device description: `Digital Matters Oyster`
- Device EUI: From the manufactures label and/or configuration app
- Device profile: `Digital Matters Oyster`

Client `Create`

- Application key: From the manufactures label and/or configuration app.
- Network key: From the manufactures label and/or configuration app.

**Access token will be added in the Thingsboard section under "Add Devices"**

With the device added into Chirpstack, power cycle the device by pulling the batteries, waiting 10 seconds, and then re-inserting.
After a few moments, the "Last seen" column should show a time or `a few seconds ago` that indicates the devices connected.

### Add device: Rain Gauge

You will need the physical device and its EUI, network key, and the application key of the sensor node.
This can be found on a label in the Oyster box as well as easily copy and pasted from the Digital Matters oyster configuration tool.

#### Configure the Digital Matter Sensor Node

1. Install the [Digital Matters configuration tool](https://support.digitalmatter.com/support/solutions/articles/16000093348-sensornode-lorawan-configuration-and-usage-guide)
2. Connect the Digital Matters debug cable to Sensor Node and to your computer.
3. Start the configuration tool, and select the COM port associated with the debug cable.
4. Download the [Rain Gauge Sensor Node configuration](https://raw.githubusercontent.com/oats-center/pod/main/digital-matter-parameters/sensor-node), load it into the configuration app, and adjust as needed.
5. Check the `Program Parameters` checkbox.
6. Plug the debug cable into the Sensor Node.
7. Insert batteries.
8. Wait until the new parameters have been installed.
9. Open the `DevEUI List` screen and copy the device EUI and both network and session keys to a safe place.

To create the device within Chirpstack, go to the relevant application page and select `+ CREATE`.
Please use these settings:

- Device name: `Rain-Gauge-XXXX` (where XXXX is the last four digital of the device ID, which makes it easier to locate later.)
- Device description: `Digital Matters sensor node w/ rain gauge, air temperature, soil moisture`
- Device EUI: From the manufactures label and/or configuration app
- Device profile: `Rain Gauge (DM SensorNode)`

Client `Create`

- Application key: From the manufactures label and/or configuration app.
- Network key: From the manufactures label and/or configuration app.

With the device added into Chirpstack, power cycle the device by pulling the batteries, waiting 10 seconds, and then re-inserting.
After a few moments, the "Last seen" column should show a time or `a few seconds ago` that indicates the devices connected.
