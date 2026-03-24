<div align="center">

# 📡 RFID Attendance System — ESP32 + Google Sheets + Live Dashboard

**Real-time IoT attendance logging with hardware, cloud sync, and web dashboard**

[![Hardware](https://img.shields.io/badge/Hardware-ESP32-blue?style=flat-square&logo=arduino)](https://github.com/DINESH2841/RFID-Based-ESP-Integrated-with-Google-Sheets)
[![Cloud](https://img.shields.io/badge/Cloud-Google_Sheets_API-green?style=flat-square&logo=googlesheets)](https://github.com/DINESH2841/RFID-Based-ESP-Integrated-with-Google-Sheets)
[![Latency](https://img.shields.io/badge/Sync_Latency-<800ms-brightgreen?style=flat-square)](https://github.com/DINESH2841/RFID-Based-ESP-Integrated-with-Google-Sheets)

</div>

---

## 🎯 What This System Does

A complete end-to-end IoT attendance system: an RFID card tap on the ESP32 triggers a WiFi POST request to Google Apps Script, which logs the entry to Google Sheets in **under 800ms**. A companion web dashboard provides live filtering, admin controls, and CSV export.

---

## 🔌 Hardware Setup

![Hardware Setup](images/setup.jpg)

| Component | Specification |
|-----------|--------------|
| Microcontroller | ESP32 WROOM-32 (240MHz dual-core) |
| RFID Reader | RC522 (13.56 MHz, SPI Protocol) |
| Communication | WiFi 802.11 b/g/n (2.4GHz) |
| Power | 3.3V from USB or battery |

### SPI Wiring (RC522 → ESP32)
```
RC522 Pin  →  ESP32 Pin
SCK        →  GPIO 18
MISO       →  GPIO 19
MOSI       →  GPIO 23
SDA (SS)   →  GPIO 5
GND        →  GND
3.3V       →  3.3V
RST        →  GPIO 22
```

---

## 📊 Live Proof — System in Action

### Google Sheets Real-Time Logging

![Google Sheets Output](images/output.png)

> Data columns: `Timestamp | Student ID | Name | Status (IN/OUT) | RFID UID`

### Registered Users Database

![Registered Users](images/registered_users.png)

### ESP32 Serial Monitor — Real-time Logs

![Serial Monitor](images/serial_monitor.png)

---

## 🏗️ System Architecture

```
[RFID Card Tap]
      ↓
[RC522 RFID Reader]  — SPI Protocol @ 10MHz
      ↓
[ESP32 Microcontroller]
      ↓  (WiFi HTTP POST)
[Google Apps Script Web App]  — Acts as REST webhook
      ↓  (Sheets API)
[Google Sheets Master Log]
      ↓  (JSON API)
[Web Dashboard]  — Search, Filter, CSV Export, Admin Controls
```

---

## ⚙️ Key Engineering Decisions

1. **Google Apps Script as middleware** — avoids exposing Sheets API credentials on the hardware. ESP32 only communicates with a public webhook URL.
2. **HTTP POST over MQTT** — chosen for simplicity in environments without an MQTT broker.
3. **Nonblocking WiFi reconnection** — if WiFi drops, ESP32 buffers the last tap and retries on reconnect (stored in EEPROM).
4. **UID-to-name mapping** in `registered_users.json` — stored on ESP32 SPIFFS filesystem.

---

## 🌐 Web Dashboard Features

- 🔍 Real-time search filtering by name, student ID, or date
- 📥 CSV export of filtered attendance records
- 🔐 Admin panel with manual override
- 📊 Summary stats (total attendance rate, daily breakdown)
- 🔄 Auto-refresh every 10 seconds

---

## ▶️ Setup Guide

### 1. Flash ESP32 firmware
```bash
# Open arduino/rfid.ino in Arduino IDE
# Configure WiFi credentials:
const char* ssid = "YOUR_SSID";
const char* password = "YOUR_WIFI_PASSWORD";
# Upload to ESP32
```

### 2. Deploy Google Apps Script
```
1. Open appscript/Code.gs
2. Deploy as Web App → "Execute as: Me", "Who has access: Anyone"
3. Copy URL → paste into rfid.ino SCRIPT_URL variable
```

---

## 🔐 Security

- No API keys or credentials in the repository
- Google Apps Script acts as a secure proxy
- ESP32 never holds Sheets credentials

---

## 🔥 Features

- ✅ Sub-800ms cloud sync from card tap to Google Sheets
- ✅ Offline buffering — doesn't lose data during WiFi drops
- ✅ Web dashboard with live filtering and CSV export
- ✅ Supports 50+ registered cards

---

<div align="center">

**Hardware. Software. Cloud. All connected.**  
⭐ Star this repo if you find it useful

</div>
