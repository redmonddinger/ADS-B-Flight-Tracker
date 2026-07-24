# ADS-B Aircraft Tracking Station

I built an ADS-B aircraft tracking station using a Raspberry Pi 5 and an RTL-SDR receiver to monitor live aircraft transmissions.

The system receives 1090 MHz ADS-B signals from nearby aircraft, decodes them with readsb, and displays real-time flight information through the tar1090 web interface.

This project gave me hands-on experience with software defined radio (SDR), Linux, RF communications, networking, and integrating hardware and software into a working system.

## Project Overview

For this project, I used a Raspberry Pi 5 and an RTL-SDR receiver to capture ADS-B transmissions broadcast by nearby aircraft at 1090 MHz. The signals are decoded with readsb and displayed through the tar1090 web interface, where I can view aircraft positions, altitude, speed, heading, and identification information in real time.

My goal was to learn more about software defined radio, Linux configuration, and RF communications. Throughout the project, I configured the software, verified the hardware, troubleshot connection issues, and got everything working together as a functional aircraft tracking station.

## Skills Demonstrated

- Raspberry Pi
- Linux
- Software Defined Radio (SDR)
- RF Communications
- TCP/IP Networking
- System Integration
- Hardware Troubleshooting
- Embedded Linux
- System Configuration
- Network Configuration
- Technical Documentation

## Hardware

| Component | Purpose |
|-----------|---------|
| Raspberry Pi 5 | Runs Raspberry Pi OS, readsb, and the tar1090 web interface |
| Nooelec NESDR Smart v5 | Receives 1090 MHz ADS-B transmissions |
| MicroSD Card | Stores Raspberry Pi OS |
| Power Supply | Powers the Raspberry Pi |
| 1090 MHz Antenna | Receives aircraft signals |

## Hardware Setup

<p align="center">
  <img src="images/159C1981-CAEF-4537-A12C-4DF9BD475E3C.png" alt="Completed ADS-B receiver setup" width="700">
</p>

## Software

- readsb
- tar1090
- raspberry pi OS

### Operating System

- Raspberry Pi OS (64-bit)

### Packages

- readsb
- tar1090
- rtl-sdr

### Configuration

Verified RTL-SDR detection using rtl_test

Confirmed the readsb service was active

Verified aircraft reception through the tar1090 web interface

Accessed the receiver remotely using the Raspberry Pi IP address

Confirmed tar1090 web interface was reachable

Verified automatic startup after reboot

## System Design

```text
+-----------+
| Aircraft  |
+-----------+
      │
1090 MHz RF
      ▼
+-----------+
| Antenna   |
+-----------+
      │
      ▼
+-----------+
| RTL-SDR   |
+-----------+
      │ USB
      ▼
+--------------+
| Raspberry Pi |
+--------------+
      │
      ▼
+--------------+
|    readsb    |
+--------------+
      │ HTTP
      ▼
+--------------+
|   tar1090    |
+--------------+
      │
      ▼
+--------------+
| Web Browser  |
+--------------+
```

The way the system works is pretty straightforward. Aircraft continuously broadcast ADS-B messages on 1090 MHz, and the antenna picks up those signals. The RTL-SDR receives the RF data and sends it to the Raspberry Pi over USB, where readsb decodes the messages. Tar1090 then displays that information in a web browser so I can view nearby aircraft in real time from any device on my local network.

## Build Guide

### 1. Install Raspberry Pi OS

I started by flashing the latest 64-bit version of Raspberry Pi OS to a microSD card using Raspberry Pi Imager. After installing the card in the Raspberry Pi, I completed the initial setup and connected it to my network.

---

### 2. Update the Raspberry Pi

Before installing anything else, I updated the operating system and installed Git.

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install git
```

---

### 3. Connect the RTL-SDR

Next, I connected the Nooelec NESDR Smart v5 to the Raspberry Pi and attached the 1090 MHz antenna. To make sure the SDR was recognized correctly, I ran:

```bash
lsusb
```

I verified that the RTL2838-based SDR device appeared in the list before moving on.

---

### 4. Install and Configure readsb and tar1090

After confirming the hardware was working, I installed readsb to decode ADS-B messages and tar1090 to display the aircraft data through a web interface.

Once everything was installed, I verified that the readsb service was running.

```bash
sudo systemctl status readsb
```

---

### 5. Verify Aircraft Reception

With the software running, I opened the tar1090 interface in my browser.

```
http://<RaspberryPi-IP>/tar1090
```

Once nearby aircraft started appearing on the map, I knew the system was successfully receiving and decoding ADS-B transmissions.

---

### 6. Access the System from Another Device

To make sure everything was working across my local network, I found the Raspberry Pi's IP address.

```bash
hostname -I
```

Then, from another device connected to the same Wi-Fi network, I opened:

```
http://<RaspberryPi-IP>/tar1090
```

This let me access the same live aircraft map from another computer without needing to connect directly to the Raspberry Pi.

## Results

After getting everything running, I was able to receive and decode live ADS-B transmissions from aircraft around the Portland area. The screenshot below show the receiver tracking nearby aircraft and displaying their position, altitude, speed, heading, and aircraft information in real time.

<p align="center">
  <img src="images/IMG_1175.jpeg" alt="Live aircraft map in tar1090" width="48%">
</p>

During testing, the system tracked five aircraft at the same time and displayed real-time flight information through the tar1090 web interface.

| Callsign | Aircraft | Airline | Altitude (ft) | Speed (kt) |
|----------|----------|---------|--------------:|-----------:|
| SKW3112 | Embraer ERJ-170 | SkyWest | 16,725 | 351 |
| ASA1394 | Boeing 737-900 | Alaska Airlines | 14,225 | 340 |
| QXE2399 | Embraer E175 | Horizon Air | 12,300 | 328 |
| FFT4499 | Airbus A320 | Frontier Airlines | 5,825 | 218 |
| SWA949 | Boeing 737-700 | Southwest Airlines | 4,950 | 259 |

## Troubleshooting

Here are a few things I checked while getting the system up and running:

| Issue | Solution |
|------|----------|
| RTL-SDR wasn't detected | Verified the USB connection and confirmed the device appeared with `lsusb`. |
| No aircraft showing in tar1090 | Checked that the antenna was connected and that the `readsb` service was running. |

## Future Improvements

- Install an outdoor 1090 MHz antenna
- Add a low-noise amplifier (LNA)
- Increase reception range
- Feed data to FlightAware
- Log aircraft data to a database
- Build a custom enclosure
- Design a custom PCB for SDR power filtering

## License

This project is licensed under the MIT License. See the `LICENSE` file for more information.
