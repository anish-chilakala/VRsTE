# VRsTE
# 🚀 2D Robotics Physics Engine A modular, high‑performance 2D physics and robotics simulation engine written in TypeScript. Designed for real‑time robotics competitions, AI research, autonomous navigation, and game‑style simulations. This engine blends: - a custom 2D physics core, - a Box2D‑style architecture (math, broadphase, narrowphase, solver), - a robotics layer (motors, sensors, drivetrain), - an AI layer (path planning, behavior trees, vision), - a field/game layer (competition presets, scoring, match flow). It is built for clarity, extensibility, and realism.


---

## 🧠 Architecture Overview

The engine is divided into **four major layers**:

### **1. Physics Core**
Implements a Box2D‑style physics engine:
- Dynamic AABB tree broadphase  
- SAT narrowphase  
- Contact manifolds  
- Sequential impulse solver  
- Baumgarte stabilization  
- Island solver  
- Continuous collision detection (TOI)  
- Full joint system  

This layer is completely independent from robotics logic.

---

### **2. Robotics Layer**
Adds realistic robot behavior:
- Differential, mecanum, and custom drivetrains  
- Motor models (torque curves, gearing, voltage)  
- Sensors (raycast camera, lidar, encoders, IMU)  
- Collision layers for robots, field, and game objects  
- Multi‑robot support  

---

### **3. AI Layer**
Provides autonomy and decision‑making:
- A* / RRT / PRM path planning  
- Trajectory generation  
- Behavior trees  
- Vision simulation  
- Lidar simulation  
- Multi‑robot coordination hooks  

---

### **4. Field & Game Layer**
Implements competition‑style environments:
- Field geometry  
- Game objects  
- Scoring zones  
- Match flow (auto, teleop, endgame)  
- Competition presets (VEX, FTC, FRC, RoboMaster, etc.)  

---

## 🧩 Key Features

### **Physics**
- Continuous collision detection  
- Stable stacking  
- Realistic friction & restitution  
- Joints (revolute, prismatic, distance, motor, pulley, gear)  
- Deterministic simulation (fixed timestep)  

### **Robotics**
- Motor physics  
- Drivetrain models  
- Sensor simulation  
- Multi‑robot collisions (configurable per competition)  

### **AI**
- Path planning  
- Trajectory following  
- Behavior trees  
- Raycast vision  
- Lidar  

### **Game Simulation**
- Field loader  
- Game object physics  
- Scoring system  
- Competition presets  

---

## 🛠 Getting Started

### Install dependencies
```bash
npm install
