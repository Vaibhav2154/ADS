

## 🗃️ Project Workflow

![Flowchart](https://github.com/NCJ-Hackademia/35-MAHAKUMBH/blob/main/RL_TRAINING/assets/flowchart.jpeg)

## 🏗️ System Architecture

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Drone D1      │    │   Drone D2      │    │   Drone D3      │
│  (Laptop 1)     │    │  (Laptop 2)     │    │  (Laptop 3)     │
└─────────┬───────┘    └─────────┬───────┘    └─────────┬───────┘
          │                      │                      │
          └──────────────────────┼──────────────────────┘
                                 │
                    ┌─────────────▼─────────────┐
                    │    Multi-Drone Server     │
                    │      (Laptop 4)           │
                    │                           │
                    │ • WebSocket Hub           │
                    │ • Position Coordination   │
                    │ • Human Detection Logic   │
                    │ • Region Management       │
                    └─────────────┬─────────────┘
                                  │
                    ┌─────────────▼─────────────┐
                    │    Admin Dashboard        │
                    │      (Laptop 4)           │
                    │                           │
                    │ • Real-time Monitoring    │
                    │ • World Map View          │
                    │ • Drone Status Tracking   │
                    │ • Human Discovery Log     │
                    └───────────────────────────┘
```

This project implements an autonomous multi-drone system for search and rescue operations using reinforcement learning (RL). The system trains drone swarms to efficiently search areas, detect victims, and optimize rescue routes while maintaining stable flight patterns. The project consists of:

![Multi Drone Training](https://github.com/NCJ-Hackademia/35-MAHAKUMBH/blob/main/RL_TRAINING/assets/multi.png)

- A **real-time drone UI** for monitoring and controlling drones
- **Reinforcement learning** models to optimize drone search efficiency
- **Simulation-based training** with PyBullet for drone behavior learning
- **Autonomous victim detection** and rescue path optimization

## 🔍 Key Features

- **Autonomous Drone Operations**: Drones navigate and search independently
- **Multi-sensor Integration**: Uses position, IMU, and FOV data
- **Victim Detection & Rescue Planning**: AI-driven decision-making for optimal rescue routes
- **Real-time UI Dashboard**: Monitor drone behavior and RL training
- **Reinforcement Learning**: PPO-based training for optimized navigation

![RL Dashboard](https://github.com/NCJ-Hackademia/35-MAHAKUMBH/blob/main/RL_TRAINING/assets/frontend.png)

## 👩‍💻 System Components

### 1. **Drone UI**
A React and Vite-powered dashboard for real-time visualization and control.

### 2. **Backend (Drone-UI)**
A Python-based backend for processing drone input and managing communication.

### 3. **Reinforcement Learning Module (Drone-RL-Processing)**
Trains drones using PPO with PyBullet simulation.

---

## 🛠️ Setup & Installation

### 1. Clone the repository
```bash
git clone https://github.com/NCJ-Hackademia/35-MAHAKUMBH.git
cd 35-MAHAKUMBH
```

### 2. Backend Setup (Drone-UI)
```bash
cd 3D-Simulation
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements_multi_drone.txt
python backend.py
```

### 3. Frontend Setup (Drone-Dashboard-Frontend)
```bash
cd ../Drone-Recognition-Dashboard
npm install
npm run dev
```
Navigate to `http://localhost:5173` to view the UI.

### 4. Running the Basic UI (Static Page)
To serve the Simulation UI:
```bash
cd ../3D-Simulation
python3 -m http.server 3000
python3 setup_multi_drone.py
```

---
![Basic UI](https://github.com/NCJ-Hackademia/35-MAHAKUMBH/blob/main/RL_TRAINING/assets/frontend_drone.png)

## 🚀 Running the RL Simulation

### 1. Setup the RL Environment
```bash
cd ../RL_TRAINING
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### 2. Start RL Training & Simulation
```bash
# Run the single drone simulation with FOV visualization
python singleDroneWithFOV.py

# Optimized single drone simulation
python singleDrone_final.py

# Multi-drone simulation
python fourDrones_final.py
```

### 3. Start RL Dashboard
```bash
cd RL_Training_FrontendReport
npm install
npm start
```
Navigate to `http://localhost:3000` to view training metrics.

---

## 📊 Performance Metrics

- **Search Efficiency**: Evaluates coverage per unit time
- **Victim Detection Rate**: Measures success in locating victims
- **Revisit Rate**: Tracks unnecessary redundant searches
- **Flight Stability**: Ensures stable drone movement during searches

## 💌 Email Notification System

Mission progress updates are automatically sent via email:
- Search coverage statistics
- Victim detection details
- Optimized rescue paths

---





