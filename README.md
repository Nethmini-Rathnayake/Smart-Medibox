# 💊 Smart Medibox — IoT Medication Reminder

An ESP32-based smart medication reminder device that solves the problem of missed doses for patients managing complex medication schedules. Features NTP-synchronized timezone-aware alarms, an OLED display menu, real-time environmental monitoring, and an automated servo-driven shade mechanism — all simulated on Wokwi.

🔗 [**Simulate on Wokwi**](https://wokwi.com/projects/397686207007907841)

---

## ✨ Features

- ⏰ **3 configurable alarms** — set hours and minutes independently, with enable/disable control
- 🌍 **Timezone-aware** — syncs with NTP server (`pool.ntp.org`) and supports configurable UTC offset
- 📺 **OLED display menu** — 6-mode navigation (Set Time, Set Timezone, Set Alarm 1–3, Disable Alarm)
- 🌡️ **DHT22 sensor** — real-time temperature and humidity monitoring
- ☀️ **Dual LDR sensors** — ambient light detection (left & right) for shade positioning
- 🔄 **Servo-driven shade** — automatically adjusts angle based on LDR readings to protect light/heat-sensitive medications
- 📡 **MQTT telemetry** — publishes live sensor data (LDR left/right, temperature, humidity) to broker
- 🔔 **Buzzer + LED alerts** — musical alarm tones using defined notes (C–C_H scale)
- 🎛️ **4-button interface** — UP, DOWN, OK, CANCEL for full menu navigation

---

## 🛠️ Hardware Components

| Component | Pin | Purpose |
|-----------|-----|---------|
| ESP32 DevKit V1 | — | Microcontroller |
| SSD1306 OLED (128×64) | SDA: D21, SCL: D22 | Display |
| DHT22 Sensor | D12 | Temperature & Humidity |
| Servo Motor | D2 | Shade angle control |
| LDR Left | D34 (ADC) | Left light sensor |
| LDR Right | D35 (ADC) | Right light sensor |
| Buzzer | D5 | Alarm sound |
| LED | D15 | Visual indicator |
| Button CANCEL | D34 | Menu navigation |
| Button OK | D32 | Menu confirm |
| Button UP | D33 | Menu up |
| Button DOWN | D35 | Menu down |

---

## 📡 MQTT Topics

| Topic | Data |
|-------|------|
| `MedBOX-LDR_LEFTT` | Left LDR value (0–1) |
| `MedBOX-LDR_RIGHTT` | Right LDR value (0–1) |
| `MedBOX-Tempp` | Temperature (°C) |
| `MedBOX-Humii` | Humidity (%) |

The Node-RED dashboard (`node-red.json`) subscribes to these topics for live visualisation.

---

## 📁 Project Structure

| File | Description |
|------|-------------|
| `esp32-arduino.ino` | Main ESP32 firmware |
| `diagram.json` | Wokwi circuit diagram |
| `wokwi-project.txt` | Wokwi project link |
| `node-red.json` | Node-RED dashboard flow |
| `libraries.txt` | Required Arduino libraries |

---

## 🚀 Getting Started

### Simulate on Wokwi
1. Go to [https://wokwi.com/projects/397686207007907841](https://wokwi.com/projects/397686207007907841)
2. Click **Start Simulation**

### Run Locally
**Install libraries** (Arduino IDE or PlatformIO):
```
Adafruit GFX Library
Adafruit SSD1306
DHT sensor library for ESPx
PubSubClient
ESP32Servo
```

**Configure WiFi & MQTT** in `esp32-arduino.ino`:
```cpp
// WiFi
WiFi.begin("YOUR_SSID", "YOUR_PASSWORD");

// MQTT Broker
mqttClient.setServer("YOUR_BROKER_IP", 1883);
```

**Flash to ESP32** and open Serial Monitor at 115200 baud.

---

## 🛠️ Tech Stack

| Component | Tool |
|-----------|------|
| Microcontroller | ESP32 DevKit V1 |
| Firmware | C++, Arduino IDE |
| Communication | MQTT (PubSubClient), WiFi |
| Time Sync | NTP (pool.ntp.org) |
| Display | Adafruit SSD1306, Adafruit GFX |
| Sensors | DHT22, LDR (photoresistor) |
| Simulation | Wokwi |
| Dashboard | Node-RED |
