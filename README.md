# Ship-Island Port Simulation

A multi-threaded Java simulation demonstrating synchronized vs unsynchronized thread behavior through a port docking system.

![Synchronized Mode](https://img.shields.io/badge/Mode-Synchronized-green)
![Unsynchronized Mode](https://img.shields.io/badge/Mode-Unsynchronized-red)

## 📋 Overview

This project simulates 20 ships attempting to dock at a single port that can only accommodate one ship at a time. It demonstrates the critical differences between synchronized and unsynchronized thread access to shared resources.

### Modes

- **Synchronized Mode**: Uses proper thread synchronization to ensure only one ship docks at a time. All ships complete their journey safely.
- **Unsynchronized Mode**: Allows race conditions where multiple ships may attempt to dock simultaneously, potentially causing crashes.

## 🎮 Features

- **20 concurrent ship threads** attempting to dock at a shared port
- **Visual simulation** with custom graphics for ships and port
- **Toggle between synchronized/unsynchronized modes** to observe race conditions
- **Real-time crash detection** in unsynchronized mode
- **Success tracking** showing ships docked vs ships attempted
- **Thread-safe counter updates** for simulation statistics

## 🚀 Getting Started

### Prerequisites

- Java Development Kit (JDK) 8 or higher
- Java Runtime Environment (JRE)

### Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/ship-island-simulation.git
cd ship-island-simulation
```

2. Ensure the asset images are in the root directory:
   - `boat.png`
   - `land.png`
   - `boat_land.png`

### Running the Simulation

#### Using JAR file:
```bash
java -jar ShipSimulation.jar
```

#### From source:
```bash
javac Question_3/*.java
java Question_3.ShipDemo
```

## 🎯 How to Use

1. **Start the simulation**: Press `SPACE` to launch all 20 ships
2. **Toggle modes**: Press `S` to switch between Synchronized and Unsynchronized modes
3. **Observe**: Watch ships navigate to the port and note the differences between modes

### Controls

| Key | Action |
|-----|--------|
| `SPACE` | Start/Restart simulation |
| `S` | Toggle Synchronized/Unsynchronized mode |

## 🏗️ Project Structure
```
ship-island-simulation/
├── src/
│   └── Question_3/
│       ├── ShipDemo.java      # Main entry point
│       ├── Panel.java         # GUI and rendering
│       ├── Ship.java          # Ship thread implementation
│       └── Port.java          # Port resource object
├── assets/
│   ├── boat.png              # Ship sprite
│   ├── land.png              # Empty port sprite
│   └── boat_land.png         # Port with docked ship sprite
├── README.md
└── LICENSE
```

## 🔧 Technical Details

### Synchronization Strategy

**Monitor Object**: The `Port` object is used as the monitor for thread synchronization.

**Rationale**: The port represents the shared resource that all ships are trying to access. Since only one ship can dock at a time, synchronizing on the port object ensures mutual exclusion and prevents race conditions. The port acts as a natural bottleneck and synchronization point for all ship threads.

### Key Components

- **Ship.java**: Extends `Thread`, implements both synchronized and unsynchronized docking logic
- **Port.java**: Shared resource with occupation flag
- **Panel.java**: Swing-based GUI with key listeners and rendering
- **ShipDemo.java**: Application entry point

### Synchronized Mode Implementation
```java
synchronized(port) {
    while (port.has_ship) {
        port.wait();
    }
    port.has_ship = true;
    // Dock at port
    port.notifyAll();
}
```

### Unsynchronized Mode Features

- Race condition detection with 50% bad timing simulation
- Collision detection when multiple ships move simultaneously
- 60% crash probability on collision
- Random backoff timers for retry attempts

## 📊 Statistics Tracked

- **Ships Successfully Docked**: Count of ships that completed docking safely
- **Ships Attempted**: Total number of ships that finished (successful + crashed)
- **Current Mode**: Display of active synchronization mode
- **Crash Detection**: Real-time visual warning when crashes occur

## 🎓 Educational Purpose

This project was created as part of a Data Structures and Algorithms course to demonstrate:

- Multi-threaded programming in Java
- Thread synchronization using monitors
- Race conditions and their consequences
- Producer-consumer patterns
- GUI programming with Swing

## 📝 Assignment Context

This is Question 3 from Assignment 1, worth 40% of the assignment grade. The project demonstrates understanding of:

- Thread creation and management
- Synchronized vs unsynchronized access to shared resources
- GUI design and event handling
- Thread-safe counter updates
- Wait/notify mechanisms for thread coordination

## 👤 Author

**Suemon Kwok**
- Student ID: 14883335
- Course: Data Structures and Algorithms

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Course: Data Structures and Algorithms


## 🐛 Known Issues

- Images must be in the root directory for proper loading
- Window focus must be on panel for keyboard input to register

## 🔮 Future Enhancements

- [ ] Add sound effects for docking and crashes
- [ ] Implement multiple ports
- [ ] Add ship priority system
- [ ] Create replay functionality
- [ ] Add statistics export feature

Question 3) Thread: ship-island(port) simulation (40%)
You need to design a ship-island(port) simulation. You are going to have at least 20 ships (this
has been provided in Panel Class). Each ship runs as a thread. They all need to get to a port at an
island. Port accepts only one ship at a time.
Question 3 project has two modes “Unsynchronized mode” and “Synchronized mode”. The ships
may crash under the “Unsynchronized mode” because of race conditions. It shall run safely
under the “Synchronized mode”.
 Design YOUR OWN GUI of the project.
 Ship and island(port) images are loaded. (2%)
 Each ship is a thread. (5%)
 Ships move to the island after type “space” key. (Line 91 in Panel class to check which
key is typed) (5%)
 Island image changes when a ship arrives. (2%)
 Ship stays at island(port) for 1 second. (5%)
 Develop two modes (“Unsynchronized mode” and “Synchronized mode”). (4%)
 In both modes, ships check whether the port is available. (2%)
 “Unsynchronized mode” (5%)
o Ships check the port is available and no other ships are moving before it moves
to the port (Allows race conditions happen).
o Ships may crash if there are more than one ship move to port at a time.
o Your program detects and prints message on the GUI when ships crash.
o port icon changes when a ship arrives.
 “Synchronized mode” (6%)
o You can synchronize your blocks of code or methods in your Ship Class.
o Only one ship moves at a time. (NO race conditions)
o All ships must finish the jobs safely.
 Answer the following questions in your Ship class (put question and your answer on the
first line of your code). (4%)
 “What is your monitor object? And why?”
You don’t need to do anything of the Port Class, and NO “synchronized” in Panel Class.
