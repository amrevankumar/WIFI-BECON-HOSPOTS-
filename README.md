# WIFI-BECON-HOSPOTS-
# Sector 2: ESP8266 Multiple SSID Beacon Broadcast

## 1. Project Overview

This project demonstrates the operation of Wi-Fi beacon frames using an ESP8266 NodeMCU microcontroller.

The program broadcasts multiple predefined Wi-Fi network names (SSIDs) by transmitting beacon frames over selected Wi-Fi channels. These network names may appear in the Wi-Fi scanning interface of nearby devices.

The project is based on the ESP8266 Wi-Fi functionality and the beacon frame transmission implementation originally developed by Stefan Kremser.

**Project Name:** ESP8266 Wi-Fi Security Awareness System

**Sector:** Sector 2 — Multiple SSID Beacon Broadcast

**Hardware:** ESP8266 NodeMCU

**Programming Language:** C++

**Development Environment:** Arduino IDE

**Category:** Wireless Network Security / IoT / Cybersecurity Awareness

---

## 2. Objectives

- Understand the structure and purpose of IEEE 802.11 Wi-Fi beacon frames.
- Study how Wi-Fi networks advertise their SSIDs.
- Explore ESP8266 wireless communication capabilities.
- Understand Wi-Fi channel selection and MAC address concepts.
- Demonstrate the security implications of misleading wireless network advertisements.
- Establish a foundation for future Wi-Fi security monitoring and awareness modules.

---

## 3. Hardware and Software Requirements

### Hardware Requirements

| Component | Purpose |
|---|---|
| ESP8266 NodeMCU | Wireless beacon frame demonstration |
| USB cable | Programming and power supply |
| Laptop | Development and debugging |
| Smartphone | Authorized Wi-Fi scanning |
| Wi-Fi adapter | Optional wireless analysis |

### Software Requirements

| Software | Purpose |
|---|---|
| Arduino IDE | Firmware development |
| ESP8266 Arduino Core | ESP8266 programming support |
| Serial Monitor | Debugging and monitoring |
| Wi-Fi analyzer | Observing advertised network names |
| Wireshark | Authorized wireless traffic analysis |

---

## 4. Working Principle

The ESP8266 uses beacon frames to advertise wireless network information.

A beacon frame is a management frame in IEEE 802.11 wireless networking. It typically contains:

- SSID (network name)
- BSSID (access point identifier)
- Supported data rates
- Wireless channel information
- Network capability information
- Beacon interval

The program prepares a beacon frame and modifies selected fields to represent different network names.

The ESP8266 then transmits these frames using its wireless interface.

### System Workflow

```text
        ESP8266 NodeMCU
               |
               v
      Initialize Wi-Fi
               |
               v
      Load SSID List
               |
               v
     Select Wi-Fi Channel
               |
               v
    Prepare Beacon Frame
               |
               v
    Insert SSID and MAC Data
               |
               v
    Transmit Beacon Frames
               |
               v
    Nearby Wi-Fi Scanners
               |
               v
  Observe Advertised Network Names
```

---

## 5. Code Explanation

### 5.1 Wi-Fi Channel Configuration

```cpp
const uint8_t channels[] = {1, 6, 11};
```

This array defines the Wi-Fi channels used by the program.

The ESP8266 switches between the configured channels while transmitting beacon frames.

Channels 1, 6, and 11 are commonly used in 2.4 GHz Wi-Fi environments.

### 5.2 SSID Configuration

```cpp
const char ssids[] PROGMEM = {
  "Mom Use This One\n"
  "Abraham Linksys\n"
  "Benjamin FrankLAN\n"
};
```

This section stores the predefined network names in program memory.

The `PROGMEM` keyword helps store constant data in flash memory rather than consuming unnecessary RAM.

Each SSID is separated using a newline character.

### 5.3 ESP8266 Wi-Fi Library

```cpp
#include <ESP8266WiFi.h>
```

This library provides Wi-Fi functionality for the ESP8266.

The code also uses lower-level ESP8266 SDK functions to access wireless packet transmission functionality.

### 5.4 Beacon Frame Structure

```cpp
uint8_t beaconPacket[109] = {
  // Beacon frame information
};
```

This array represents the structure of a beacon frame.

It contains:

| Field | Description |
|---|---|
| Frame Control | Identifies the frame as a management beacon |
| Destination | Broadcast address |
| Source | Transmitter address |
| BSSID | Wireless network identifier |
| Timestamp | Beacon timing information |
| Beacon Interval | Time between beacon announcements |
| SSID Information | Advertised network name |
| Supported Rates | Supported wireless data rates |
| Channel Information | Wireless channel |
| Capability Information | Network capability details |

### 5.5 Channel Switching

```cpp
void nextChannel() {
  // Channel selection logic
}
```

This function changes the ESP8266's current wireless channel based on the configured channel array.

The purpose is to demonstrate how wireless communication operates across different channels.

### 5.6 MAC Address Configuration

```cpp
void randomMac() {
  for (int i = 0; i < 6; i++) {
    macAddr[i] = random(256);
  }
}
```

This function generates a randomized six-byte address used in the beacon frame.

A MAC address identifies a wireless interface at the link layer.

### 5.7 Setup Function

```cpp
void setup() {
  Serial.begin(115200);

  WiFi.mode(WIFI_OFF);
  wifi_set_opmode(STATION_MODE);

  wifi_set_channel(channels[0]);
}
```

The `setup()` function executes once when the ESP8266 starts.

Its responsibilities include:

1. Initializing the Serial Monitor.
2. Initializing variables.
3. Configuring the wireless interface.
4. Selecting the initial Wi-Fi channel.
5. Displaying the configured SSID list.

### 5.8 Main Loop

```cpp
void loop() {
  currentTime = millis();

  // Main program execution
}
```

The `loop()` function executes continuously.

The program periodically processes the SSID list, updates beacon frame information, and maintains packet transmission statistics.

### 5.9 Packet Rate Monitoring

```cpp
Serial.print("Packets/s: ");
Serial.println(packetCounter);
```

This section displays a packet counter through the Serial Monitor.

It helps observe the program's activity during an authorized laboratory demonstration.

**Note:** The displayed value represents successful calls reported by the transmission function, not necessarily the number of frames successfully received by nearby devices.

---

## 6. Implementation Procedure

### Step 1: Install Arduino IDE

Download and install Arduino IDE from:

https://www.arduino.cc/en/software

### Step 2: Install ESP8266 Board Support

Add the ESP8266 board package through the Arduino IDE Boards Manager.

Select the appropriate ESP8266 NodeMCU board.

### Step 3: Connect the ESP8266

Connect the ESP8266 to the laptop using a USB cable.

Select the appropriate COM port.

### Step 4: Load the Source Code

Open the provided `.ino` file in Arduino IDE.

Review the configuration settings and ensure the device is being used in an authorized laboratory environment.

### Step 5: Compile the Program

Click Verify to compile the program.

Resolve any compilation errors before proceeding.

### Step 6: Upload the Firmware

Upload the compiled firmware to the ESP8266.

Wait until the upload completes successfully.

### Step 7: Open the Serial Monitor

Set the baud rate to:

`115200`

Observe the initialization messages and packet counter.

### Step 8: Observe Wi-Fi Network Advertisements

Using an authorized Wi-Fi scanning device, observe the network names being advertised.

Document the observations for the project report.

---

## 7. Expected Output

### Serial Monitor

The program prints initialization information and a packet counter.

Example:

```text
SSIDs:
Mom Use This One
Abraham Linksys
Benjamin FrankLAN
Martin Router King

Started \o/

Packets/s: ...
Packets/s: ...
Packets/s: ...
```

The exact packet count depends on the device, firmware, and execution conditions.

### Wi-Fi Scanner

A Wi-Fi scanner may display some of the configured network names.

The results can vary depending on:

- Distance from the ESP8266
- Wi-Fi channel
- Wireless interference
- Device scanning behavior
- Beacon frame compatibility

---

## 8. Limitations

1. The program advertises SSIDs but does not create normal access points for clients to connect to.
2. The ESP8266 has limited memory and processing resources.
3. The displayed packet counter does not confirm reception by nearby devices.
4. Wi-Fi scanner applications may filter or suppress repeated network advertisements.
5. The code uses low-level SDK functions that may depend on the ESP8266 Arduino Core version.
6. The code does not implement a captive portal, internet connection, or client data collection.

---

## 9. Security and Ethical Considerations

This project is intended for controlled cybersecurity education and authorized wireless testing.

- Perform demonstrations only in an authorized laboratory.
- Do not impersonate real public Wi-Fi networks.
- Do not interfere with nearby wireless networks.
- Do not attempt to collect credentials or private information.
- Do not attempt to access connected devices without authorization.
- Stop the demonstration if it affects other wireless users.

The project should be used to understand wireless security risks and improve awareness of suspicious Wi-Fi advertisements.

---

## 10. Future Development

The following modules can be developed in subsequent project sectors:

| Sector | Proposed Module |
|---|---|
| Sector 1 | ESP8266 Wi-Fi initialization and configuration |
| Sector 2 | Multiple SSID beacon broadcast demonstration |
| Sector 3 | Controlled Wi-Fi access point and client monitoring |
| Sector 4 | Captive portal security awareness demonstration |
| Sector 5 | Wi-Fi connection event logging |
| Sector 6 | Security awareness dashboard |
| Sector 7 | Defensive wireless security analysis |

---

## 11. Conclusion

Sector 2 demonstrates the fundamental operation of Wi-Fi beacon frames and SSID advertisements using an ESP8266 NodeMCU.

The project provides practical knowledge of wireless management frames, channel selection, MAC address concepts, and Wi-Fi network discovery.

This sector establishes the foundation for the next stages of the ESP8266 Wi-Fi Security Awareness System, where controlled access points, client monitoring, and defensive security demonstrations can be explored.

---

## 12. References

- ESP8266 Arduino Core Documentation: https://arduino-esp8266.readthedocs.io/
- Espressif ESP8266 Resources: https://www.espressif.com/en/products/socs/esp8266ex/resources/
- IEEE 802.11 Wireless LAN Standards
- Original project reference: https://github.com/spacehuhn
