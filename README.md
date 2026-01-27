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

## VRSTE vs Professional Robotics Software

VRSTE is designed to feel like a **full robotics lab in your browser**, combining the accessibility of educational tools with the power and flexibility of professional robotics software.  

| Feature / Capability | VRSTE | Professional Robotics Software (e.g., Webots, Gazebo, ROS + RViz) |
|---------------------|-------|---------------------------------------------|
| Programming Language | Real C++ in browser | C++, Python, or proprietary scripting (requires local setup) |
| Editor | Monaco-powered, live transpilation | External IDE (VS Code, Eclipse, etc.) |
| Execution | Live, asynchronous runtime in-browser | Requires compilation, runtime often local or server-based |
| Physics Engines | Modular & swappable (Simulation.js, MuJoCo, Bullet, Drake) | Usually fixed per simulator; advanced engines require manual integration |
| Robot API | Engine-agnostic, consistent across physics engines | Engine-specific APIs; may require adaptation |
| Coordinate Plane Mode | Full XY grid, axes, real-time pose visualization | Usually available, but often requires setup and configuration |
| Installation | Browser-native, zero-install, cross-platform | Local installation, OS-dependent, may require GPU/driver setup |
| Extensibility | Community-driven: add engines, sensors, robot models, fields | Often limited to plugin system or source modifications |
| Target Users | Students, educators, competitive teams, researchers | Researchers, engineers, professional developers |
| Accessibility | Works on laptops, Chromebooks, partial tablet support | Desktop-only; often requires high-performance hardware |
| Open Source | ✅ Fully open & community-driven | Partially open or proprietary |

**Summary:** VRSTE bridges the gap between **classroom robotics and professional simulation environments**, offering a modern, extensible platform that’s accessible, yet powerful enough for research and competitive robotics.

## Who VRSTE Is For

VRSTE is designed to be **for everyone** — from hobbyists experimenting at home to competitive teams, researchers, and even top-tier professional robotics labs. It combines the accessibility of educational tools with the precision and extensibility needed for advanced robotics work.  

| Feature / User Level | Hobbyists / Students | Competitive Teams / Educators | Researchers / Professional Labs | Top-Security / Advanced Robotics |
|---------------------|-------------------|-------------------------------|--------------------------------|--------------------------------|
| Programming | Real C++ in-browser | Real C++ & advanced algorithms | C++/Python prototyping, engine-agnostic | High-fidelity simulation, custom physics integration |
| Editor | Monaco editor, simple UI | Live code transpilation, debugging | Full API access, async runtime | Extendable environment for custom robots and sensors |
| Physics Engine | Built-in Simulation.js | MuJoCo, Bullet (planned) | Swappable engines, high-accuracy physics | Custom engines, multi-robot simulation, research-grade models |
| Coordinate Plane Mode | Optional, visual guidance | Path planning, motion profiling | Real-time pose, autonomous routines | Full control for algorithm testing & sensor validation |
| Accessibility | Browser-native, zero install | Cross-platform, Chromebooks supported | High-performance optional | Can integrate with secure/proprietary networks |
| Extensibility | Add sensors, simple robots | Custom robot models, fields | New physics engines, advanced sensors | Full plugin & API access for complex robotics systems |
| Target Users | Beginners, hobbyists | Students, educators, competition teams | Researchers, professional engineers | Labs, defense or proprietary robotics teams |

**Summary:**  
VRSTE is a **universal robotics platform**, scaling from beginner-friendly simulations to professional-grade robotics testing. It gives **hobbyists a playground**, **students and teams a learning lab**, and **researchers and advanced developers the tools they need to prototype, test, and extend complex robotic systems** — all in the browser.



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

## Timeline & Roadmap

VRSTE is under active development, with the **first official version scheduled for release next month**. The project roadmap highlights key milestones and planned features:




