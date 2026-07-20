# ADS-B-Flight-Tracker
Raspberry Pi ADS-B receiver using an RTL-SDR to monitor live aircraft transmissions.

The system receives 1090 MHz ADS-B broadcasts from nearby aircraft, decodes them using dump1090-fa, and displays real-time aircraft positions and flight information through a browser-based interface.

This project demonstrates RF fundamentals, Software Defined Radio (SDR), Linux system administration, networking, and hardware/software integration.

## Project Overview

This project uses a Raspberry Pi 5 and an RTL-SDR receiver to capture Automatic Dependent Surveillance–Broadcast (ADS-B) transmissions from nearby aircraft operating at 1090 MHz. The received signals are decoded using dump1090-fa and served through a browser-based interface, allowing aircraft positions, altitude, speed, and identification information to be monitored in real time.

The goal of this project was to gain hands-on experience with software defined radio, Linux system configuration, RF communications, and integrating hardware and software into a functional monitoring system.

## Skills Demonstrated

- Raspberry Pi
- Linux
- Software Defined Radio (SDR)
- RF Communications
- TCP/IP Networking
- System Integration
- Command Line
- Hardware Troubleshooting

## Hardware

| Component | Purpose |
|-----------|---------|
| Raspberry Pi 5 | Runs Raspberry Pi OS, dump1090-fa, and the SkyAware web interface |
| Nooelec NESDR Smart v5 | Receives 1090 MHz ADS-B transmissions |
| MicroSD Card | Stores Raspberry Pi OS |
| Power Supply | Powers the Raspberry Pi |
| USB Extension (optional) | Reduces RF interference |
| 1090 MHz Antenna | Receives aircraft signals |

## Software

- rtl-sdr

### Operating System

- Raspberry Pi OS (64-bit)

### Packages

- dump1090-fa
- lighttpd
- git

### Installation

```bash
sudo apt update
sudo apt upgrade
sudo apt install git
```
wget https://flightaware.com/adsb/piaware/files/packages/pool/bookworm/piaware-repository_11.0_all.deb
...

### Configuration

Verified RTL-SDR detection using rtl_test

Confirmed dump1090-fa service was active

Verified aircraft reception through the SkyAware web interface

Accessed the receiver remotely using the Raspberry Pi IP address

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
| dump1090-fa  |
+--------------+
      │ HTTP
      ▼
+--------------+
| SkyAware UI  |
+--------------+
      │
      ▼
+--------------+
| Web Browser  |
+--------------+
```
Aircraft continuously broadcast ADS-B messages at 1090 MHz. The antenna receives these RF signals and passes them to the RTL-SDR, which digitizes the data and sends it to the Raspberry Pi over USB. The dump1090-fa software decodes the messages and serves them through the SkyAware web interface, allowing nearby aircraft to be viewed from any browser on the local network.

## Build Guide

### 1. Install Raspberry Pi OS

Flash the latest 64-bit version of Raspberry Pi OS to a microSD card using Raspberry Pi Imager. Insert the microSD card into the Raspberry Pi, connect power, and complete the initial operating system setup.

---

### 2. Update the Raspberry Pi

Update the operating system and install Git.

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install git
```

---

### 3. Connect the RTL-SDR

Connect the Nooelec NESDR Smart v5 to a USB port on the Raspberry Pi and attach the 1090 MHz antenna.

Verify that the RTL-SDR is detected:

```bash
lsusb
```

You should see an RTL2838-based SDR device listed.

---

### 4. Install dump1090-fa

Install FlightAware's dump1090-fa package following the official installation instructions. This software decodes ADS-B transmissions received by the RTL-SDR and hosts the SkyAware web interface.

After installation, verify that the service is running:

```bash
sudo systemctl status dump1090-fa
```

---

### 5. Verify Aircraft Reception

Open the local SkyAware interface:

```
http://<RaspberryPi-IP>/skyaware
```

You should see nearby aircraft displayed on the map.

You can also verify that aircraft are being received from the terminal:

```bash
journalctl -u dump1090-fa -f
```

---

### 6. Access the System from Another Device

Determine the Raspberry Pi's IP address:

```bash
hostname -I
```

From any device connected to the same local network, open a browser and navigate to:

```
http://<RaspberryPi-IP>/skyaware
```

The web interface displays live aircraft positions, altitude, speed, heading, and identification information in real time.

## Results

## Troubleshooting

## Future Improvements

- Install an outdoor 1090 MHz antenna
- Add a low-noise amplifier (LNA)
- Increase reception range
- Feed data to FlightAware
- Log aircraft data to a database
- Build a custom enclosure
- Design a custom PCB for SDR power filtering

## License

