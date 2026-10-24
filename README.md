# TIRC 2023 Autonomous Sumo Robot

An autonomous sumo robot developed for the **TIRC 2023 International Robot Competition**. The robot uses ultrasonic sensors to detect and track opponents, a servo-driven lifting hook to gain a mechanical advantage, and an infrared sensor to detect the boundary of the arena. It runs on an Arduino Uno R3 with custom 3D-printed chassis components.

**Competition Achievement: 3rd Place Overall**

## Project Overview

The goal of this project was to design and build an autonomous sumo robot capable of detecting opponents, approaching them, and pushing them out of the competition arena without human intervention.

The robot integrates embedded C++ programming, distance sensing, motor control, signal filtering, and custom mechanical design into a single autonomous system.

## Features

- **Autonomous Opponent Detection:** Three HC-SR04 ultrasonic sensors scan the front of the robot to detect opponents across different directions.
- **Median Filtering:** Takes three distance measurements and uses a median filter to reduce the effect of noisy or inconsistent ultrasonic readings.
- **Target Tracking and Attack:** Uses distance measurements to determine the opponent's direction, turns towards the target, and moves forward to attack.
- **Servo-Driven Lifting Hook:** When an opponent is detected within 20 cm, an SG90 servo activates a lifting hook to lift or destabilise the opponent while the robot advances.
- **Adaptive Attack Behaviour:** If the opponent escapes the hook or is no longer detected, the robot stops its forward attack and resumes searching for a target.
- **Boundary Detection and Recovery:** A front-mounted infrared sensor detects the arena boundary. When the boundary is detected, the robot turns approximately 140 degrees and moves forward to return to the arena.
- **PWM Motor Control:** Two drive motors are controlled independently through a BTS7960 motor driver, allowing differential steering and adjustable motor speed.
- **Custom Mechanical Design:** The chassis and structural components are self-designed and 3D-printed.

## Hardware

| Component | Purpose |
|---|---|
| Arduino Uno R3 | Main microcontroller for sensing, decision-making, and control |
| 3 × HC-SR04 Ultrasonic Sensors | Front-facing opponent detection and distance measurement |
| 1 × Infrared (IR) Sensor | Detecting the arena boundary |
| BTS7960 Motor Driver | Driving the two motors with PWM speed control |
| SG90 Servo Motor | Operating the lifting hook |
| DC Drive Motors | Providing propulsion and steering |
| Custom 3D-Printed Parts | Chassis, sensor mounts, and mechanical structures |

## Software

- **Programming Language:** C++
- **Development Platform:** Arduino IDE
- **Microcontroller Framework:** Arduino Core
- **Control Techniques:** PWM motor control, differential steering, threshold-based decision-making, and servo positioning
- **Signal Processing:** Three-sample median filtering for ultrasonic distance measurements

## System Architecture

The robot follows a sensor-driven control loop:

1. Read distance measurements from the three front-facing ultrasonic sensors.
2. Apply a median filter to each sensor's three measurements.
3. Determine whether an opponent is present and estimate its direction.
4. Turn towards the target and approach it.
5. If the target is within 20 cm, activate the servo-driven lifting hook and continue the attack.
6. If the target is lost or escapes the hook, stop the forward attack and return to target-search mode.
7. Continuously monitor the front IR sensor. If the arena boundary is detected, interrupt the attack, turn approximately 140 degrees, and move forward to recover.

Boundary avoidance takes priority over opponent engagement to reduce the risk of leaving the arena.

## Mechanical Design

The robot's chassis and structural components were custom-designed and 3D-printed. This allowed the mechanical layout to be tailored to the sensor positions, motor arrangement, and lifting-hook mechanism.

<img width="1141" height="768" alt="image" src="https://github.com/user-attachments/assets/8395197d-886f-4ecc-a458-2409c5cf815b" />



## How to Run

1. Install the [Arduino IDE](https://www.arduino.cc/en/software).
2. Connect the Arduino Uno R3 to your computer.
3. Open the project `.ino` file in the Arduino IDE.
4. Select **Arduino Uno** under Tools → Board.
5. Select the correct serial port.
6. Verify that the sensor, motor driver, servo, and IR sensor wiring matches the pin assignments in the code.
7. Upload the firmware to the Arduino Uno R3.
8. Test the sensors, motor directions, servo mechanism, and boundary detection in a safe test environment before competition use.

**Note:** The original source code is currently unavailable. The implementation details above describe the intended system behaviour; the actual pin assignments, servo positions, motor speeds, and control logic should be confirmed against the recovered or rewritten firmware.
