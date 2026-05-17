<div align="center">
  <kbd>
    <img src="img/logo.png" width="70%"/>
  </kbd>
</div>

<h1 align="center">Grand Hack Auto Sandbox</h1>

<p align="center">
  CARLA + MQTT + Malware Detection Engine for Connected and Autonomous Vehicle Security Research
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3-blue" />
  <img src="https://img.shields.io/badge/CARLA-0.9.13-green" />
  <img src="https://img.shields.io/badge/MQTT-Mosquitto-orange" />
  <img src="https://img.shields.io/badge/Docker-Supported-blue" />
</p>

---

# Overview

Grand Hack Auto Sandbox is a reproducible research environment designed for studying cloud-based malware attacks against Connected and Autonomous Vehicles (CAVs).

The project integrates:

- CARLA 0.9.13 simulator
- Eclipse Mosquitto MQTT broker
- Docker-based deployment
- Python MQTT clients
- Hydra-MQTT toolkit
- Telemetry logging and detection pipelines

Each simulated vehicle becomes an addressable MQTT endpoint capable of receiving commands and publishing telemetry data.

This enables:

- MQTT-based vehicle command injection testing
- Telemetry monitoring and replay analysis
- Malware behavior simulation
- Network-level attack experimentation
- Real-time anomaly detection research

---

# Architecture

The sandbox combines three major layers:

## Simulation Layer
- CARLA server running inside Docker
- Unreal Engine 4 simulation backend
- Synchronous simulation mode
- Multi-vehicle support

## Messaging Layer
- Eclipse Mosquitto MQTT broker
- Topic-based command and telemetry exchange
- Vehicle-specific MQTT topics

## Client Layer
- Python MQTT clients
- Pygame rendering interface
- Telemetry logging system
- Hydra-MQTT integration

---

# Features

- ✅ CARLA 0.9.13 integration
- ✅ Dockerized simulation environment
- ✅ MQTT-based vehicle communication
- ✅ Multi-vehicle simulation
- ✅ Telemetry collection and logging
- ✅ Hydra-MQTT toolkit support
- ✅ Malware command injection experimentation
- ✅ Real-time telemetry monitoring
- ✅ Detection engine architecture
- ✅ CSV logging for replay and analysis
- ✅ MQTT topic-based command routing
- ✅ Headless CARLA support (No-rendering mode)

---

# VMware Environment

The following VMware files were used:

```bash
carla-ubuntu-20.ovf
carla-ubuntu-20.mf
carla-ubuntu-20-disk1.vmdk
```

These files provide a preconfigured Ubuntu 20 environment prepared for CARLA simulation and MQTT experimentation.

---

# Virtual Machine Login

```bash
Username: carla
Password: carla
```

Create personal workspace:

```bash
mkdir ~/Desktop/imran
```

---

# Requirements

- Ubuntu 20.04 LTS
- Python 3.7+
- Docker
- Docker Compose
- VMware Workstation Pro
- CARLA Simulator 0.9.13

---

# Clone Repository

```bash
git clone https://github.com/your-username/your-repository-name.git
```

```bash
mv your-repository-name ~/Desktop/
cd ~/Desktop/your-repository-name
```

---

# Install Docker

Update packages:

```bash
sudo apt update
```

Install Docker:

```bash
sudo apt install docker.io -y
```

Start Docker service:

```bash
sudo systemctl start docker
```

Enable Docker:

```bash
sudo systemctl enable docker
```

Verify installation:

```bash
docker --version
```

---

# Install Docker Compose

```bash
sudo apt install docker-compose -y
```

Verify:

```bash
docker-compose --version
```

Add user to Docker group:

```bash
sudo usermod -aG docker $USER
newgrp docker
```

---

# Start CARLA MQTT Environment

Navigate to project directory:

```bash
cd cav-sandbox-mqtt-master
```

Launch containers:

```bash
sudo docker compose up
```

This starts:

- CARLA Server
- Mosquitto MQTT Broker

Default MQTT Port:

```bash
1883
```

---

# Configure MQTT Client

Edit broker configuration inside:

```bash
/app/main.py
```

Change:

```python
broker = "localhost"
```

---

# Install Python Dependencies

```bash
pip install -r requirements.txt
```

---

# Run CARLA Simulation

Single vehicle:

```bash
python3 run.py --num-cars 1
```

Multiple vehicles:

```bash
python3 run.py --num-cars 2
python3 run.py --num-cars 3
python3 run.py --num-cars 4
```

---

# MQTT Topic Scheme

| Topic | Direction | Description |
|---|---|---|
| carla/car{N}/control | SUB | Vehicle command input |
| carla/car{N}/location | PUB | Vehicle position |
| carla/car{N}/velocity | PUB | Vehicle velocity |
| carla/car{N}/acceleration | PUB | Vehicle acceleration |
| carla/car{N}/gnss | PUB | GPS telemetry |

---

# Run MQTT Client

```bash
python3 client.py --broker localhost --topics topics.txt --commands commands.txt
```

This connects the MQTT client to the local Mosquitto broker and enables CARLA vehicle communication.

---

# Hydra-MQTT Toolkit

## Verify Installation

```bash
python3 mqtthydra.py -h
```

---

## Execute Hydra-MQTT

```bash
python3 mqtthydra.py --carla_command commands.txt --carla_topic topics.txt
```

The toolkit subscribes to CARLA MQTT topics and performs MQTT command interaction testing.

---

# Command Map

The default command vocabulary:

```python
command_map = {
    "stop": {"brake": 1.0},
    "forward": {"throttle": 0.5, "steer": 0.0, "brake": 0.0},
    "left": {"throttle": 0.3, "steer": -0.5, "brake": 0.0},
    "right": {"throttle": 0.3, "steer": 0.5, "brake": 0.0},
}
```

---

# Telemetry Lifecycle

Each vehicle continuously publishes:

- Location
- Velocity
- Acceleration
- GNSS data

Telemetry is:
- Published through MQTT
- Logged into CSV files
- Consumed by the detection engine

---

# Malware Detection Engine

The project includes the design of a layered malware detection engine capable of:

- Detecting anomalous MQTT behavior
- Monitoring telemetry drift
- Detecting spoofed telemetry
- Identifying command flooding attacks
- Performing statistical anomaly detection
- Running ML-based behavioral analysis

## Detection Layers

### Rule-Based Detection
- Command-rate thresholding
- Invalid command detection
- Forbidden topic publishing
- Telemetry spoofing checks

### Statistical Detection
- Z-score analysis
- EWMA drift monitoring
- MQTT latency analysis

### ML-Based Detection
- Isolation Forest
- LSTM sequence anomaly detection

---

# Threat Scenarios Supported

- Command injection
- Replay attacks
- MQTT flooding
- Topic hijacking
- Telemetry spoofing
- Stealthy steering drift
- Latency attacks

---

# Logging System

Generated logs:

```bash
logs/all_vehicles_log.csv
logs/per_vehicle/{car}.csv
logs/per_vehicle/{car}_latency.csv
logs/incidents.csv
```

---

# Project Structure

```bash
cav-sandbox-mqtt-master/
│
├── app/
├── docker-compose.yml
├── requirements.txt
├── run.py
├── client.py
├── commands.txt
├── topics.txt
├── mqtthydra.py
├── telemetry_logger.py
├── mqtt_car_client.py
├── world.py
├── hud.py
└── carla-client-mqtt/
```

---

# Technologies Used

- CARLA Simulator 0.9.13
- Docker
- Docker Compose
- Mosquitto MQTT Broker
- Paho MQTT
- Python 3
- Pygame
- VMware Workstation Pro

---

# Research Use Cases

- Connected vehicle cybersecurity
- MQTT attack simulation
- Malware analysis
- Vehicle telemetry analysis
- Cloud-connected automotive systems
- Anomaly detection research
- Autonomous vehicle security

---

# References

- CARLA Documentation
- Eclipse Mosquitto
- Paho MQTT Python Client
- starter-carla-0913 project

---

# Research and Educational Disclaimer

This project is intended strictly for:

- Academic research
- Educational purposes
- Controlled cybersecurity experiments
- Authorized testing environments

Do not deploy against production or unauthorized systems.

---

# Author

Imran Hasan

Department of Computer Science and Engineering  
Islamic University, Bangladesh
