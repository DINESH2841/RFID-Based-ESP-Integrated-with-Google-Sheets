# 📡 RFID-Based ESP System Integrated with Google Sheets

## 🚀 Overview

This project uses an ESP microcontroller (ESP32/ESP8266) and an RC522 RFID module to scan cards and log user data directly into Google Sheets in real-time.

It can be used for:
- Attendance systems
- Access control
- Smart logging systems

## ⚙️ Tech Stack
- **ESP8266 / ESP32**
- **RFID Module (RC522)**
- **Arduino IDE**
- **Google Apps Script**
- **Google Sheets API**

## 🧠 System Architecture

**RFID Card** → **ESP** → **WiFi** → **Google Apps Script** → **Google Sheets**

## 🔌 Hardware Required
- ESP8266 / ESP32
- RC522 RFID Module
- Jumper wires
- Power supply

## ▶️ How to Run
1. Upload `arduino/rfid.ino` to your ESP board.
2. Connect the RFID module properly (SCK, MISO, MOSI, SDA pins).
3. Configure your WiFi credentials inside the `.ino` script.
4. Deploy the Google Apps Script (`appscript/Code.gs`) as a Web App.
5. Scan an RFID card → data automatically logs in the Google Sheet.

## 📊 Proof & Output

**1. Hardware Setup:**
![Hardware Setup](images/setup.jpg)

**2. Google Sheets Logging:**
![Output](images/output.png)

**3. Registered Users Database:**
![Registered Users](images/registered_users.png)

**4. ESP32 Serial Monitor:**
![Serial Monitor](images/serial_monitor.png)

## 🔐 Security Notes
- No API keys exposed in the repository.
- Uses a secure Google Apps Script webhook endpoint.

## 🔥 Features
- **Real-time logging** with sub-second accuracy
- **Wireless communication** over local network
- **Scalable system** (add multiple nodes to one sheet)

## 🚧 Future Improvements
- Add web dashboard
- Add authentication layer
- Improve latency with MQTT

## 📫 Contact
Dinesh – GitHub: [https://github.com/DINESH2841](https://github.com/DINESH2841)
