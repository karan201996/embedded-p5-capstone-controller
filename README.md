# embedded-p5-capstone-controller  

## Overview  
This capstone project implements a configurable embedded controller with PID (proportional–integral–derivative) control, a command-line interface over UART, modular architecture, and testing infrastructure. The goal is to demonstrate proficiency in system design, real-time control, hardware–software integration, and continuous integration (CI) for embedded systems.  

The controller can adjust the setpoint and PID gains at runtime via UART commands, read sensor input (e.g., temperature or a simulated value), compute a control output using a PID algorithm, and drive an actuator (such as a fan or LED via PWM). The project includes unit tests for the PID algorithm and command parser, and a GitHub Actions workflow to build and test the firmware.  

## Hardware Requirements  
- ARM Cortex-M microcontroller (e.g., STM32F4 or STM32G4) with a PWM-capable timer.  
- Temperature sensor or simulated input.  
- Fan or LED as actuator (controlled via PWM).  
- UART-to-USB adapter for serial console.  
- Optional: oscilloscope or logic analyser for verifying control outputs.  

## Software Requirements  
- C/C++ compiler for the target MCU (e.g., `arm-none-eabi-gcc`).  
- CMake build system and Ninja.  
- FreeRTOS or a custom scheduler (optional).  
- Unit test framework such as CMocka for host-based testing.  
- Python (for CLI demonstration or plotting).  
- GitHub Actions configured for continuous integration.  

## Build & Flash Instructions  
1. Clone this repository and initialize any submodules.  
2. Configure the `toolchain.cmake` file to point to your ARM GCC toolchain.  
3. Create a build directory and run `cmake ..` with appropriate variables for your MCU, then build with `cmake --build .`.  
4. Flash the generated binary (`.elf` or `.bin`) to your MCU using ST‑Link (`st-flash write`) or another programmer.  
5. Connect the UART console to your PC and open a terminal (e.g., `minicom`) at the configured baud rate (e.g., 115200).  
6. Use UART commands to set the controller setpoint, adjust PID gains, and view status. Example commands:  

   ```  
   setpoint 30  
   kp 1.2  
   ki 0.5  
   kd 0.01  
   status  
   ```  

## Features  
- Modular architecture with separate layers for drivers, control logic, and interface.  
- Configurable PID control loop with tunable gains (Kp, Ki, Kd).  
- UART command‑line interface supporting parameter adjustment and status queries.  
- Optional RTOS tasks for sensor reading, control computation, and logging.  
- Host-based unit tests for the PID algorithm and command parser.  
- GitHub Actions workflow for building the firmware and running tests on each push.  
- Clear documentation and diagrams describing system architecture.  

## Demo  
1. Build and flash the firmware onto your MCU.  
2. Connect a UART terminal and power the board.  
3. Enter commands to configure the setpoint and PID gains. For example:  

   ```  
   setpoint 25  
   kp 0.8  
   ki 0.1  
   kd 0.05  
   ```  

4. Observe the actuator's PWM output adjusting to achieve the target setpoint (e.g., LED brightness or fan speed).  
5. Monitor status output (e.g., sensor reading, control output, error values) through the UART console.  

## Future Work  
- Add support for additional sensors and actuators.  
- Implement auto‑tuning of PID gains.  
- Support multiple control channels in parallel.  
- Integrate a web-based dashboard for remote control and monitoring.  
- Improve the command parser with command history and help functionality.
