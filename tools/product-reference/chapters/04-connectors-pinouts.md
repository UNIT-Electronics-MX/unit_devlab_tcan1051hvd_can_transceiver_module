
## 4 Connectors and Pinouts

The UE0085 module provides controller-side logic connections,
differential CAN bus terminals, and castellated contacts
for integration with external hardware.

The following pinout identifies the available signals,
power connections, and onboard configuration options.

![](hardware/resources/unit_pinout_v_1_1_ue0085_tcan1051hvd_en.png){width=5.2in}

### **4.1 Signal Reference** {.section-page}

| Label | Direction | Description |
|---|---|---|
| VIN | Power input | Module input supply, 3.3 V to 5.0 V |
| GND | Power | Common module and bus reference |
| CTX | Input | Controller transmit signal; LOW = dominant |
| CRX | Output | Controller receive signal; LOW = dominant |
| CANH | Bus I/O | CAN high bus line |
| CANL | Bus I/O | CAN low bus line |
| EN | Input | 5 V boost-converter enable; LOW disables the generated supply rails |
| 5V | Power output | Generated 5 V transceiver rail |
| 3V3 | Power output | Generated 3.3 V logic rail |
| VIO | Power | Selected transceiver logic supply (3.3 V or 5 V) |

The CTX and CRX signals operate at the voltage level
selected through VIO. The host controller must use
compatible logic levels. The module implements the CAN physical layer only.
An external CAN controller or a microcontroller with
an integrated CAN peripheral is required.

### **4.2 J1 Controller Connector** {.section-page}

J1 is a 4-position, 1 mm-pitch connector providing
power and communication signals to the host controller.

Use the bottom-side silkscreen to confirm the pin
order before connecting a cable.

| Signal | Connection |
|---|---|
| GND | Host ground |
| VIN | Host power supply |
| CTX | Host CAN TX output |
| CRX | Host CAN RX input |

Verify the cable orientation and signal order before
connecting the module to an external controller.

### **4.3 J2 CAN Bus Terminal** {.section-page}

J2 is a 2-position, 3.81 mm screw terminal providing
the differential CAN bus connections.

| Position | Signal | Connection |
|---|---|---|
| Upper | CANH | CAN bus high line |
| Lower | CANL | CAN bus low line |

Use twisted-pair wiring for CANH and CANL.
Maintain correct bus polarity and minimize
stub lengths to preserve signal integrity.

### **4.4 Castellated Headers** {.section-page}

The castellated contacts provide access to controller
signals, CAN bus connections, regulated power rails,
and configuration signals.

These contacts support direct wiring, carrier-board
integration, and prototyping applications.

![](hardware/resources/unit_top_v_1_0_ue0085_TCAN1051HVD.png){width=4.0in}

The contact labels are printed on the board silkscreen.
Refer to the pinout illustration for signal identification.

### **4.5 Configuration Jumpers** {.section-page}

The module includes two jumper-selectable functions:
VIO logic-voltage selection and CAN bus termination.

| Configuration | Selection | Function |
|---|---|---|
| VIO | 3V3 | Sets the transceiver logic interface to 3.3 V |
| VIO | 5V | Sets the transceiver logic interface to 5 V |
| CAN termination | Enabled | Connects the onboard 120 Ω termination network |
| CAN termination | Disabled | Disconnects the selectable termination network |

**VIO Selection**

Select the VIO voltage according to the logic level
of the connected host controller.

Only one VIO voltage selection must be active at a time.
Connecting both the 3.3 V and 5 V rails together may
damage the module or the host controller.

**CAN Bus Termination**

Enable the onboard 120 Ω termination only when the
module is installed at a physical end of the CAN bus.

For intermediate nodes, leave the termination disabled.

A correctly terminated CAN bus normally uses one
120 Ω termination at each physical end of the main bus.

The termination network and jumper configuration
must match the released hardware assembly revision.
