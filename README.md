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
- Networking
- System Integration
- Command Line
- Hardware Troubleshooting

## Hardware

| Component | Purpose |
|-----------|---------|
| Raspberry Pi 5 | Hosts the ADS-B software and web server |
| Nooelec NESDR Smart v5 | Receives 1090 MHz ADS-B transmissions |
| MicroSD Card | Stores Raspberry Pi OS |
| Power Supply | Powers the Raspberry Pi |
| USB Extension (optional) | Reduces RF interference |
| 1090 MHz Antenna | Receives aircraft signals |

## Software

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

Install dump1090-fa following FlightAware's repository instructions.

### Configuration

- Enabled the dump1090-fa service
- Verified RTL-SDR detection
- Accessed the web interface through the Raspberry Pi IP address

## System Design

```text
Aircraft
    │
    ▼
1090 MHz ADS-B Signal
    │
    ▼
1090 MHz Antenna
    │
    ▼
RTL-SDR Receiver
    │ USB
    ▼
Raspberry Pi 5
    │
    ▼
dump1090-fa
    │
    ▼
SkyAware Web Server
    │ HTTP
    ▼
Web Browser
```

## Build Guide

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

