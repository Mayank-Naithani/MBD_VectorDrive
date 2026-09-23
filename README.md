# \# MBD\_VectorDrive: Field-Oriented Control (FOC) Smart Motor Controller

##### 

##### !\[Model-Based Design](https://img.shields.io/badge/Methodology-Model--Based%20Design%20%28MBD%22-blue)

##### !\[MATLAB Simulink](https://img.shields.io/badge/Simulation-MATLAB%20%2F%20Simulink-orange)

##### !\[KiCad PCB](https://img.shields.io/badge/Hardware-KiCad%203--Phase%20Inverter-green)

##### !\[FreeRTOS ESP32](https://img.shields.io/badge/Firmware-FreeRTOS%20%2F%20ESP32-red)

##### !\[CAN Bus](https://img.shields.io/badge/Protocol-CAN%20Bus%20Telemetry-purple)

##### !\[License](https://img.shields.io/badge/License-MIT-brightgreen)

##### 

### \## Executive Summary

##### \*\*MBD\_VectorDrive\*\* is an open-source, automotive-grade Field-Oriented Control (FOC) smart motor controller developed using \*\*Model-Based Design (MBD)\*\* workflows. The project integrates high-speed closed-loop vector control modeling, 3-phase power inverter hardware design, real-time deterministic task scheduling, and CAN bus telemetry.

##### 

##### Designed to meet tier-1 automotive and robotics hardware/firmware standards, this repository bridges theoretical control systems with production-ready C/C++ firmware auto-generated directly from MATLAB/Simulink models.

##### 

##### \---

##### 

### \## Technical Architecture \& System Specifications



##### &#x09;	 +----------------------------------------+

##### &#x20;                |         MATLAB / Simulink Model        |

##### &#x20;                |  - Clarke \& Park Transformations       |

##### &#x20;                |  - PI Current Loops (d-q decoupling)   |

##### &#x20;                |  - Space Vector PWM (SVPWM) Generator  |

##### &#x20;                +-------------------+--------------------+

##### &#x20;                                    | Embedded Coder

##### &#x20;                                    v

##### &#x20;                +----------------------------------------+

##### &#x20;                |        FreeRTOS / ESP32 Firmware       |

##### &#x20;                |  - High-Priority FOC Loop (10-20 kHz)  |

##### &#x20;                |  - ADC-PWM Center-Aligned Sync         |

##### &#x20;                |  - Telemetry \& CAN Broadcast Task      |

##### &#x20;                +-------------------+--------------------+

##### &#x20;                                    | SPI / PWM / ADC

##### &#x20;                                    v

##### &#x20;                +----------------------------------------+

##### &#x20;                |         KiCad Power Inverter PCB       |

##### &#x20;                |  - 3-Phase Bridge (6x N-Channel FETs)  |

##### &#x20;                |  - Half-Bridge Gate Drivers \& Shunts   |

##### &#x20;                |  - CAN Transceiver (SN65HVD230)        |

##### &#x20;                +----------------------------------------+



### \### Core Parameters

##### \* \*\*Control Algorithm:\*\* Field-Oriented Control (FOC) / Vector Control with $i\_d = 0$ flux decoupling.

##### \* \*\*Modulation Scheme:\*\* Space Vector Pulse Width Modulation (SVPWM) for max DC-bus voltage utilization.

##### \* \*\*Control Loop Execution:\*\* 10–20 kHz deterministic execution inside dedicated hardware timer interrupt.

##### \* \*\*Target Controller:\*\* Dual-Core ESP32 operating under FreeRTOS.

##### \* \*\*Power Stage:\*\* 3-phase half-bridge driver layout with low-side shunt current sensing amplifiers.

##### \* \*\*Communication Protocol:\*\* CAN 2.0B broadcast frame telemetry (RPM, phase current, bus voltage, thermal diagnostics).

##### 

##### \---

##### 

### \## Industry Skill Matrix

##### 

##### | Core Domain | Technology \& Tooling | Project Implementation |

##### | :--- | :--- | :--- |

##### | \*\*Model-Based Design\*\* | MATLAB, Simulink, Embedded Coder | Mathematical modeling of Clarke/Park transforms, SVPWM, and C/C++ auto-code generation. |

##### | \*\*Control Systems\*\* | FOC Vector Control | Decoupling $i\_a, i\_b, i\_c$ phase currents into independent flux ($i\_d$) and torque ($i\_q$) DC components. |

##### | \*\*Power Hardware\*\* | KiCad EDA | High-current 3-phase power stage layout, parasitic inductance minimization, thermal via stitching. |

##### | \*\*Embedded Systems\*\* | FreeRTOS, ESP32, ESP-IDF | Hardware interrupt synchronization, center-aligned PWM triggering, multithreaded task partitioning. |

##### | \*\*Automotive Networks\*\* | CAN Bus (SN65HVD230) | Hardware physical layer differential pair layout and real-time telemetry frame broadcasting. |

##### 

##### \---

##### 

### \## Repository Structure

##### 

##### ```text

##### MBD\_VectorDrive/

##### ├── sim\_matlab/          # MATLAB \& Simulink control models

##### │   ├── models/          # FOC loop, Clarke/Park, and SVPWM .slx files

##### │   ├── scripts/         # Motor parameter initialization scripts (.m)

##### │   └── generated\_code/  # Production C/C++ source generated via Embedded Coder

##### │

##### ├── hw\_kicad/            # KiCad EDA hardware design files

##### │   ├── schematics/      # Power stage, driver, and sensing schematics

##### │   ├── layout/          # 3-phase inverter board layout (.kicad\_pcb)

##### │   └── manufacturing/   # Gerbers, Drill files, BOM, Pick-and-Place data

##### │

##### ├── fw\_esp32/            # ESP32 FreeRTOS firmware project

##### │   ├── include/         # Driver headers \& auto-generated model interfaces

##### │   └── src/             # Peripheral drivers, FreeRTOS tasks, and CAN stack

##### │

##### ├── paper/               # Academic publication drafts \& validation data

##### │   ├── draft/           # IEEE transaction/conference LaTeX manuscript

##### │   └── plots/           # Current waveforms, THD analysis, and thermal capture

##### │

##### └── docs/                # Architecture diagrams and design specifications



### Experimental \& Research Goals



##### This project serves as an experimental platform for a prospective IEEE/Springer research publication:

##### 

##### 1\. Total Harmonic Distortion (THD) Analysis: Quantifying phase current THD under Space Vector PWM vs. conventional sinusoidal PWM.

##### 

##### 2\. Software-in-the-Loop (SIL) Validation: Comparing theoretical Simulink step responses against real-time phase current waveforms captured from physical shunts.

##### 

##### 3\. Interrupt Latency Profiling: Execution profiling of auto-generated C code running within a high-frequency FreeRTOS interrupt service routine (ISR).

##### 

### Author



##### Mayank Naithani – Electrical Engineer

##### 

##### GitHub: @Mayank-Naithani

##### 

##### Project Repository: MBD\_VectorDrive

##### 

##### License: This project is licensed under the MIT License - see the LICENSE file for details.

