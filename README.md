# Autonomous Solar Panel Cleaning Robot

This repository contains the control software and structural design analysis for an autonomous solar panel cleaning robot, developed by Group 10 at the Department of Mechanical Engineering, IIT Indore. The system automates the removal of dust and dirt from solar installations, significantly reducing human labor, maintenance costs, and cleaning time while improving overall energy generation efficiency. 

## Project Overview

The robot navigates across solar panel surfaces utilizing a motorized drive system and specialized cleaning mechanism. It relies on edge-detection sensors to autonomously map the panel grid, turning and shifting rows dynamically until the entire surface is cleaned. 

**Development Team (IIT Indore):** 
Ch. Prajay Verma, B. Samith Lal, B. Santhosh, M. Naveen, R. Manthru Naik, R. Yogendhra Babu, S. Manjunatha, S. Praveen, Y. Akshay.

**Key Capabilities:**
*   **Autonomous Navigation:** Utilizes four IR obstacle sensors to detect panel edges and row boundaries, ensuring the robot does not fall off the inclined surface.
*   **Automated Cleaning:** A 12V water pump and motorized brush system are toggled via an onboard relay to actively scrub the panel.
*   **High-Traction Drive:** Driven by four high-torque BO motors and geared wheels, configured to maintain grip on a standard $21^\circ$ solar panel inclination.
*   **Lightweight Chassis:** Built from Polylactic Acid (PLA), minimizing the dynamic overturning moment while maintaining a total mass of 0.7 kg.

## Hardware Architecture

The structural body is designed using CAD and 3D printed with PLA, measuring 240.00 mm in length, 180.00 mm in width, and 3.00 mm in thickness. The following electronic and mechanical components are integrated into the chassis:

| Component | Specification / Function |
| :--- | :--- |
| **Arduino Uno R3** | ATmega328P microcontroller operating at 5V; serves as the central control unit. |
| **L298N Motor Driver** | Dual H-Bridge module used to control the direction and speed of the four drive motors. |
| **IR Obstacle Sensors** | 4 units placed at the Front Left (FL), Front Right (FR), Back Left (BL), and Back Right (BR) to detect edges and row limits. |
| **2-Channel Relay** | 5V electromagnetic switching module utilized to activate the 12V water pump and cleaning brushes. |
| **BO Motors & Wheels** | 4 high-torque geared motors providing locomotion across the inclined panel surface. |
| **LM2596 Buck Converter** | DC-DC step-down voltage regulator ensuring stable voltage supply to the logic components. |
| **18650 Li-ion Batteries** | 4 rechargeable 3.7V batteries powering the entire system. |

**Pin Configuration:**
*   **Motor Driver:** ENA (Pin 5), ENB (Pin 6), IN1 (Pin 8), IN2 (Pin 9), IN3 (Pin 10), IN4 (Pin 11)
*   **Relay (Pump/Brush):** Pin 7
*   **Sensors:** Front Left (Pin 2), Front Right (Pin 3), Back Left (Pin 4), Back Right (Pin 12)

## Software & State Machine

The robot's logic is governed by a finite state machine programmed in C++ for the Arduino platform. The loop continuously evaluates sensor inputs to transition between the following operational states:

1.  **STARTUP (State 0):** The robot initializes and moves forward blindly for 1.5 seconds to establish its position on the panel before activating the sensor array.
2.  **MOVE_FORWARD (State 1):** The default cleaning state. Both tracks move forward via PWM control. If the front sensors (FL and FR) detect an edge, the robot immediately stops and transitions to reversing.
3.  **REVERSING (State 2):** The robot backs away from the detected edge for 800ms. It uses a `turnCount` variable to alternate between clockwise and counter-clockwise 180-degree turns to traverse the panel in a serpentine pattern.
4.  **TURN_CW (State 3) / TURN_CCW (State 4):** Executes a sharp zero-radius turn by driving the left and right wheels in opposite directions. The turn times are hardcoded to calibrate a precise 180-degree rotation.
5.  **ROW_SHIFT (State 5):** The robot moves forward briefly to align with the next uncleaned row. If the back sensors (BL or BR) trigger during this phase, it indicates the end of the panel array, transitioning the system to the final state.
6.  **DONE (State 6):** All drive motors are halted, the relay deactivates the cleaning mechanisms, and the system terminates the run.

## Engineering & Structural Analysis

Comprehensive engineering analyses were conducted to guarantee the system's stability and durability on a standard $21^\circ$ solar panel inclination. 

*   **Static & Dynamic Stability:** The normal force securing the robot to the panel is 6.41 N. The static restoring moment (0.577 Nm) easily overcomes the static overturning moment (0.273 Nm), resulting in a static factor of safety of 2.11. Under active acceleration (0.654 m/s²), the dynamic factor of safety remains stable at 1.54. 
*   **Traction Requirements:** To prevent slipping, the system requires a minimum coefficient of friction of $\mu_{min} = 0.42$. Standard rubber wheels provide an approximate friction coefficient of 0.60, ensuring sufficient grip without slippage.
*   **Fatigue & Stress Limits:** The PLA chassis experiences maximum localized stress at the front support arms, measured at 19.41 MPa. Given PLA's ultimate tensile strength of 58 MPa, this yields a structural safety factor of approximately 3. Using the corrected endurance limit (3.375 MPa) and the material's S-N curve equation ($S = 628.88(N)^{-0.3603}$), the estimated fatigue life of the chassis under fully reversed cyclic loading is approximately 15,570 cycles.
