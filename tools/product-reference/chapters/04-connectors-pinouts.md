## 4 Connectors and Pinouts

### 4.1 Signal Reference

| Label | Direction | Description |
|---|---|---|
| VIN | Power input | Module input supply, 3.3 V to 5.0 V |
| GND | Power | Common module and bus reference |
| CTX | Input | Controller transmit signal; LOW = dominant |
| CRX | Output | Controller receive signal; LOW = dominant |
| CANH | Bus I/O | CAN high bus line |
| CANL | Bus I/O | CAN low bus line |
| EN | Input | 5 V boost-converter enable; LOW disables the module |
| 5V | Power output | Generated 5 V transceiver rail |
| 3V3 | Power output | Generated 3.3 V logic rail |
| VIO | Power | Selected transceiver logic supply (3.3 V or 5 V) |

### 4.2 J1 Controller Connector

J1 is a 4-position, 1 mm-pitch connector. Use the bottom-side silkscreen to
confirm pin order before connecting a cable.

| Signal | Connection |
|---|---|
| GND | Host ground |
| VIN | Host power supply |
| CTX | Host CAN TX output |
| CRX | Host CAN RX input |

### 4.3 J2 CAN Bus Terminal

| Position | Signal | Connection |
|---|---|---|
| Upper | CANH | CAN bus high line |
| Lower | CANL | CAN bus low line |

### 4.4 Castellated Headers

The castellated pads duplicate the controller, bus, regulator, and control
signals for solderless prototyping or carrier-board mounting. Their labels are
printed directly on the top silkscreen.

![](hardware/resources/unit_top_v_1_0_ue0085_TCAN1051HVD.png){width=4.0in}
