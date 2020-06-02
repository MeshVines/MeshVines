![](RackMultipart20200602-4-1k91q4r_html_4b245d8aa650c39e.jpg)

# **MeshVines: Zigbee® Temperature, Humidity and CO2 Wireless Sensor Network**

**Project Overview**

This project represents senior design work of undergraduates in the Electrical Engineering Department at the University of California, Davis. The goal of this project was to create a Zigbee sensor network to monitor the temperature, humidity and CO2 in a winery.

**Main Components**

Texas Instruments

- CC1352r Wireless MCU
- TPS22860 Ultra-Low Leakage Load Switch
- TPL5111 Nano-Power System Timer
- TPS61291 DC-DC Boost
- HDC1080 Ultra-Power Temperature Humidity Sensor

COZIR

- GC-0012 5,000 ppm CO2 Sensor

Polycase

- SN-29
- SN-22
- ML-44F

**Design Features**

- Battery Life of 23 months
- 3% Relative Humidity Accuracy
- Temperature Accuracy
- 50 ppm CO2 Accuracy
- Unit cost less than $35 at 30 units
- Zigbee Mesh Network

#


# Table of Contents

**[Table of Contents](#_bqwg5a180l7e) 2**

**[1 System Description](#_v47b8lscjgvd) 4**

[1.1 Temperature, Humidity and CO2 Sensors](#_u7z4s9c2k24p) 4

[1.2 Ultra-Low Power Wireless Microcontroller (MCU)](#_f2d0v3vtkd2i) 5

[1.3 Nano-Power System Timer](#_pxxk28d5r6zc) 6

[1.4 Boost Converter](#_1vvmb7l45ie) 7

[1.5 Low-Leakage Load Switch](#_6idbwnv2cdc2) 8

[1.6 IFA Antenna](#_92cnit3l6io2) 8

[1.7 Power Methods](#_iae6uem3ys1i) 9

**[2 System Design Theory and Considerations](#_5v2dfx3az1r7) 10**

[2.1 Duty-Cycled Power Calculations](#_sdwakkq3l7rs) 11

[2.2 Firmware](#_ldakdu91hls0) 11

[2.3 Zigbee Network](#_x0zmup1763kg) 12

[2.4 Zigbee Gateway](#_3kamdmnngyhn) 13

[2.5 Antenna Design](#_s78utcrihxjy) 15

**[3 Hardware Versions](#_3vgfs99lqnc3) 16**

[3.1 Hardware Overview](#_qh9f6ylnn8zb) 16

[3.1.1 MeshVines\_RE\_THC\_WB1000](#_jecwgsq5791z) 17

[3.1.2 MeshVines\_RE\_TH\_WB220](#_sc7fgbdgtdoc) 18

[3.1.3 MeshVines\_C\_W](#_q14xw2dwpl7h) 19

[3.1.4 MeshVines\_R\_TH\_WB5200](#_8b83c3lqrrmj) 20

**[4 Implementation Results and Characterization](#_u0wwsx6isncb) 21**

[4.1 Jess S Jackson Sustainable Winery Building Results](#_85fqmgpxqldv) 21

[4.1.1 Node Placement](#_6hhwcknfhb25) 22

[4.1.2 Recorded Data](#_dcot728w6pmo) 23

[4.2 Apartment Building Results](#_cdf2j19j70zv) 25

[4.2.1 Node Placement](#_ckfjzyiclygw) 25

[4.2.2 Recorded Data](#_7hjeuekw21bv) 26

[4.3 Power Consumption](#_i33cvs9y0aga) 27

[4.3.1 On-State Power Characterization](#_2yknireuwo78) 27

[4.3.2 Off-State Power Characterization](#_mort9sz85mlf) 27

[4.3.3 Estimated Battery Life Calculations](#_odfz272gojfb) 27

[4.4 Verification of Mesh Network](#_b3ag3b21ymd) 28

[4.5 Cost Analysis](#_s9w0w6awmlvw) 28

**[5 Conclusion](#_3wlgcwfz1aef) 29**

**[6 Team Members](#_y66gwplzxo8y) 29**

**[7 Acknowledgements](#_xbvj2byctai2) 29**

**[8 References](#_50zl4iwk749e) 30**

#


#


#


#


# 1 System Description

Temperature, humidity and CO2 are important parameters for wineries to monitor. Temperature provides important feedback on the health of the building&#39;s HVAC systems, while humidity is directly correlated to evaporation of wine as it ages in barrell rooms. By both monitoring and controlling for humidity, this loss of wine, and ultimately revenue, can be minimized. Additionally, during the fermentation of wine, sugar in juice is converted to alcohol and CO2 is produced as a byproduct. Since it is denser than air, CO2 can linger in pockets of a building and poses a serious health risk to employees. Current measurement systems often consist of a single sensor or a hand-held device that requires an employee to manually walk around to check CO2 levels. This project provides a cost-effective solution for wineries to monitor these parameters with a high temporal and spatial resolution.

## **1.1 Temperature, Humidity and CO2 Sensors**

![](RackMultipart20200602-4-1k91q4r_html_4ad5c37ecc12592e.jpg)

Fig 1. HDC1080 Block Diagram

The HDC1080 temperature and humidity sensor from Texas Instruments was chosen for its high accuracy and low power, drawing only 1.3 uA for an 11-bit measurement. Additionally, it comes with an I2C interface and a 3 mm x 3 mm footprint.

The COZIR GC-0012 CO2 sensor was chosen for its high accuracy and low power. The COZIR uses Non-dispersive infrared (NDIR) to measure the CO2 in ppm to within 30ppm. The COZIR CO2 sensor comes in different versions that can measure up to 2,000, 5,000, and 10,000 ppm. Outdoor air typically ranges from 300 to 500 ppm. The OSHA Permissible Exposure Limit for 8-hour exposure is 5,000 ppm, therefore the 5,000 ppm measurement range of this sensor was chosen. The COZIR CO2 sensor also features a fast response time of 1.2 seconds, making it attractive for use in a low power system.

## 1.2 Ultra-Low Power Wireless Microcontroller (MCU)

![](RackMultipart20200602-4-1k91q4r_html_36ac5fd48fef0b34.jpg)

Fig 2. CC1352r Block Diagram

To collect data from sensors and transmit to a central node, a radio and processor is necessary and must be low power. The CC1352r was chosen for this application. As a part of TI&#39;s SimpleLink(tm) ultra-low power wireless microcontroller (MCU) platform, software development is standard across this family of devices. In addition, a Zigbee 3.0 device can be created quickly with the provided Z-Stack software resources from TI. The CC1352r is a multi-standard device that supports a wide range of communication protocols including IEEE 802.15.4 for Zigbee.

## 1.3 Nano-Power System Timer

![](RackMultipart20200602-4-1k91q4r_html_5791468417accfbd.jpg)

Fig 3. TPL5111 Block Diagram

To maximize battery life, a nano-power system timer is used. The use of this device replaces the internal timer of any standard microcontroller with a discrete analog system timer that consumes much less power than the microconteroller&#39;s internal timer. The external timer can then be used to bring an MCU out of sleep mode through a pin interrupt, or to completely shut off power to the system.

In this design the TPL5111 nano-power system timer is used to control both the boost converter mode and load switch, reducing the off-state current drawn from the battery to the order of nanoamps. The timer interval is selectable by an external resistor, and was chosen to be 100kohm || 100kΩ to give about 7 mins time intervals, or the can be selected as a function of the resistance of the potentiometer.

## 1.4 Boost Converter

![](RackMultipart20200602-4-1k91q4r_html_82bb0b8cce597410.png)

Fig 4. Simplified Schematic of the TPS61291

The TPS61291 was chosen to boost battery voltage from 3V to 3.3 V. This allows for the microcontroller to be powered via 2 AAA batteries. Additionally, the integrated bypass mode of the TPS61291 allows for maximum battery life by reducing current draw from the battery when 3.3 V is not needed.

## 1.5 Low-Leakage Load Switch

![](RackMultipart20200602-4-1k91q4r_html_3b31f04a346254a7.jpg)

Figure 5. TPS22860 Functional Block Diagram

In conjunction with a non-power system timer, a low-leakage load switch is used to shut off power to the CC1352r and sensors. The TPS22860 device was chosen for its rated leakage current of +- 20nA at 25C, enabling long battery life.

## 1.6 IFA Antenna

![](RackMultipart20200602-4-1k91q4r_html_445fb1f52f682d5b.jpg)

Fig 6. Implemented 2.4 GHz Inverted-F PCB Trace Antenna

In any low-power wireless embedded system, the wireless transmission of data will very likely represent the largest power cost. The TX power of the CC1352r is selectable from -20 to +5 dbm. Decreasing this power allows the battery life to be extended. By optimizing the antenna efficiency, the TX power can be minimized while still maintaining an acceptable range. For this device, an Inverted-F PCB trace antenna antenna (IFA) was simulated in HFSS and then measured in the enclosure and operating environment. A PCB trace antenna also has the benefit of having no cost, as the antenna is built into the PCB. Measurement results are discussed in section 3.5.

## 1.7 Power Methods

All boards are powered through some combination of 2 x AAA batteries, CR2032 coin-cell battery, 18650 Li-Ion battery or 2 x 5.55 mm barrel jack

#


#


# 2 System Design Theory and Considerations

![](RackMultipart20200602-4-1k91q4r_html_4ca71aa109db10a1.png)

Fig 7. Low-power block diagram

A battery powered sensor node will have two main states: on and asleep. In the off state, the battery is completely disconnected from the microcontroller and sensors by the TPS22780 switch being open. Additionally, the TPS61291 DC-DC Boost is operating in bypass mode. Overall, the off state current draw is in the nA range.

When the timing interval on the nano power system timer has ended, the TPS22860 switch is closed, connecting the battery to the microcontroller and sensors. The DC-DC Boost is also put into boost mode, bringing the voltage to 3.3V. When the microcontroller has finished its tasks of collecting and transmitting sensor data, a GPIO pin (Done) connected to the nano power timer is written high, opening the switch and bringing the system back to the off state.

## 2.1 Duty-Cycled Power Calculations

Our system uses a duty cycle (turning the device &quot;on&quot; for a percentage of a periodic time interval) in order to extend the battery life of our devices. We can calculate a battery life estimate by using the following equation:

![](RackMultipart20200602-4-1k91q4r_html_7a15027ad7f01a90.png)

where the derating factor is used to account for variations in the battery&#39;s capacity due to leakage current or the environment.

## 2.2 Firmware

Software for all Zigbee nodes was developed in Code Composer Studio (CCS). Nodes are a part of the HVAC cluster and include uint16 attributes for temperature, humidity and CO2. When data temperature and humidity reach the coordinator, the uint16 value is converted to a ℃ and %RH value through the following equation and sent via UART to the BeagleBone Black:

## 2.3 Zigbee Network

![](RackMultipart20200602-4-1k91q4r_html_69be9a0df3bcfc0e.png)

Figure 8. Typical Zigbee Mesh topology. White circles represent end

nodes, red circles represent routers, and the black circle

represents a coordinator

Our sensor network takes advantage of Texas Instruments Zigbee Stack (Z-Stack) application. ZigBee is a IEEE 802.15.4 based, low power, low data rate supporting wireless networking standard, typically useful for two-way communication between sensors and control systems. By implementing a zigbee mesh network, we can exploit favorable properties other network designs lack such as a self healing and low powered network.

Zigbee mesh networks consist of three main devices - end nodes, routers, and typically a single coordinator. Coordinators can create networks and add devices to the network once created. Since all the information from the end nodes get sent to the coordinator, the coordinator is connected to our gateway where the data can be collected on cloud devices.The routers main function is to relay information from the end node to the coordinator. They also have network creating capabilities but they are not used for our purposes. Finally end nodes are the hardware that sample data and send to routers.

## 2.4 Zigbee Gateway

![](RackMultipart20200602-4-1k91q4r_html_7ec4e0c5dc721fed.jpg)

Fig 9. OSI Model

The linux gateway is a BeagleBone Black running Ubuntu 18.04 LTS for armv7l.

The cloud server used is OSIsoft&#39;s PI Server. The gateway communicates to the server using Osisoft message format (OMF). Fledge is an open source framework focused for industrial IoT applications. Fledge is a suite of microservices that allow for rapid deployment of light-weight modules to extend the software&#39;s functionality. We chose this software because omf support in its builtin package.

The gateway communicates with the zigbee coordinator using UART protocol. Adafruit BeagleBoneBlack drivers and pySerial are installed. Using these two packages, the south plugin is written according to the plugin developer guide.

Once the data collected by fledge, the fledge-north-omf plugin would send the data to the cloud. We needed assistance gaining credentials to communicate with the server, but that was in the scope of winery IT and OSIsoft licensing.

##


## 2.5 Antenna Design

![](RackMultipart20200602-4-1k91q4r_html_2e97573b4df7803b.jpg)

Fig 10. S11: Simulated vs. Measured

#


#


#


# 3 Hardware Versions

To achieve high performance in a variety of implementation settings, multiple devices were created. The naming of these these devices is the following:

- MeshVines\_ZigbeeActor\_MeasurementParameter\_PowerInput&amp;mAh
  - MeshVines\_CoordinatorRouterEnd\_TempHumCO2\_WallBatteryxxxx
    - MeshVines\_RE\_THC\_WB1000
    - MeshVines\_RE\_TH\_WB220
    - MeshVines\_C\_W
    - MeshVines\_R\_TH\_WB\_5200

## 3.1 Hardware Overview

| Device Name - External (NEW) | Hardware Name-Internal Name (OLD) | Type | Enclosure (Polycase) | Battery | Sensing | Capacity |
| --- | --- | --- | --- | --- | --- | --- |
| MeshVines\_RE\_THC\_WB1000 | MeshVines V3 | Router/End | SN-29 | 2 x AAA | Temp, Hum, CO2 | 1000 mAh |
| MeshVines\_RE\_TH\_WB220 | MeshVines\_TempHum\_V1 | Router/End | SN-21 or SN-22 | CR2032 | Temp, Hum | 220 mAh |
| MeshVines\_C\_W | MeshVines\_BBB\_Coordinator\_Cape | Coordinator (cape for BBB) | ML-44F | None (Powered through BBB) | N/A | N/A |
| MeshVines\_R\_TH\_WB5200 | MeshVines\_Router\_Battery | Router | SN-29 | 2 x 3.7V Lithium-Ion | Temp, Hum | 5200 mAh |

###


### 3.1.1 MeshVines\_RE\_THC\_WB1000

![](RackMultipart20200602-4-1k91q4r_html_a826a8adefeeffaa.png)

Fig 11. MeshVines\_RE\_THC\_WB1000

MeshVines\_RE\_THC\_WB1000 is mainly used as an end node in the Zigbee mesh network and can measure temperature, humidity and CO2.

MeshVines\_RE\_THC\_WB1000 has the following features:

- 2 x AAA batteries
- Inverted-F 2.4 GHz PCB trace antenna
- Commission, Clear, and Reset buttons
- Power status LED
- Switch to select the input power supply
- 2 x 5.5 mm barrel connector for 5 V input
- HDC1080 for temperature and humidity measurement
- COZIR 5,000 ppm for CO2 measurement
- Low power architecture for maximizing battery life
- Polycase enclosure SN-29

###


### 3.1.2 MeshVines\_RE\_TH\_WB220

![](RackMultipart20200602-4-1k91q4r_html_bbcc2b65e79c8300.png)

Fig 12. MeshVines\_RE\_TH\_WB220

MeshVines\_RE\_TH\_WB220 is mainly used as an end node in the Zigbee mesh network, and can measure temperature and humidity.

MeshVines\_RE\_TH\_WB220 has the following features:

- CR2032 Battery
- Inverted-F 2.4 GHz PCB trace antenna
- Commission and Reset buttons
- Power status LED
- Switch to select the input power supply
- 2 x 5.5 mm barrel connector for 5 V input
- HDC1080 for temperature and humidity measurement
- Low power architecture for maximizing battery life
- Polycase enclosure SN-21 or SN-22

###


### 3.1.3 MeshVines\_C\_W

![](RackMultipart20200602-4-1k91q4r_html_3589972e81e0e15d.png)

Fig 13. MeshVines\_C\_W

MeshVines\_C\_W is used as the coordinator in the Zigbee mesh network, and is designed to fit into the header pins of a BeagleBone Black (BBB).

MeshVines\_C\_W has the following features:

- Header pins to fit onto BeagleBone Black
- uFL connector for 2.4 GHz antenna
- Commission, Clear and Reset buttons
- LED for commissioning countdown
- LED for indication of received packets

###


### 3.1.4 MeshVines\_R\_TH\_WB5200

![](RackMultipart20200602-4-1k91q4r_html_a4bee2d2ca0aa593.gif)

Fig 14. MeshVines\_R\_TH\_WB5200

In an industrial environment such as a winery, one cannot rely on a conveniently placed outlet to power a Zigbee router. Therefore, MeshVines\_R\_TH\_WB5200 was created to allow a router to be powered off battery for up to 2 months. If an uninterruptible power supply is used for the Zigbee coordinator, then the entire network can run independently of the building&#39;s infrastructure. In the event of a power outage or network disruption, the coordinator can buffer data locally until the power or network disruption is resolved.

MeshVines\_R\_TH\_WB5200 has the following features:

- 2 x 18650 battery holders in parallel
- 2 x 5.5 mm barrel connector for 5 V input
- Side mount PCB SMA connector for 2.4 GHz antenna
- Commission, Clear and Reset buttons
- Switch to select the input power supply
- Power indicator LED

# 4 Implementation Results and Characterization

The system was installed in 2 locations, the Jess S Jackson Sustainable Winery Building (Section 5.1) on the UC Davis campus and an apartment (Section 5.2) to collect data for approximately 1 week each.

## 4.1 Jess S Jackson Sustainable Winery Building Results

![](RackMultipart20200602-4-1k91q4r_html_165da12f2befa66a.jpg)

Fig 15. Jess S Jackson Sustainable Winery Building

This project was implemented in the Jess S Jackson Sustainable Winery Building on the UC Davis campus. From the UC Davis Viticulture and Enology website, &quot;The Jackson Sustainable Winery Building is designed to never drop below 50°F (10°C) or above 80°F (27°C ) even during the hot summers found in Davis. Temperature is controlled by efficient night air cooling in summer and warm day heating in winter. Windows near the peak of the slanted ceiling open automatically at night during the summer to allow natural circulation of the air through a fan that introduces the cool nighttime air near the floor. Hot or cold water can be circulated to heat or cool the floor slab of the building via tubes within the slab.&quot; In addition to its LEED platinum certification, this building houses many ongoing projects in sustainable design of wineries and is an important part of UC Davis being the most sustainable campus in the world (UI GreenMetric World University Ranking, 2016).

Data is collected from nodes and recorded into a csv at the coordinator to be processed by MATLAB later

### 4.1.1 Node Placement

![](RackMultipart20200602-4-1k91q4r_html_e8b77d9efb3f7f0d.gif)

![](RackMultipart20200602-4-1k91q4r_html_d090ce2d88cdc166.gif)

Fig 16. Jess S Jackson Sustainable Winery Building Node Placement

### 4.1.2 Recorded Data

![](RackMultipart20200602-4-1k91q4r_html_edf194d3a887d20d.jpg)

Fig 17. Jess S Jackson Sustainable Winery Building Recorded Temperature

![](RackMultipart20200602-4-1k91q4r_html_ad5d314b6b7caba4.jpg)

Fig 18. Jess S Jackson Sustainable Winery Building Recorded Humidity

Between May 16 and May 17, node 14 is added. Additionally this node contains a software update to take 3 samples and send the most recent sample. This correlated to a smoother temperature and humidity curve.

![](RackMultipart20200602-4-1k91q4r_html_385ac30dec6a30d.jpg)

Fig 19. Jess S Jackson Sustainable Winery Building Recorded RSSI

Received Signal Strength Intensity (RSSI) was also recorded and is measured in dBm.

##


## 4.2 Apartment Building Results

Data is collected from end nodes and sent to an OSIsoft database via Fledge.

### 4.2.1 Node Placement

![](RackMultipart20200602-4-1k91q4r_html_519f78f4f86f5e99.gif)

Fig 20. Apartment Node Placement

### 4.2.2 Recorded Data

![](RackMultipart20200602-4-1k91q4r_html_688537a012242a6e.jpg)

Fig 21. Apartment Recorded Temperature and Humidity

Node 8 (brown) was placed outside for reference and reflects diurnal periodicity. Additionally, node 1, which is placed in the kitchen, shows higher temperature for certain parts of the day.

## 4.3 Power Consumption

![](RackMultipart20200602-4-1k91q4r_html_aa9e78802c969dca.jpg)

Fig 22. Measured Current on MeshVines\_RE\_TH\_WB220

Our sensor end nodes save power by using a duty cycle to control how long and how often the devices are powered on for. Accurate analysis of the power consumption of our end nodes is essential to maximizing the battery life of our devices. To measure the power consumption of our devices, we used the Otii Arc® to measure the current draw by our end nodes while they are collecting and transmitting data (the &quot;on-state&quot;) and while the device is not active (the &quot;off-state&quot;).

### 4.3.1 On-State Power Characterization

The on-state of an end node is when the device sampling data from the onboard sensors and transmitting this data to a router node, we found the average on-state current of MeshVines\_RE\_TH\_WB220 to be 1 mA. The device is active in this state for 10 seconds.

### 4.3.2 Off-State Power Characterization

When a device is not actively sampling, MeshVines\_RE\_TH\_WB220 draws 220 nA.

### 4.3.3 Estimated Battery Life Calculations

Based on the on-state and off-state current, powering the device by a common 2032 coin cell battery, and given a sampling duration of every 15 minutes, the expected battery life of an end node device is 23 months.

## 4.4 Verification of Mesh Network

![](RackMultipart20200602-4-1k91q4r_html_5e52f3c577a45bad.png)

Fig 23. Data Path for Verification of Mesh Network

The Zigbee network was verified as a mesh by forcing data through 2 paths and observing the RSSI on the coordinator. By powering the router on the off, the path is also switched, demonstrating the self-healing nature of a Zigbee mesh network.

## 4.5 Cost Analysis

| **Device** | **Cost per unit** | **Total cost** |
| --- | --- | --- |
| MeshVines\_RE\_THC\_WB1000
 | $155.53 (with CO2 sensor) $46.53 (without CO2 sensor) |
 |
| MeshVines\_C\_TH\_W | $25.69 |
 |
| MeshVines\_R\_TH\_WB5200 |
 |
 |
| MeshVines\_RE\_TH\_WB220 |
 |
 |

#


# 5 Conclusion

This project demonstrates the scalability of a large sensor network through low power design, a mesh topology, low cost and consideration of antenna design. By using Fledge to manage data into the cloud, the system addresses common industrial IoT security concerns.

# 6 Team Members

# ![](RackMultipart20200602-4-1k91q4r_html_ec3fe7a1e2fd8005.jpg)

# 7 Acknowledgements

The support of this project was made available by Opus One Winery and Texas Instruments and was performed in collaboration with the Robert Mondavi Institute for Wine and Food Science.

![](RackMultipart20200602-4-1k91q4r_html_70931c7451290bb4.png) ![](RackMultipart20200602-4-1k91q4r_html_5535f1e03eb6192c.png)

#


# 8 References

**\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_**

![](RackMultipart20200602-4-1k91q4r_html_4b245d8aa650c39e.jpg)MeshVines: Zigbee Temperature, Humidity and CO2 Wireless Sensor Network 22
