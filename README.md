# Custom Meshtastic Node (ESP32-S3 + E22-900M22S)

> **⚠️ PROJECT STATUS: WORK IN PROGRESS (PROTOTYPE PHASE)**  
> This project is under active hardware development and schematic design. Specifications, schematics, and BOM are continuously updated. Production-ready design files will be released after prototype verification.

---

## Overview

A standalone, custom **Meshtastic** node hardware implementation designed from the ground up. Shifted from early high-power PA concepts to a balanced, standard-power profile (+22 dBm / ~160 mW) for optimized thermal management and extended battery life. 

The core architecture utilizes the dual-core **ESP32-S3** with external antenna support (U.FL), providing abundant GPIOs, native USB OTG/JTAG, and 8 MB Octal PSRAM to accommodate future hardware expansions such as dedicated standalone keyboards and displays.

---

## Hardware Architecture & Key Specifications

* **MCU:** Espressif ESP32-S3-WROOM-1U-N16R8
  * Dual-core Xtensa 32-bit LX7 @ up to 240 MHz
  * 16 MB Quad SPI Flash & 8 MB Octal PSRAM
  * Integrated USB OTG & USB Serial/JTAG controller
  * External antenna connection via U.FL (IPEX) connector
  * 2.4 GHz Wi-Fi (802.11 b/g/n) & Bluetooth 5 (LE / Mesh)
  * Ample IO expansion capability for standalone peripherals
* **LoRa Transceiver:** Ebyte E22-900M22S
  * Semtech SX1262 architecture
  * Standard Meshtastic power output: up to +22 dBm (~160 mW)
  * Target frequency bands: Sub-GHz ISM (868/915 MHz)
  * Standard operating currents (optimized thermal profile, no discrete high-power external PA needed)
* **GNSS Engine:** u-blox MAX-M10S
  * Multi-constellation concurrent reception (GPS, GLONASS, Galileo, BeiDou)
  * Integrated TCXO and low-noise amplifier (LNA)
  * Ultra-low power consumption profile
* **Power & Charging Subsystem (In Progress):**
  * **Topology:** Dual 18650 Li-ion battery setup
  * **BMS / Protection:** Discrete battery management circuitry (overvoltage, undervoltage, overcurrent protection)
  * **Charging:** USB Type-C charging stage with standard CC termination resistors
  * **Power Distribution Network (PDN):** High-efficiency buck/LDO stages providing stable 3.3V rails for MCU, LoRa, and GNSS modules

---

## Engineering & Layout Notes

* **RF Path:** 50Ω coplanar waveguide with ground (CPW-G) layout referencing Layer 2 unbroken ground for sub-GHz RF output to the SMA connector.
* **Peripherals Headroom:** Pin multiplexing and bus allocations (I2C/SPI) are planned with reserve capacity to ensure glitch-free addition of display and keyboard peripherals without bus collisions or pin starvation.
* **Power Rail Decoupling:** Dedicated decoupling networks placed directly at the VCC pins of the SX1262 (E22) and ESP32-S3 modules to mitigate ripple and brownout risks.

---

## Development Roadmap & Status

- [x] **MCU Core Subsystem:** ESP32-S3-WROOM-1U-N16R8 schematic capture, pin planning, and symbol/footprint verification *(Completed)* edit: needs revision
- [x] **LoRa RF Subsystem:** E22-900M22S integration and RF pin mapping *(Completed)*
- [x] **GNSS Subsystem:** MAX-M10S integration, antenna circuit, and serial interface *(Completed)*
- [ ] **Power Management & Charging:** USB Type-C charging input, BMS protection circuit, and buck/LDO voltage regulation stages *(Draft / In Progress - actively being implemented)*
- [ ] **UI & Human Interface (HMI):** Display (E-ink / OLED / SPI LCD) and hardware keyboard integration *(Concept / Planning Phase)*
- [ ] **PCB Routing & Layer Stackup:** Final routing, 50Ω RF trace impedance matching, and design rule checks (DRC)
- [ ] **Prototype Assembly & Bring-up (Rev 1.0):** SMT assembly and bench-level power/signal testing
- [ ] **Meshtastic Custom Target:** Firmware configuration, custom pin definitions, and field range verification

---

## License

Hardware design files, schematics, and documentation will be licensed under an open hardware license (CERN-OHL or similar) upon hardware verification.
