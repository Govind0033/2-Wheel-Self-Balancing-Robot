# 2-Wheel Self-Balancing Robot

A two-wheeled inverted-pendulum robot that keeps itself upright using real-time tilt feedback from an MPU6050 IMU and a PID controller running on an Arduino Nano. Bluetooth control is added through an HC-05 module.

> Project Lead | August 2024
> An IEEE-format research paper was written for this project (see [Research Paper](#research-paper)).

---

## Overview

A self-balancing robot is an unstable system: without active control it falls over. The robot reads its tilt angle, computes a correction with a PID controller, and drives the motors to move the wheels under its center of gravity, keeping it upright.

Compact, low-cost and nonlinear, this platform is useful for education, research, embedded control, sensor fusion, and mobile robotics.

**Result:** the robot reaches stable balance within **3 seconds** of activation.

---

## Features

- Real-time tilt estimation from the MPU6050 (gyroscope + accelerometer)
- PID control loop for motor correction
- Arduino Nano based controller
- Wireless control via HC-05 Bluetooth module
- Circuit simulation in Wokwi, schematic/PCB in Easy EDA, wiring diagrams in Fritzing

---

## Hardware Components

| Component | Purpose |
|---|---|
| Arduino Nano | Main microcontroller |
| MPU6050 | 3-axis gyroscope + 3-axis accelerometer (tilt sensing) |
| Motor driver module | Drives the DC motors (e.g., L298N / L293D, update to yours) |
| 2 x DC geared motors with wheels | Locomotion |
| HC-05 Bluetooth module | Wireless control |
| Battery pack | Power supply (update voltage/type) |
| Chassis | Robot frame |

---

## Software and Tools

- **Arduino IDE** (C/C++)
- **PID control** for balancing
- **Wokwi** for circuit simulation
- **Easy EDA** for schematic and PCB design
- **Fritzing** for circuit and wiring diagrams

---

## System Architecture

```
 MPU6050 --(I2C)--> Arduino Nano --(PWM/DIR)--> Motor Driver --> DC Motors
                        ^
                        |
                 HC-05 (UART/Bluetooth)
```

1. The **MPU6050** measures acceleration and angular velocity.
2. The Arduino estimates the **tilt angle** from this data.
3. The **PID controller** computes the correction from the angle error.
4. The **motor driver** applies the correction to the wheels.
5. The **HC-05** receives commands from a phone or other Bluetooth device.

---

## Pin Connections

> Update this table to match your wiring.

| Module | Pin | Arduino Nano Pin |
|---|---|---|
| MPU6050 | VCC | 5V / 3.3V |
| MPU6050 | GND | GND |
| MPU6050 | SDA | A4 |
| MPU6050 | SCL | A5 |
| Motor Driver | IN1 | D? |
| Motor Driver | IN2 | D? |
| Motor Driver | IN3 | D? |
| Motor Driver | IN4 | D? |
| Motor Driver | ENA / ENB | D? (PWM) |
| HC-05 | TX | D? (RX) |
| HC-05 | RX | D? (TX) |

---

## PID Controller

The controller output is:

```
output = Kp * error + Ki * integral(error) + Kd * d(error)/dt
```

where `error = setpoint_angle - measured_angle`.

| Parameter | Value |
|---|---|
| Kp | _your value_ |
| Ki | _your value_ |
| Kd | _your value_ |
| Setpoint angle | _your value_ |

**Tuning approach:** _(describe, e.g., manual tuning: raise Kp until the robot oscillates, add Kd to damp, then a small Ki to remove drift)._

**Sensor fusion:** _(state your method, e.g., complementary filter, Kalman filter, or MPU6050 DMP)._

---

## Getting Started

### Prerequisites
- Arduino IDE
- Libraries: `Wire` (built in), plus your MPU6050 library (e.g., `MPU6050` by Electronic Cats / `I2Cdevlib`) and your PID library if used

### Steps
1. Assemble the hardware following the schematic in `/hardware`.
2. Clone this repository:
   ```bash
   git clone https://github.com/<your-username>/<repo-name>.git
   ```
3. Open the sketch in Arduino IDE.
4. Select **Board:** Arduino Nano and the correct **Port**.
5. Calibrate the MPU6050 offsets with the robot held upright.
6. Upload the sketch.
7. Place the robot upright and power it on. It should stabilize within about 3 seconds.

---

## Repository Structure

> Adjust to match your repo.

```
.
├── src/            # Arduino sketch (.ino)
├── hardware/       # Schematic, PCB (Easy EDA), Fritzing files
├── simulation/     # Wokwi project
├── docs/           # Research paper, images
└── README.md
```

---

## Results

- Stable balance within **3 seconds** of activation
- Add photos / GIF of the robot balancing here
- Add a plot of tilt angle vs. time if you have one

---

## Research Paper

**Title:** _Design, Modelling and Implementation of a Self-Balancing Robot Using Arduino Nano and PID Control_ _(update to your exact title)_

**Status:** _(Published in [venue, year] / Submitted / Authored)_

**Abstract:** The paper presents the design, modelling and implementation of a self-balancing robot built with an Arduino Nano and an HC-05 Bluetooth module. It covers the hardware description and control logic, system architecture, PID controller design and tuning, and hardware-software integration. Wokwi was used for circuit simulation, Easy EDA for schematic and PCB design, and Fritzing for circuit design and wiring. Owing to its low cost and rich nonlinear dynamics, the work is also relevant to human-robot interaction, self-navigation and mobile robotics.

---

## Future Improvements

- Speed and direction control through a mobile app
- Encoder feedback for position and speed hold
- Kalman filter for improved angle estimation
- Larger-scale version as a personal transport platform

---

## Author

Govind Gautam

## License

This project is licensed under the MIT License. Add a `LICENSE` file if you choose this.
