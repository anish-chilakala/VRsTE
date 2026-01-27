# VRSTE — Virtual Robotics Simulation & Testing Environment

VRSTE (Virtual Robotics Simulation & Testing Environment) is a high-performance, browser-based robotics simulator designed for education, competitive robotics, and professional autonomous systems development.  
Users write **C++ code directly in the browser**, which is transpiled and executed in real time on a fully simulated field.

VRSTE features a modular physics backend, a robust robot API, and a flexible rendering system that supports both educational and advanced research workflows.

---

## Features

### C++ Programming in the Browser
- Monaco-powered editor
- C++ → JavaScript transpilation
- Real-time execution
- Async runtime with timing, motor control, and sensor access

### Robot API
A consistent, engine-agnostic API for:
- Motor power control
- Encoder simulation
- Heading and odometry
- Autonomous routines
- Sensor modeling (planned)

### Physics Abstraction Layer
VRSTE supports multiple physics engines through a unified interface:
- Simulation.js (built-in engine)
- MuJoCo (planned)
- Bullet (planned)
- Drake (planned)

This design allows the community to add new engines without modifying the core simulator.

### Coordinate Plane Mode
For competitive robotics and professional applications:
- Field displayed as a full coordinate plane
- X/Y axes, grid, and origin markers
- Real-time pose visualization
- Supports inches or meters

### Browser-Native
- No installation required
- Runs on any modern browser
- Cross-platform support

---

## Architecture
VRSTE is built on a layered, modular architecture designed for **flexibility, performance, and long-term extensibility**.

C++ Editor
->
C++ → JS Transpiler
->
Async Runtime Sandbox
->
Robot API (engine-agnostic)
->
Physics Abstraction Layer
->
Selected Physics Engine
->
Field Renderer & UI


Each layer is **isolated and replaceable**, allowing VRSTE to evolve without breaking existing user code or community extensions.

---

## Why VRSTE Is Different

### Modular Physics Engine System
Most browser-based robotics simulators are locked to a single physics engine. VRSTE introduces a **Physics Abstraction Layer**, enabling seamless switching between:

- **Simulation.js** – fast, lightweight, built-in  
- **MuJoCo** – high-fidelity robotics physics  
- **Bullet** – rigid-body dynamics and collisions  
- **Drake** – research-grade robotics modeling  

This makes VRSTE suitable for both **education and professional robotics research**, a rare capability in web-based tools.

### True C++ Programming in the Browser
Unlike block-based or simplified scripting environments, VRSTE supports **real C++**, transpiled and executed asynchronously. This allows:

- Competitive robotics teams to practice real autonomous programming  
- Students to learn industry-standard languages  
- Professionals to prototype algorithms without installing toolchains

### Engine-Agnostic Robot Model
VRSTE maintains a consistent robot model for:

- Encoders  
- Odometry  
- Heading  
- Motor power → wheel velocity mapping  
- Sensor simulation (planned)  

This ensures consistent behavior across all physics engines — something missing in most simulators.

### Coordinate Plane Mode
VRSTE includes a **full coordinate-plane visualization** for:

- Autonomous path planning  
- Motion profiling  
- Pure pursuit and Ramsete-style controllers  
- Professional robotics workflows  

Essential for competitive robotics and advanced algorithm development.

### Browser-Native, Zero Install
Unlike many simulators that require heavy downloads or OS-specific dependencies, VRSTE runs entirely in the browser, making it accessible on:

- Windows  
- macOS  
- Linux  
- Chromebooks  
- Tablets (partial support)  

This dramatically lowers the barrier to entry for teams and classrooms.

---

## How VRSTE Compares to Other Tools

| Feature / Tool | VRSTE | VEXcode VR | Webots / Gazebo | FTC / FRC Simulators | Proprietary Educational Simulators |
|----------------|-------|------------|----------------|--------------------|----------------------------------|
| Language       | Real C++ | Simplified C++ subset | Multiple | Platform-specific | Drag & drop / simplified |
| Physics Engines | Modular / swappable | Fixed | Fixed | Fixed | Fixed |
| Coordinate Plane Mode | ✅ | ❌ | ❌ | Partial | ❌ |
| Browser-based | ✅ | ✅ | ❌ | ❌ | ❌ |
| Open-source / Extensible | ✅ | ❌ | Partially | ❌ | ❌ |

---

## Extensibility

VRSTE is designed from the ground up to be **community-extendable**:

- Add new physics engines  
- Add new robot models  
- Add new field types  
- Add new sensors  
- Add new UI tools  
- Add new programming libraries  

The architecture ensures that new modules can be added **without breaking existing functionality**.

---

## Vision

VRSTE aims to become the **standard open-source robotics simulator** for:

- Students learning robotics  
- Competitive teams practicing autonomous routines  
- Educators teaching programming and physics  
- Researchers prototyping algorithms  
- Professionals testing control systems  

By combining **accessibility, performance, and extensibility**, VRSTE bridges the gap between educational tools and professional robotics platforms.


