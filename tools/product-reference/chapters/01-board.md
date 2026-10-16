
## **1 The Board**

The DevLab TCAN1051HVD CAN Transceiver Module (UE0085) provides
a physical-layer interface between a CAN-capable host controller
and a differential CAN bus.

The design separates the controller-side logic interface from
the CANH and CANL bus signals. Controller connections are
available through a 4-pin JST-compatible connector and
castellated contacts, while the CAN bus is accessible through
a 3.81 mm screw terminal and dedicated board contacts.

An onboard 5 V boost converter, 3.3 V linear regulator,
selectable logic voltage, and CAN bus protection circuitry
support integration with 3.3 V and 5 V controllers.

### **1.1 Accessories** {.section-page}

The UE0085 module is supplied with the following accessories:

| Accessory | Quantity | Purpose |
|---|---:|---|
| DevLab TCAN1051HVD CAN Transceiver Module (UE0085) | 1 | Main CAN physical-layer interface board |
| JST/Qwiic-compatible cable (AR4561) | 1 | Connects the module to the host controller through the 4-pin interface |
| Single-row male header, 1 × 9 pins | 1 | Provides solderable connections for board integration |
| Single-row male header, 1 × 8 pins | 1 | Provides additional solderable connections |
| Jumper bridge, 2.54 mm | 2 | Configures onboard jumper-selectable functions |

The supplied headers and jumper bridges may require
installation depending on the intended application.

Verify connector orientation, signal assignment, and
voltage compatibility before connecting the module.

### **1.2 Board Identification**

| Item | Value |
|---|---|
| Product | DevLab TCAN1051HVD CAN FD Transceiver Breakout |
| Brand / company | UNIT Electronics |
| Board ecosystem | DevLab |
| Product type | High-speed CAN / CAN FD physical-layer transceiver module |
| Main transceiver | Texas Instruments TCAN1051HVD |
| Power converter | TPS61023 |
| Voltage regulator | AP2112K-3.3 |
| Logic interface | Selectable 3.3 V / 5 V |
| CAN interface | CANH and CANL differential bus |
| Manufacturer Part Number (MPN) | UE0085 |
| Available schematic | Revision 1 |
| Product Reference | Version 1.0.0 |

Board, schematic, pinout, and documentation revisions are
controlled independently.

### **1.3 Identified Assemblies**

| Assembly | Function | Source status |
|---|---|---|
| TCAN1051HVD (IC1) | High-speed CAN physical-layer transceiver supporting Classic CAN and CAN FD up to 2 Mbps | Identified in the schematic and product reference |
| TPS61023 (U1) | Boost converter generating the regulated 5 V rail from VIN | Identified in the schematic |
| AP2112K-3.3 (U2) | Linear regulator generating the 3.3 V rail from the 5 V supply | Identified in the schematic |
| PESD2CANFD24L-UX (D1) | Transient protection for CANH and CANL | Identified in the schematic |
| Green LED (D2) | Indicates the presence of the regulated 5 V supply | Identified in the schematic |
| Controller connector (J1) | 4-pin, 1 mm-pitch connection for VIN, GND, CTX, and CRX | Identified in the schematic and pinout |
| CAN bus terminal | 2-position, 3.81 mm screw terminal for CANH and CANL | Identified in the schematic |
| Split termination network (R2, R3, C5) | Provides 120 Ω CAN bus termination using two 60 Ω resistors and a 4.7 nF center capacitor | Identified in the schematic |
| Termination selector (JP1) | Controls the connection of the onboard termination network | Identified in the schematic; assembly configuration requires verification |
| VIO selector (JP4) | Selects 3.3 V or 5 V transceiver logic levels | Identified in the schematic and pinout |
| Enable signal (EN) | Controls the TPS61023 boost converter | Identified in the schematic and pinout |
| Castellated contacts | Provide access to power, control, and CAN bus signals | Identified in the board documentation |

The module implements the CAN physical layer only.
A host microcontroller with an integrated CAN controller
or an external CAN controller is required for communication.


### **1.4 Board Views** {.section-page}

![](hardware/resources/unit_topology_v_1_0_ue0085_TCAN1051HVD.png){width=5.2in}

**Views of Board Topology**

The top view identifies the main integrated circuits,
controller and CAN bus connectors, power circuitry,
and castellated contacts.

The bottom view shows the VIO solder selector,
board identification markings, and controller
signal references.

| Reference | Description | Location |
|---|---|---|
| IC1 | TCAN1051HVD CAN transceiver | Top |
| IC2 | AP2112K-3.3 linear regulator | Top |
| IC3 | TPS61023 boost converter | Top |
| J1 | 4-pin controller interface connector | Top |
| J2 | 2-position CAN bus screw terminal | Top |
| JP1 | CAN bus termination selector | Top |
| JP2 | Controller and power castellated contacts | Top |
| L1 | Boost converter inductor | Top |
| SB1 | VIO solder selector | Bottom |
| QR code | Board identification and product reference | Bottom |
| GND, VIN, CTX, CRX | Controller interface signal markings | Bottom |

The board topology illustration identifies component
placement and interface locations. Electrical connections
and component values are defined by the released schematic.

Board artwork and schematic revisions must be verified
independently before manufacturing or hardware modification.

### **1.5 Handling** {.section-page}

Use standard electrostatic discharge (ESD) precautions
when handling or installing the module.

Remove power before installing headers, changing jumper
positions, or modifying the VIO selection.

Select only one VIO voltage level at a time. Connecting
the 3.3 V and 5 V rails together may damage the module
or the connected host.

Verify CANH and CANL polarity before connecting the
module to an active CAN network.

Enable the onboard 120 Ω termination only when the
module is installed at a physical end of the CAN bus.
Intermediate nodes must not introduce additional
termination resistance.

Do not connect external power directly to the regulated
3V3 or 5V outputs unless the application has been
specifically validated for that configuration.

The module does not provide galvanic isolation between
the host controller and the CAN bus.
