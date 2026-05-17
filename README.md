<div align="center">
  <kbd>
    <img src="img/logo.png" width="70%"/>
  </kbd>
</div>
<br />

# CARLA Simulator with MQTT & Hydra Toolkit

A practical sandbox environment for experimenting with the CARLA autonomous driving simulator, MQTT communication, and the Hydra-MQTT toolkit for reconnaissance and command interaction testing.

This environment integrates CARLA, Docker, Mosquitto MQTT broker, and Python MQTT clients to simulate connected vehicle communication and controlled MQTT-based experimentation.

---

## Overview

This project demonstrates:

- CARLA simulator deployment inside Ubuntu VM
- MQTT communication using Mosquitto broker
- Docker-based CARLA environment
- MQTT client interaction with CARLA
- Hydra-MQTT toolkit integration
- Multi-vehicle simulation support
- MQTT topic monitoring and command testing

> This project is intended for research, educational purposes, and controlled lab experimentation only.

---

## Features

- ✅ CARLA simulator running in Docker containers
- ✅ Mosquitto MQTT broker integration
- ✅ MQTT client communication with CARLA
- ✅ Multiple simulated vehicle support
- ✅ Hydra-MQTT toolkit execution and testing
- ✅ Docker Compose deployment workflow
- ✅ Lightweight Python MQTT client implementation
- ✅ Ubuntu 20 virtual machine environment

---

## Requirements

- Ubuntu 20.04 LTS
- VMware Workstation Pro
- Python 3
- Docker
- Docker Compose
- CARLA Simulator
- Mosquitto MQTT Broker

---

## VMware Environment

The following VMware files were used:

```bash
carla-ubuntu-20.ovf
carla-ubuntu-20.mf
carla-ubuntu-20-disk1.vmdk
```

These files provide a preconfigured Ubuntu 20 environment prepared for CARLA simulation and MQTT experimentation.

---

## Virtual Machine Login

```bash
Username: carla
Password: carla
```

A separate workspace was created for experimentation:

```bash
mkdir ~/Desktop/imran
```

---

## Clone Repository

```bash
git clone https://github.com/your-username/your-repository-name.git
```

Move repository to Desktop:

```bash
mv your-repository-name ~/Desktop/
cd ~/Desktop/your-repository-name
```

---

## Install Docker

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

Enable Docker on boot:

```bash
sudo systemctl enable docker
```

Verify installation:

```bash
docker --version
```

---

## Install Docker Compose

```bash
sudo apt install docker-compose -y
```

Verify installation:

```bash
docker-compose --version
```

Add current user to Docker group:

```bash
sudo usermod -aG docker $USER
newgrp docker
```

---

## Start CARLA MQTT Environment

Navigate to the project directory:

```bash
cd cav-sandbox-mqtt-master
```

Start Docker containers:

```bash
sudo docker compose up
```

This launches:

- CARLA server container
- Mosquitto MQTT broker container

Default MQTT broker port:

```bash
1883
```

---

## Configure MQTT Client

Modify the MQTT broker configuration inside:

```bash
/app/main.py
```

Set broker:

```python
broker = "localhost"
```

---

## Install Python Dependencies

```bash
pip install -r requirements.txt
```

---

## Run CARLA Simulation

Run simulation with a single vehicle:

```bash
python3 run.py --num-cars 1
```

Run with multiple vehicles:

```bash
python3 run.py --num-cars 2
python3 run.py --num-cars 3
python3 run.py --num-cars 4
```

---

## MQTT Client Workspace

Copy MQTT client into a personal workspace:

```bash
cp -r carla-client-mqtt ~/Desktop/imran/
```

---

## Run MQTT Client

Execute the MQTT client:

```bash
python3 client.py --broker localhost --topics topics.txt --commands commands.txt
```

This connects to the local MQTT broker and enables topic-based communication with the CARLA simulation environment.

---

## Hydra-MQTT Toolkit

### Verify Installation

```bash
python3 mqtthydra.py -h
```

This displays:

- Available command-line options
- Topic configuration settings
- MQTT interaction commands

---

## Run Hydra-MQTT Toolkit

Execute Hydra-MQTT with custom topic and command files:

```bash
python3 mqtthydra.py --carla_command commands.txt --carla_topic topics.txt
```

The toolkit connects to the local MQTT broker and subscribes to configured CARLA MQTT topics for communication monitoring and experimentation.

---

## Project Structure

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
└── carla-client-mqtt/
```

---

## Technologies Used

- Ubuntu 20
- VMware Workstation Pro
- Docker
- Docker Compose
- CARLA Simulator
- Mosquitto MQTT Broker
- Python 3
- Hydra-MQTT Toolkit

---

## Research and Educational Disclaimer

This project and toolkit are intended strictly for:

- Research
- Educational purposes
- Controlled lab experimentation
- MQTT communication testing

Do not deploy these tools against unauthorized or production systems.

---

## License

This project is intended for academic and research purposes.

---

## Author

Imran Hasan

Department of Computer Science and Engineering  
Islamic University, Bangladesh
