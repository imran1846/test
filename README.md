# CARLA Simulator with MQTT & Hydra Toolkit

A practical setup and experimentation environment for running the CARLA autonomous driving simulator with MQTT-based communication and the Hydra-MQTT toolkit for topic interaction and reconnaissance testing.

## Overview

This project demonstrates:

- CARLA simulator setup inside Ubuntu VM
- MQTT broker communication using Mosquitto
- Docker-based deployment environment
- MQTT client interaction with CARLA
- Hydra-MQTT toolkit execution and testing
- Multi-vehicle simulation support

> This setup is intended for research, learning, and controlled lab experimentation purposes only.

---

# Environment Setup

## VMware Files

The following VMware virtual machine files were used:

```bash
carla-ubuntu-20.ovf
carla-ubuntu-20.mf
carla-ubuntu-20-disk1.vmdk
```

These files contain a preconfigured Ubuntu 20 environment prepared for CARLA simulation.

---

# Virtual Machine Login

```bash
Username: carla
Password: carla
```

After logging into the VM, a separate personal workspace was created for custom experimentation and testing.

Example:

```bash
mkdir ~/Desktop/imran
```

---

# Clone Repository

Clone the project repository:

```bash
git clone https://github.com/your-username/your-repository-name.git
```

Move the repository to the Desktop:

```bash
mv your-repository-name ~/Desktop/
cd ~/Desktop/your-repository-name
```

---

# Install Docker

Update package lists:

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

Enable Docker at boot:

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

# Start CARLA MQTT Environment

Navigate to the project directory:

```bash
cd cav-sandbox-mqtt-master
```

Start containers:

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

# Configure MQTT Client

Navigate to the client-side project directory.

Modify the MQTT broker configuration inside:

```bash
/app/main.py
```

Set broker configuration:

```python
broker = "localhost"
```

---

# Install Python Dependencies

Install required packages:

```bash
pip install -r requirements.txt
```

---

# Run CARLA Simulation

Run simulation with different numbers of vehicles.

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

# Copy MQTT Client Workspace

Copy the MQTT client project into a separate workspace:

```bash
cp -r carla-client-mqtt ~/Desktop/imran/
```

---

# Run MQTT Client

Execute the MQTT client:

```bash
python3 client.py --broker localhost --topics topics.txt --commands commands.txt
```

This connects the MQTT client to the local broker and enables topic-based interaction with the CARLA environment.

---

# Hydra-MQTT Toolkit

## Verify Installation

Run help command:

```bash
python3 mqtthydra.py -h
```

This displays:

- Available CLI options
- Topic configuration settings
- MQTT interaction commands

---

# Run Hydra-MQTT Toolkit

Execute Hydra-MQTT using custom topic and command files:

```bash
python3 mqtthydra.py --carla_command commands.txt --carla_topic topics.txt
```

This connects to the MQTT broker and subscribes to configured CARLA MQTT topics for testing and experimentation.

---

# Project Structure

Example structure:

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

# Technologies Used

- Ubuntu 20
- VMware Workstation Pro
- Docker
- Docker Compose
- CARLA Simulator
- Mosquitto MQTT Broker
- Python 3
- Hydra-MQTT Toolkit

---

# Research and Educational Disclaimer

This project and toolkit are intended strictly for:

- Research
- Educational purposes
- Controlled lab experimentation
- MQTT communication testing

Do not deploy these tools against unauthorized or production systems.

---

# Author

Imran Hasan

Department of Computer Science and Engineering  
Islamic University, Bangladesh
