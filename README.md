# moOde-audio-USB-disable

This repository contains a script designed to monitor an MPD (Music Player Daemon) log file and manage the power state of a USB hub port based on specific log entries. The script can be configured to run automatically at system startup using a systemd service.

## Overview

The script performs the following functions:

1. **Monitors the MPD log file** for specific error messages indicating that the USB audio device is not available.
2. **Enables the USB port** if the error is detected, allowing MPD to play music.
3. **Checks the playback status** of MPD and increments a timer if playback is stopped.
4. **Disables the USB port** if playback has been stopped for a specified period (default: 600 seconds).

## Script Details

- **Path and Variables:**
  - `TIMER_FILE`: Path to the file storing the timer value.
  - `MPD_LOG`: Path to the MPD log file.
  - `SEARCH_STRING`: String to search for in the log file.
  - `HUB` and `PORT`: USB hub and port to manage. (check with 'sudo uhubctl' command)

## Installation and Setup

### Prerequisites

- Ensure that `uhubctl` is installed
  ```
  sudo apt install uhubctl
  ```
 
### Setting Up the Script

Make the script executable:
```bash
chmod +x usb_disable.sh
```
Create a systemd service unit file and paste usb_disable.service inside:
```bash
sudo nano /etc/systemd/system/usb_disable.service
```
Enable the service to run at startup:
```bash
sudo systemctl enable usb_disable.service
```
Start the service immediately to test:
```bash
sudo systemctl start usb_disable.service
```
Check the status of the service to ensure it’s running correctly:
```bash
sudo systemctl status usb_disable.service
```
