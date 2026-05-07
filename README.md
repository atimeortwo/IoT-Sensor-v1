# IoT-Sensor-v1
A secure IoT environmental monitoring system built with an ESP32 sensor node, FastAPI backend, SQLite logging, and a live dashboard with history charting.

# Overview
This project collects environmental data from an ESP32-based sensor node, applies local threshold logic, transmits authenticated telemetry over Wi-Fi, validates and stores readings in a backend database, and visualizes both live and historical data in a browser dashboard.

## What problem does this solve? 
Many homes in the US do not have an easy adaptable and low cost way of monitoring key indicators to improve home health and efficiency. That is where this device comes in allowing for the interfacing with various physical aspects such as closing a vent because that room is already cool or monitoring VOC levels in a workshop. This device allows for easy inputs into a locally ran or cloud based smart home system leading to improved costs, comfort, and safety at the house. 

The system currently monitors:
- Temperature
- Humidity
- User-defined threshold
- Alert/normal state

<img width="995" height="877" alt="Screenshot 2026-05-07 183331" src="https://github.com/user-attachments/assets/779966bb-eb80-4f40-b621-8393fd051208" />


It also includes basic security controls such as:
- API key authentication
- Device ID validation
- Input validation
- Secrets separation from source control

### Hardware
- 1 x ESP32 DevKitV1
- 1 x DHT11 temperature/humidity sensor
- 1 x Potentiometer for threshold adjustment
- 1 x Red LED and 1 x Green LED for alert status
- 2 x Resistors for LEDs
- 1 x Breadboard
- Various jumper wires

### Software Capabilities
- Wi-Fi connection from ESP32 to backend
- FastAPI backend for ingestion and dashboard serving
- SQLite database logging
- Live browser dashboard
- Historical chart using Chart.js
- API key authentication
- Device ID allowlist
- Input validation for sensor payloads

### Pin Map on ESP32
- DHT11 DATA → GPIO 4
- Potentiometer middle pin → GPIO 34
- Red LED → GPIO 2
- Green LED → GPIO 25

### Power
- ESP32 3V3 powers the DHT11 and potentiometer
- Shared ground is used across all components

### Wiring Example
<img width="3024" height="4032" alt="IMG_0343" src="https://github.com/user-attachments/assets/da35c3a1-149b-4eea-a6e1-08f2c9b20a20" />
<img width="4032" height="3024" alt="IMG_0348" src="https://github.com/user-attachments/assets/54011305-ab6e-416e-980f-169a04f020d2" />
<img width="4284" height="5712" alt="IMG_0388" src="https://github.com/user-attachments/assets/0ca79af7-f22a-459d-bfd2-699ab6f0a04e" />

## Software Stack
### Embedded
- PlatformIO
- Arduino framework for ESP32

### Backend
- Python
- FastAPI
- Uvicorn
- SQLite

### Frontend / Visualization
- HTML
- JavaScript
- Chart.js
  
## Data from sensor to end user (DSEU) v1 
DHT11 + Potentiometer -> ESP32 -> Threshold logic and red/green LEDs -> Wi-Fi HTTP POST -> FastAPI backend -> SQLite database -> Live dashboard + history chart

<img width="838" height="260" alt="image" src="https://github.com/user-attachments/assets/d25a3b36-bf5e-4d9f-b49f-35eeb8134239" />

## Security
- secrets.h stores Wi-Fi credentials and API key outside the main code
- .gitignore prevents secrets from being committed
- API key authentication protects the ingestion endpoint
- Device ID validation restricts which devices may submit data
- Input validation rejects impossible or malformed readings
    Current request outcomes
      - 200 = valid reading accepted
      - 401 = invalid API key
      - 403 = unknown device ID
      - 422 = invalid payload

## Threat Model Summary
## Assets
- Sensor data integrity
- Backend availability
- Database integrity
- Dashboard visibility
- Wi-Fi credentials
- API key
- Device identity
- Future actuator safety

## Threats
### 1. Fake client submits sensor data
- Risk: false readings, bad dashboards, wrong future control decisions
- Current control: API key authentication
- Current control: device ID allowlist

### 2. Valid device sends malformed or impossible readings
- Risk: corrupted database, misleading alerts, unsafe future automation
- Current control: input validation

### 3. Secrets exposed in source control
- Risk: unauthorized access to backend or Wi-Fi
- Current control: `secrets.h`
- Current control: `.gitignore`

### 4. Compromised IoT node on trusted network
- Risk: pivoting or spoofed telemetry
- Planned control: isolate IoT devices on separate VLAN/network
- Planned control: firewall restrictions

### 5. Backend unavailable
- Risk: telemetry loss, stale dashboards
- Planned control: move to Raspberry Pi always-on host
- Planned control: service management and restart behavior

### 6. Future actuator behaves unsafely
- Risk: incorrect vent movement or unsafe environmental control
- Planned control: fail-open design
- Planned control: manual override
- Planned control: min/max actuator limits
- Planned control: deadband and cooldown logic

## Security Posture Summary
This project currently implements:
- authentication
- device identity validation
- payload validation
- secrets separation

This project still needs:
- stronger deployment on Raspberry Pi
- network segmentation
- MQTT authentication
- logging/alerting improvements
- actuator safety controls before real control deployment

## How to Run
1) ESP32
Open the project in PlatformIO
Configure include/secrets.h
Upload the firmware to the ESP32
Open Serial Monitor
2) Backend
From the backend/ folder, run: .venv\Scripts\python.exe -m uvicorn main:app --host 0.0.0.0 --port 8000 --reload
3) Dashboard
Open in browser: http://127.0.0.1:8000/dashboard
Or from another device on the same network: http://<your-computer-ip>:8000/dashboard

## Validation and Testing
The following tests have been performed:
- Sensor data changes with environment changes
- Potentiometer changes threshold behavior
- LEDs reflect alert vs normal state
- Backend receives ESP32 telemetry
- Dashboard updates live
- SQLite stores readings persistently
- Invalid API key returns 401
- Invalid device ID returns 403
- Invalid humidity/temperature/threshold values return 422

## Future Plans
### Near-Term
- Move backend to Raspberry Pi
- Add MQTT
- Add Grafana
- Add multiple ESP32-C3 nodes
- Add RSSI and uptime telemetry

### Mid-Term
- Add ESP-NOW relay/gateway support
- Upgrade sensors from DHT11 to BME280/SHT31
- Build one durable node with enclosure/perfboard

### Long-Term
- Add mini vent actuator prototype
- Add safe control logic
- Add LocalStack / AWS-style architecture practice
- Add STM32 + RTOS track
- Add TinyML/anomaly detection
- Digital Twin

## What I learned...
- Embedded systems
- Sensor integration
- IoT telemetry
- Backend API development
- Database logging
- Dashboarding and observability
- Basic IoT security controls
- Systems engineering thinking for cyber-physical systems

## Project Structure
```text
Temperature and Humidity Sensor/
├─ src/
│  └─ main.cpp
├─ include/
│  └─ secrets.h
├─ backend/
│  ├─ main.py
│  └─ sensor_readings.db
├─ .gitignore
├─ platformio.ini
└─ README.md
