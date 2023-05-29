---
description: TBD
title: TBD
keywords:
- Grove
image: TBD
slug: xiao can
last_update:
  date: 5/23/2023
  author: Stephen Lo
---


<!-- ![](https://files.seeedstudio.com/wiki/Grove-VOC_and_eCO2_Gas_Sensor-SGP30/img/IMG_0012a.jpg) -->
  <p style={{textAlign: 'center'}}><img src="https://raw.githubusercontent.com/Longan-Labs/CAN_DEV_XIAO_RES/main/images/main.jpg" alt="pir" width={600} height="auto" /></p>

The Xiao CAN Bus Expansion Board is specifically designed to work with the Seeed Studio Xiao development board, providing an easy and convenient way to add CAN bus communication functionality to your projects. CAN bus (Controller Area Network) is a widely used communication protocol in automotive, industrial, and other embedded systems, allowing for reliable and robust data exchange between different nodes.

The integration of the MCP2515 controller and SN65HVD230 transceiver chips on the expansion board ensures seamless and efficient communication over the CAN bus. The MCP2515 controller handles the protocol management, message filtering, and error handling, while the SN65HVD230 transceiver converts the digital signals from the controller into the differential signals required for CAN bus communication.

With the Xiao CAN Bus Expansion Board, you can leverage the power of the Seeed Studio Xiao development board and its extensive ecosystem to create projects that require CAN bus communication. Whether you're working on automotive applications, industrial control systems, robotics projects, or IoT devices, this expansion board provides a reliable and compact solution for integrating CAN bus capabilities into your designs.

The expansion board features a user-friendly terminal connection, allowing you to easily connect the CANH and CANL lines to the CAN bus network. The compact design of the board ensures compatibility with various project enclosures and facilitates seamless integration into your existing setups.

By utilizing the Xiao CAN Bus Expansion Board, you can take advantage of the robustness, reliability, and scalability of the CAN bus protocol, enabling efficient data exchange, system control, and interconnectivity in your projects.

<p style={{textAlign: 'center'}}><a href="https://www.seeedstudio.com/-Grove-VOC-and-eCO2-Gas-Sensor-(SGP30)-p-3071.html" target="_blank"><img src="https://files.seeedstudio.com/wiki/Seeed-WiKi/docs/images/300px-Get_One_Now_Banner-ragular.png" /></a></p>

## Features

- Compatibility: Designed to work seamlessly with the Seeed Studio Xiao development board.
- MCP2515 Controller: The onboard MCP2515 chip provides reliable control and handling of the CAN bus communication.
- SN65HVD230 Transceiver: The integrated SN65HVD230 chip ensures accurate signal conversion and robust communication over the CAN bus.
- Terminal Connection: The CANH and CANL lines are conveniently accessible through a 3-pin terminal, allowing easy connection to the CAN bus.
- Compact Design: The expansion board has been designed with a compact form factor, making it suitable for various applications.

## Specification

- Compatibility: Seeed Studio Xiao development board.
- Communication Interface: CAN bus (Controller Area Network).
- CAN Transceiver: SN65HVD230.
- CAN Controller: MCP2515.
- Terminal Connection: 2-pin terminal for CANH and CANL lines.

## Applications

The Xiao CAN Bus Expansion Board can be utilized in various projects that require CAN bus communication. Here are a few application ideas to inspire you:

- Automotive Projects: Connect the expansion board to the Xiao and build automotive applications that require CAN bus communication, such as vehicle diagnostics or data logging.
- Industrial Control Systems: Utilize the CAN bus capabilities to interface with industrial devices and systems, enabling efficient data exchange and control.
- Robotics: Incorporate the expansion board into your robotic projects to enable communication between different robotic modules and components.
- IoT Applications: Integrate the expansion board with IoT devices to facilitate communication and data exchange over the CAN bus protocol.

Please refer to the Xiao CAN Bus Expansion Board datasheet and examples for detailed usage instructions and code samples.

## Hardware Overview

<!-- ![](https://raw.githubusercontent.com/Longan-Labs/NFC_ST25DV_RES/main/images/pinmap.png) -->
  <p style={{textAlign: 'center'}}><img src="https://raw.githubusercontent.com/Longan-Labs/CAN_DEV_XIAO_RES/main/images/hw.jpg" alt="pir" width={600} height="auto" /></p>

1. CANH
2. GND
3. CANL
4. LED Indicators for RX/TX
5. SN65NVD230
6. MCP2515

## Getting Started

#### Hardware
This product does not include the Xiao module, so you will need to purchase a separate Xiao module. In this example, we use the XIAO ESP32C3 for demonstration purposes, but other versions of the Xiao module will work similarly. The hardware connection is straightforward - simply insert the Xiao module into the expansion board.

#### Software

- **Step 1.** Download the [CAN Bus Library](https://github.com/Longan-Labs/Aruino_CAN_BUS_MCP2515) from Github.

- **Step 2.** Refer to [How to install library](https://wiki.seeedstudio.com/How_to_install_Arduino_Library) to install library for Arduino.

- **Step 3.** After downloading and installing the library correctly, you can find an example program named send.ino in the examples folder. This program is designed for the D7S module.

```Arduino
#include <mcp_can.h>
#include <SPI.h>

/* Please modify SPI_CS_PIN to adapt to different baords.

   CANBed V1        - 17
   CANBed M0        - 3
   CAN Bus Shield   - 9
   CANBed 2040      - 9
   CANBed Dual      - 9
   OBD-2G Dev Kit   - 9
   OBD-II GPS Kit   - 9
   Hud Dev Kit      - 9
*/

#define SPI_CS_PIN  9 

MCP_CAN CAN(SPI_CS_PIN);                                    // Set CS pin

void setup()
{
    Serial.begin(115200);
    while(!Serial);
    
    // below code need for OBD-II GPS Dev Kit Atemga32U4 version
    // pinMode(A3, OUTPUT);
    // digitalWrite(A3, HIGH);
    
    // below code need for OBD-II GPS Dev Kit RP2040 version
    // pinMode(12, OUTPUT);
    // digitalWrite(12, HIGH);
    
    while (CAN_OK != CAN.begin(CAN_500KBPS))    // init can bus : baudrate = 500k
    {
        Serial.println("CAN BUS FAIL!");
        delay(100);
    }
    Serial.println("CAN BUS OK!");
}

unsigned char stmp[8] = {0, 1, 2, 3, 4, 5, 6, 7};
void loop()
{
    CAN.sendMsgBuf(0x00, 0, 8, stmp);
    delay(100);                       // send data per 100ms
}

// END FILE
```

- **Step 4.** Upload the demo. If you do not know how to upload the code, please check [How to upload code](https://wiki.seeedstudio.com/Upload_Code/).

- **Step 5.** After a successful code upload, you will notice that the RX and TX LEDs light up, indicating that the CAN bus is actively transmitting data. If your CAN bus is connected to other devices, these LEDs will blink instead of remaining constantly lit.



## Arduino Library

We provide an [Arduino library for the MCP2515 board](https://github.com/Longan-Labs/Aruino_CAN_BUS_MCP2515). 

The library includes several examples, including:

* ***OBDII-PIDs*** -  retrieve data from the OBD-II interface
* ***send*** - send a frame to the CAN bus
* ***recv*** - receive a frame from the CAN bus
* ***set_mask_filter_recv*** - receive a frame from the CAN bus with mask and filter settings

## ***APIs***
--------------------------

### 1. Set the Baud rate

This function is used to initialize the baud rate of the CAN Bus system.

The available baud rates are listed as follows:

	#define CAN_5KBPS    1
	#define CAN_10KBPS   2
	#define CAN_20KBPS   3
	#define CAN_25KBPS   4
	#define CAN_31K25BPS 5
	#define CAN_33KBPS   6
	#define CAN_40KBPS   7
	#define CAN_50KBPS   8
	#define CAN_80KBPS   9
	#define CAN_83K3BPS  10
	#define CAN_95KBPS   11
	#define CAN_100KBPS  12
	#define CAN_125KBPS  13
	#define CAN_200KBPS  14
	#define CAN_250KBPS  15
	#define CAN_500KBPS  16
	#define CAN_666kbps  17
	#define CAN_1000KBPS 18

### 2. Set Receive Mask and Filter

The controller chip has 2 receive mask registers and 5 filter registers that can be used to ensure that data is received from the targeted device. These registers are particularly useful in large networks with many nodes. We have provided two functions that allow you to utilize these mask and filter registers.

**Mask:**

	init_Mask(unsigned char num, unsigned char ext, unsigned char ulData);

**Filter:**

	init_Filt(unsigned char num, unsigned char ext, unsigned char ulData);

- **num** represents which register to use. You can fill 0 or 1 for mask and 0 to 5 for filter.
- **ext** represents the status of the frame. 0 means it's a mask or filter for a standard frame. 1 means it's for a extended frame.
- **ulData** represents the content of the mask of filter.

###3. Check Receive
The MCP2515 controller chip has the ability to operate in either a polled mode or an interrupt mode. In polled mode, the software regularly checks for a received frame. In interrupt mode, additional pins can be used to signal that a frame has been received or transmit has completed. This allows for more efficient use of resources as the processor does not need to constantly check for incoming data.

This function is used to check if there are any received frames waiting in the receive buffer. If there are, the function will return true, otherwise it will return false. You can use this function in a loop to continuously check for received frames. 

    INT8U MCP_CAN::checkReceive(void);

###4. Get CAN ID
You can use the following function to get the length of the data received from the "send" node.

    INT32U MCP_CAN::getCanId(void)

###5. Send a frame

    CAN.sendMsgBuf(INT8U id, INT8U ext, INT8U len, data_buf);

This function is used to send data onto the CAN Bus. The parameters are as follows:

* **id** - The ID of can frame.
* **ext** - A boolean value representing the status of the frame. '0' means standard frame. '1' means extended frame.
* **len** - The length of the frame.
* **data_buf** - The content of the message.

For example, In the 'send' example, we have:

    unsigned char stmp[8] = {0, 1, 2, 3, 4, 5, 6, 7};
    CAN.sendMsgBuf(0x00, 0, 8, stmp); //send out the message 'stmp' to the bus and tell other devices this is a standard frame from 0x00.

###6. Receive a frame

The following function is used to receive data on the 'receive' node:

    CAN.readMsgBuf(unsigned char len, unsigned char buf);
    
In conditions that masks and filters have been set. This function can only get frames that meet the requirements of masks and filters.

* **len** represents the data length.
* **buf** is where you store the data.

## Schematic Online Viewer

<div className="altium-ecad-viewer" data-project-src="https://github.com/Longan-Labs/D7S_SENSOR_RES/raw/main/D7S%20Vibration%20Sensor.zip" style={{borderRadius: '0px 0px 4px 4px', height: 500, borderStyle: 'solid', borderWidth: 1, borderColor: 'rgb(241, 241, 241)', overflow: 'hidden', maxWidth: 1280, maxHeight: 700, boxSizing: 'border-box'}}>
</div>

## FAQ

Q: What is the maximum baud rate supported by the Xiao CAN Bus Expansion Board?

A: The maximum baud rate supported by the MCP2515 controller on the expansion board is 1 Mbps. Please ensure that the baud rate settings of your CAN bus network are compatible with this limitation.

Q: Can I use multiple Xiao CAN Bus Expansion Boards in the same CAN bus network?

A: Yes, you can use multiple expansion boards in the same CAN bus network. Each expansion board should have a unique node ID assigned to it to ensure proper communication and avoid conflicts on the bus.

Q: Can I use the Xiao CAN Bus Expansion Board with other microcontrollers or development boards?

A: The Xiao CAN Bus Expansion Board is specifically designed to work with the Seeed Studio Xiao development board. However, with proper pin mapping and configuration, it may be possible to use it with other microcontrollers or development boards that support the necessary CAN bus communication protocols.

Q: Are there any limitations on the maximum cable length for the CAN bus connection?

A: The maximum cable length for the CAN bus connection depends on factors such as the baud rate, cable quality, and electromagnetic interference. In general, for lower baud rates, longer cable lengths (up to several hundred meters) can be supported. However, for higher baud rates, it is recommended to keep the cable length shorter (within a few meters) to maintain reliable communication.

Q: How can I troubleshoot CAN bus communication issues?

A: If you encounter any issues with CAN bus communication, you can follow these steps for troubleshooting:

- Verify the physical connections of the CAN bus network, ensuring correct wiring and termination.
- Check the baud rate settings and ensure they match on all devices connected to the CAN bus.
- Monitor the CAN bus traffic using a CAN bus analyzer or terminal software to identify any errors or issues in the transmitted messages.
- Double-check the program code for proper initialization and configuration of the MCP2515 controller.
- Ensure that the power supply to the Xiao development board and the CAN bus network is stable and within the specified voltage range.
- If you have any other questions or issues not covered in this FAQ section, please feel free to contact our technical support team for further assistance.

## Resources

- **[Zip]** [Eagle file](https://github.com/stephen1874/CAN_DEV_XIAO_RES/raw/main/CAN_DEV_XIAO.zip)
- **[PDF]** [Datasheet - MCP2515](https://www.mouser.com/datasheet/2/268/MCP2515-Stand-Alone-CAN-Controller-with-SPI-200018-708845.pdf)
- **[PDF]** [Datasheet - SN65HVD230](https://www.mouser.com/datasheet/2/268/20001667G-1115479.pdf)
- **[GITHUB]** [MCP_CAN Library](https://github.com/Longan-Labs/Aruino_CAN_BUS_MCP2515)

## Tech Support
If you have any technical issue.  submit the issue into our [forum](https://forum.seeedstudio.com/).