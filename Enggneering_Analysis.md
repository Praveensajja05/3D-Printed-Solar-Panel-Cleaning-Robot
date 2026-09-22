# Engineering and Structural Analysis

This document details the physical parameters, stability forces, and fatigue limits of the autonomous solar panel cleaning robot operating on a 21° inclined surface, as documented in dESIGN.docx[cite: 1].

## 1. System Parameters & Constants
| Parameter | Value |
| :--- | :--- |
| **Total Mass (m)** | 0.7 kg[cite: 1] |
| **Solar Panel Inclination (θ)** | 21°[cite: 1] |
| **Center of Gravity Height (h)** | 111 mm (0.111 m)[cite: 1] |
| **Track Width (Wheelbase, w)** | 180 mm (0.180 m)[cite: 1] |
| **Wheel Radius (r)** | 65 mm (0.065 m)[cite: 1] |
| **Motor Efficiency (η)** | 60%[cite: 1] |
| **Chassis Dimensions** | 240 mm x 180 mm x 3 mm[cite: 1] |

## 2. Stability Analysis
*   **Total Weight (W):** 6.867 N[cite: 1]
*   **Normal Force (N):** 6.41 N[cite: 1]
*   **Downslope Force (Fd):** 2.46 N[cite: 1]
*   **Static Overturning Moment:** 0.273 Nm[cite: 1]
*   **Restoring Moment (Mr):** 0.577 Nm[cite: 1]
*   **Static Factor of Safety:** 2.11 (Safe Condition)[cite: 1]
*   **Dynamic Factor of Safety:** 1.54 (Stable during motion)[cite: 1]

## 3. Traction and Movement
*   **Available Drive Force:** 1.086 N[cite: 1]
*   **Total Resistance Force:** 0.628 N (Rolling resistance + Brush drag)[cite: 1]
*   **Net Acceleration:** 0.654 m/s²[cite: 1]
*   **Minimum Coefficient of Friction required:** 0.42[cite: 1] (Standard rubber wheels provide ~0.60, ensuring adequate grip without slippage[cite: 1]).

## 4. Stress and Fatigue Analysis (PLA Chassis)
The chassis is subjected to static and cyclic loading during operation[cite: 1].
*   **Front Arm Root Stress:** Identified as the critical stress region[cite: 1]. The nominal bending stress is 6.47 MPa, with a maximum localized stress of 19.41 MPa[cite: 1].
*   **Material Strength:** PLA plastic has an Ultimate Tensile Strength (UTS) of 58 MPa[cite: 1]. 
*   **Structural Safety:** The maximum stress of 19.41 MPa provides a static safety factor of nearly 3[cite: 1].
*   **Fatigue Life Estimate:** Using a corrected endurance limit of 3.375 MPa, the calculated fatigue life under fully reversed cyclic loading is approximately 15,570 cycles[cite: 1].
