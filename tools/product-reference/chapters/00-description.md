## Description

The **DevLab TCAN1051HVD CAN Transceiver Module** is a compact physical-layer
interface for Classic CAN and CAN FD networks. It connects a microcontroller or
stand-alone CAN controller to the differential CAN bus through the CTX (TXD),
CRX (RXD), CANH, and CANL signals.

The module is built around the Texas Instruments TCAN1051HVD, a fault-protected
high-speed CAN transceiver with a separate VIO supply. An onboard boost
converter and 3.3 V regulator generate the transceiver and logic rails from VIN.
The VIO selector allows direct use with either 3.3 V or 5 V controllers.

![](hardware/resources/unit_top_v_1_0_ue0085_TCAN1051HVD.png){width=6.2in}

> This module implements the CAN physical layer only. The host must provide a
> CAN controller or a microcontroller with an integrated CAN/TWAI peripheral.

### Applications

- Industrial automation and distributed control
- Robotics and mobile platforms
- Building and environmental control
- Automotive prototyping and diagnostics
- CANopen, DeviceNet, NMEA 2000, ISOBUS, and other CAN-based networks

### Hardware Features

- TCAN1051HVD high-speed, fault-protected CAN transceiver
- Classic CAN and CAN FD operation up to 2 Mbps
- Selectable 3.3 V or 5 V logic interface (VIO)
- Onboard TPS61023 5 V boost converter and AP2112K 3.3 V regulator
- Switchable split 120 Ω termination (2 × 60 Ω with 4.7 nF center capacitor)
- PESD2CANFD24L-UX protection device on CANH and CANL
- 22 Ω series resistors on CTX and CRX
- 3.81 mm screw terminal for the CAN bus
- 4-pin, 1 mm-pitch connector for VIN, GND, CTX, and CRX
- Castellated headers for breadboard, carrier-board, or direct-wire integration
- Power indicator LED and exposed regulator enable signal

