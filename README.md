# Cruise Control System — MATLAB/Simulink

<div align="center">

![MATLAB](https://img.shields.io/badge/MATLAB-Simulink-orange?style=for-the-badge)
![Controller](https://img.shields.io/badge/PID-Controller-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

**A PID-controlled cruise control system modelled and simulated in MATLAB/Simulink**

Analysing vehicle speed regulation with realistic engine dynamics.

[Architecture](#️-system-architecture) · [Math Model](#-mathematical-model) · [PID Parameters](#-pid-parameters) · [Results](#-results) · [Future Work](#-future-work)

</div>

---

## Overview

This project models a cruise control system that automatically maintains a desired vehicle speed of **60 km/h** while accounting for resistive forces. It uses a **PID controller** combined with a realistic engine model for accurate vehicle dynamics simulation.

---

## System Architecture

```
Desired Speed (Setpoint: 60 km/h)
            ↓
    Summation Block (Error)
            ↓
      PID Controller
            ↓
    Saturation Block (Throttle Limits)
            ↓
       Engine Force Gain
            ↓
  Net Force (F_engine − F_drag)
            ↓
      1/mass Gain (a = F/m)
            ↓
      Integrator (velocity)
            ↓
    Feedback → Summation Block
```

---

## Mathematical Model

**Equation of motion:**
```
m * (dv/dt) = F_engine − F_drag
```

**Engine force:**
```
F_engine = PID output × Throttle_max × Gear Ratio / R_wheel
         = PID output × 200 × 10 / 0.3
         = PID output × 6666.7
```

**Drag force (linear model):**
```
F_drag = Drag Gain × velocity = 10 × v
```

---

## PID Parameters

| Parameter | Value | Purpose |
|-----------|-------|---------|
| Proportional (P) | 0.5 | Reduces steady-state error |
| Integral (I) | 0.21 | Eliminates offset over time |
| Derivative (D) | 0.11 | Dampens overshoot |

---

## Physical Model Parameters

| Parameter | Value | Meaning |
|-----------|-------|---------|
| Vehicle Mass | 1000 kg | 1/mass gain = 0.001 |
| Drag Gain | 10 | Linear air resistance |
| Max Throttle | 200 | Engine throttle limit |
| Gear Ratio | 10 | Transmission ratio |
| Wheel Radius | 0.3 m | Force-to-torque conversion |

---

## Results

- Vehicle speed rises smoothly from 0 m/s and stabilises at 60 km/h
- Minimal overshoot and short settling time
- PID controller maintains constant speed effectively under linear drag

### Pros & Cons

| Pros | Cons |
|------|------|
| Simple and robust | Simplified drag model |
| Smooth & stable response | No road gradient or wind variation |
| Computationally inexpensive | PID tuned for specific conditions only |
| Easy to implement | No tire friction modelling |

---

## Future Work

- More realistic drag model (aerodynamic + rolling resistance)
- Engine torque curves and transmission shifts
- Adaptive PID or Model Predictive Control (MPC)
- Road gradient and wind resistance integration

---

## Tools Used

| Tool | Purpose |
|------|---------|
| MATLAB / Simulink | Modelling and simulation |
| PID Controller block | Speed regulation |
| Scope block | Result visualization |

---


---

## 🏷️ Tags

`MATLAB` `Simulink` `PID Controller` `Control Systems` `Cruise Control` `Vehicle Dynamics` `Modelling & Simulation`
