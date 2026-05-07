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

### Main Features
- 1 x ESP32 DevKitV1
- 1 x DHT11 temperature/humidity sensor
- 1 x Potentiometer for threshold adjustment
- 1 x Red LED and 1 x Green LED for alert status
- 2 x Resistors for LEDs
- 1 x Breadboard
- Various jumper wires
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

## Future Plans
I built this project to learn and demonstrate:

- Embedded systems
- Sensor integration
- IoT telemetry
- Backend API development
- Database logging
- Dashboarding and observability
- Basic IoT security controls
- Systems engineering thinking for cyber-physical systems

This project is intended to grow into a distributed sensor network with Raspberry Pi hosting, MQTT, Grafana, relay/gateway nodes, and later actuator control.

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
