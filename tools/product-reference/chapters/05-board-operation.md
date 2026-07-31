## 5 Board Operation

### 5.1 Before Connecting the Module

1. Confirm that the host includes a CAN controller or CAN-capable peripheral.
2. With power removed, set VIO to match the host logic voltage (3.3 V or 5 V).
3. Enable the onboard 120 Ω termination only if this node is at an end of the
   CAN trunk.
4. Check CANH/CANL polarity and provide a common ground where required by the
   system design.

### 5.2 Basic Connection

| Module | Host or bus |
|---|---|
| VIN | 3.3 V to 5.0 V supply |
| GND | Host/bus reference ground |
| CTX | CAN controller TX output |
| CRX | CAN controller RX input |
| CANH | CANH trunk conductor |
| CANL | CANL trunk conductor |

Keep the CANH/CANL pair twisted, minimize stubs, and place termination only at
the two physical ends of the main bus.

### 5.3 Power-Up Check

After applying VIN:

- The green power LED should illuminate.
- The 5V rail should measure approximately 5 V.
- The 3V3 rail should measure approximately 3.3 V.
- CRX should idle HIGH at the selected VIO level when the bus is recessive.
- CANH and CANL should both be near the recessive common-mode level when idle.

Do not continue if either regulator rail is shorted, if the device becomes hot,
or if the VIO selector connects both rails.

### 5.4 Controller Configuration

Configure the host CAN controller with the same nominal bit rate as every other
node. CAN FD data-phase timing must also match when CAN FD is used. The
TCAN1051HVD supports Classic CAN and CAN FD data rates up to 2 Mbps; protocol
timing, message identifiers, filters, and acknowledgments are handled by the
host controller and software.

### 5.5 Troubleshooting

| Symptom | Checks |
|---|---|
| No power LED | VIN polarity/level, GND continuity, EN state |
| Host receives nothing | VIO setting, CRX pin mapping, bit rate, CANH/CANL polarity |
| Bus errors or missing ACK | Second active node, matching bit rate, two end terminators |
| Communication degrades with cable length | Twisted pair, stub length, topology, termination, bit rate |
| Bus held dominant | CTX stuck LOW, incorrect host pin mode, wiring short |

