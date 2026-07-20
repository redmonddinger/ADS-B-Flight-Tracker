# ADS-B-Flight-Tracker
Raspberry Pi ADS-B receiver using an RTL-SDR to monitor live aircraft transmissions.

The system receives 1090 MHz ADS-B broadcasts from nearby aircraft, decodes them using dump1090-fa, and displays real-time aircraft positions and flight information through a browser-based interface.

This project demonstrates RF fundamentals, Software Defined Radio (SDR), Linux system administration, networking, and hardware/software integration.

## Project Overview

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

## Build Guide

## Results

## Troubleshooting

## Future Improvements

## License

