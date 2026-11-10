# FlightQPlanner

FlightQPlanner is a ground control station and flight planning application designed for UAVs. Built with **Qt6** for a modern, responsive user interface and **MAVSDK** for robust communication with MAVLink-compatible drones, this application allows for telemetry monitoring, mission planning, and offboard control.

## Features

* **Real-time Telemetry:** Monitor altitude, speed, battery life, and GPS status.

* **Offboard Control:** Execute custom flight loops and maneuvers.

* **Simulation Support (In Development):** Full integration with SITL (Software In The Loop) environments like PX4 or ArduPilot is currently a work in progress. 

* **Cross-Platform UI:** Built on Qt6, ensuring compatibility across Windows, macOS, and Linux.

## Prerequisites

Before you build the project, ensure you have the following installed:

* **C++17** (or higher) compatible compiler

* **CMake** (version 3.14+)

* **Qt6** (Core, Gui, Widgets modules minimum)

* **MAVSDK** C++ library

## Building the Project

1. **Clone the repository:**

   ```
   git clone https://github.com/kurwei/FlightQPlanner.git
   cd FlightQPlanner
   ```

2. **Create a build directory:**

   ```
   mkdir build
   cd build
   ```

3. **Configure with CMake:**

   ```
   cmake -DCMAKE_PREFIX_PATH="/path/to/Qt6;/path/to/MAVSDK" ..
   ```

   *(Note: Update the paths to point to your local Qt6 and MAVSDK installations if they are not in your system path).*

4. **Build the application:**

   ```
   cmake --build .
   ```

## Usage

1. **Power on your physical drone** *(Note: Simulator support is currently in development)*.

2. **Run FlightQPlanner:**

   ```
   ./FlightQPlanner
   ```

3. Use the connection settings in the UI to connect to your drone via UDP, TCP, or Serial.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request or open an Issue for bug reports and feature requests.

## License

This project is licensed under the [MIT License](LICENSE) - see the LICENSE file for details.
