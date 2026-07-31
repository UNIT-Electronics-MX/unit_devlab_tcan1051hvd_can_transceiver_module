
# DevLab: TCAN1051HVD CAN Transceiver Module


The TCAN1051HVD CAN Transceiver Module is a compact physical-layer interface between a CAN controller and a differential CAN bus. Based on the Texas Instruments TCAN1051HVD, it supports Classic CAN and CAN FD communication up to 2 Mbps, selectable 3.3 V or 5 V controller logic, onboard power regulation, CAN bus protection, and a 120 Ω termination network.

> **Note:** This module implements the CAN physical layer only. The host must provide a CAN controller or a microcontroller with an integrated CAN/TWAI peripheral.

<div align="center">
  <a href="#"><img src="https://img.shields.io/badge/version-1.0.0-blue.svg" alt="Version"></a>
  <a href="#"><img src="https://img.shields.io/badge/interface-Classic_CAN-lightgrey.svg" alt="Classic CAN"></a>
  <a href="#"><img src="https://img.shields.io/badge/interface-CAN_FD-lightgrey.svg" alt="CAN FD"></a>
  <a href="./LICENSE"><img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License"></a>
  <br>
</div>

<div align="center">
  <img src="./hardware/resources/unit_top_v_1_0_ue0085_TCAN1051HVD.png" width="450px" alt="Product Image">
  <p><em>TCAN1051HVD CAN Transceiver Module — UE0085</em></p>
</div>

<div align="center">

### Quick Setup


[<img src="https://img.shields.io/badge/Product%20Wiki-blue?style=for-the-badge" alt="Product Wiki" target="_blank">](https://unit-electronics-mx.github.io/unit_devlab_tcan1051hvd_can_transceiver_module/)
[<img src="https://img.shields.io/badge/Datasheet-green?style=for-the-badge" alt="Datasheet" target="_blank">](./docs/hardware/unit_product_reference_v_1_0_0_ue0085_tcan1051hvd_can_transceiver_module.pdf)
[<img src="https://img.shields.io/badge/Buy%20Now-orange?style=for-the-badge" alt="Buy Now" target="_blank">](https://uelectronics.com/)
[<img src="https://img.shields.io/badge/Getting%20Started-purple?style=for-the-badge" alt="Getting Started" target="_blank">](./hardware/README.md)

</div>

## Overview

| Feature / Component              | Details                                                                                      |
| -------------------------------- | -------------------------------------------------------------------------------------------- |
| **Communication**                | Classic CAN and CAN FD physical-layer interface up to 2 Mbps.                                |
| **Input Voltage**                | Module VIN range from 3.3 V to 5.0 V.                                                       |
| **Logic Voltage**                | Selectable 3.3 V or 5 V controller-side logic through VIO.                                  |
| **IC1 – TCAN1051HVD**            | High-speed, fault-protected CAN transceiver with separate VIO supply.                        |
| **IC2 – AP2112K**                | Onboard 3.3 V regulator.                                                                     |
| **IC3 – TPS61023**               | Onboard 5 V boost converter.                                                                 |
| **D1 – CAN Protection**          | PESD2CANFD24L-UX protection device on CANH and CANL.                                         |
| **D2 – Power LED**               | Onboard green power-status indicator.                                                        |
| **J1 – Controller Port**         | 1 mm-pitch connector for GND, VIN, CTX, and CRX.                                             |
| **J2 – CAN Bus Port**            | 3.81 mm screw terminal for CANH and CANL.                                                    |
| **JP1 / JP2 / JP3**              | Castellated connections for bus, logic, power, and control signals.                          |
| **JP4 / SB1 – VIO Selector**     | Solder selector for 3.3 V or 5 V controller logic.                                           |
| **CAN Termination**              | Onboard 120 Ω CAN termination network.                                                       |



## Applications

- Industrial automation and distributed control
- Robotics and mobile platforms
- Building and environmental control
- Automotive prototyping and diagnostics
- CANopen, DeviceNet, NMEA 2000, ISOBUS, and other CAN-based networks

## License

This product and its documentation are licensed under the MIT License.  
See [`LICENSE`](LICENSE) for details.

<div align="center">
  <sub>Template by UNIT Electronics • Customize this file for your product documentation.</sub>
</div>
