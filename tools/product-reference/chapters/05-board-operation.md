## 5 Board Operation

This procedure brings up a two-node, 500 kbit/s Classic CAN bus. It uses one
UE0085 module with a Pulsar ESP32-H2 transmitter and a second UE0085 module
with an ESP32-P4 receiver. The module supplies the CAN physical layer; each
ESP32 supplies the TWAI/CAN controller.

### 5.1 Required Hardware and Software

| Item | Quantity | Purpose |
|---|---:|---|
| UE0085 TCAN1051HVD module | 2 | One transceiver per controller |
| Pulsar ESP32-H2 and ESP32-P4 development boards | 1 each | TWAI controllers |
| USB data cables and a computer | 2 | Uploads and serial monitoring |
| Twisted pair, hookup wires, common ground wire | As needed | Bus and host wiring |
| Regulated 3.3 V to 5.0 V supply for each module | 1 per module | UE0085 VIN; a host 3.3 V rail is suitable only if it can supply the module |
| Multimeter | Recommended | Power and termination checks |

Install Arduino IDE, an ESP32 board package supporting the selected boards,
and the [DevLab_TCAN1051HVD Arduino library](https://github.com/UNIT-Electronics-MX/unit_devlab_tcan1051hvd_library).
This library wraps the ESP32 TWAI peripheral; it does not add a CAN controller
to a host without one. Confirm GPIO availability against the actual
development-board revisions.

### 5.2 Hardware Connection and Configuration

**Remove power before wiring or changing selectors.** Each host needs its own
UE0085 module. Connect J1 as follows; these GPIO assignments match the supplied
example sketches.

| UE0085 signal | Pulsar ESP32-H2 transmitter | ESP32-P4 receiver |
|---|---|---|
| VIN | Regulated 3.3 V to 5.0 V supply | Regulated 3.3 V to 5.0 V supply |
| GND | Host GND | Host GND |
| CTX | TWAI TX, GPIO12 | TWAI TX, GPIO20 |
| CRX | TWAI RX, GPIO22 | TWAI RX, GPIO21 |

The controller-facing labels belong to the **UE0085 board**. The mounted
TCAN1051HVD (IC1) uses different pin names:

| IC1 pin | UE0085 connection | Function |
|---|---|---|
| 1 TXD | CTX through R4 (22 Ω) | Logic input from the controller's CAN TX |
| 2 GND | GND | Common reference |
| 3 VCC | Onboard regulated 5V rail | Transceiver bus-side supply; not the module's VIN |
| 4 RXD | CRX through R5 (22 Ω) | Logic output to the controller's CAN RX |
| 5 VIO | 3V3/5V selector | Sets TXD/S input thresholds and RXD HIGH level |
| 6 CANL, 7 CANH | J2 bus terminal, with onboard protection and selectable termination | Differential CAN bus |
| 8 S | Unconnected on the revision 1 schematic | Internal pull-down selects normal transceiver mode by default; no external S control |

VIN is the **module input**. The labeled 5V and 3V3 contacts are generated
output rails, not substitutes for VIN. Set each module's VIO selector to
**3V3** for these 3.3 V ESP32 GPIOs. Select exactly one VIO position; bridging
3V3 and 5V shorts the rails. Leave EN in its normal, onboard-enabled state.
EN controls the boost converter; it does not select IC1's silent mode. For a
5 V host, select 5V only when its controller logic is 5 V compatible.

Connect the two J2 terminals **CANH to CANH** and **CANL to CANL** with a short
twisted pair. Connect both module/host grounds as a common reference, even
when the modules have separate supplies. Do not connect CANH or CANL to GPIOs.
For this two-node bus, close the **120R Termination** selector on each module:
the modules occupy the two physical ends. Do not add external terminators when
both onboard networks are enabled. On a larger bus, terminate only its two
physical ends and keep branch stubs short.

With all power removed, approximately **60 Ω** should measure between CANH
and CANL on the assembled two-node bus. Approximately 120 Ω suggests a
missing terminator; a much lower reading suggests extra termination or a
short. After applying power, check that both green power LEDs illuminate and
the 5V and 3V3 rails are near their nominal voltages. Remove power if a rail
is shorted, the device heats unexpectedly, or the VIO selector bridges both
rails.

The photographs below show an **illustrative mixed-transceiver bench setup**:
the black UE0085 is connected to the ESP32-H2, while a different blue CAN
transceiver is connected to the ESP32-P4. They show the physical arrangement,
not the exact two-UE0085 wiring specified above. If using the blue module,
follow its own pinout and supply requirements. In either setup, match CANH,
CANL, ground reference, bit rate, and the two physical end terminations.

| Connection overview | Closer view of the two CAN nodes |
|---|---|
| ![ESP32-P4 with a blue CAN transceiver and ESP32-H2 with the black UE0085 module](hardware/resources/img/conn1.JPG){width=2.6in} | ![Closer view of the ESP32 boards, UE0085, and second CAN transceiver](hardware/resources/img/conn2.JPG){width=2.6in} |

### 5.3 Arduino Library and Controller Setup

1. Install a compatible ESP32 board package in Arduino IDE. Select the exact
   ESP32-H2 or ESP32-P4 board and its serial port before each upload.
2. Install `DevLab_TCAN1051HVD` through Library Manager if listed. Otherwise
   download its repository as a ZIP and use **Sketch > Include Library >
   Add .ZIP Library**. Restart Arduino IDE if the header does not appear.
3. Open the two sketches in Section 5.4. The library also contains
   `CAN_Transmitter` and `CAN_Receiver` examples; this repository has
   `software/examples/basic_tx.ino` and `basic_rx.ino`.

![Arduino Library Manager listing for DevLab_TCAN1051HVD; the displayed version may differ from the installed release](hardware/resources/img/library.png){width=1.9in}

Both sketches explicitly use **500 kbit/s** and `TWAI_MODE_NORMAL`. Every
node must use the same nominal bit rate. Normal mode requires another active
node to acknowledge a transmitted frame. The example uses standard 11-bit
identifier `0x100` and one data byte. The TCAN1051HVD supports the CAN FD
physical layer up to 2 Mbps, but this ESP32-H2/P4 TWAI example uses **Classic
CAN frames**, not CAN FD. `TWAI_MODE_NORMAL` selects the ESP32 controller
mode; it does not drive IC1's unconnected S pin.

### 5.4 CAN Communication Example

Upload this transmitter sketch to the Pulsar ESP32-H2. It queues a frame
containing an incrementing byte approximately once per second.

```cpp
#include <DevLab_TCAN1051HVD.h>

DevLab_TCAN1051HVD can(GPIO_NUM_12, GPIO_NUM_22);
uint8_t counter = 0;

void setup() {
  Serial.begin(115200);
  if (!can.begin(TWAI_TIMING_CONFIG_500KBITS(), TWAI_MODE_NORMAL)) {
    Serial.println("CAN initialization failed");
    while (true) delay(1000);
  }
  Serial.println("Transmitter ready");
}

void loop() {
  uint8_t data[1] = {counter};
  if (can.send(0x100, data, 1, false, false, 1000)) {
    Serial.print("Frame queued, counter: ");
    Serial.println(counter);
    counter++;
  } else {
    Serial.println("CAN transmit queue failed");
  }
  delay(1000);
}
```

Upload this receiver sketch to the ESP32-P4. It prints the identifier and
counter received from the bus.

```cpp
#include <DevLab_TCAN1051HVD.h>

DevLab_TCAN1051HVD can(GPIO_NUM_20, GPIO_NUM_21);

void setup() {
  Serial.begin(115200);
  if (!can.begin(TWAI_TIMING_CONFIG_500KBITS(), TWAI_MODE_NORMAL)) {
    Serial.println("CAN initialization failed");
    while (true) delay(1000);
  }
  Serial.println("Receiver ready");
}

void loop() {
  TCAN1051_Frame frame;
  if (can.receive(frame, 100) && !frame.extended && !frame.rtr &&
      frame.id == 0x100 && frame.length == 1) {
    Serial.print("ID: 0x");
    Serial.print(frame.id, HEX);
    Serial.print("  Counter: ");
    Serial.println(frame.data[0]);
  }
}
```

The library's `send()` return value means the ESP32 TWAI driver accepted the
frame into its transmit queue. By itself, it does **not** prove another node
acknowledged or received the frame. The receiver output is the end-to-end
communication check.

### 5.5 Upload and Communication Verification

1. With power off, recheck VIN, GND, CTX/CRX, CANH/CANL, both VIO selectors,
   and the two end terminators. Confirm about 60 Ω across CANH and CANL.
2. Power both boards and modules. Confirm both power LEDs illuminate.
3. Select the ESP32-P4 board and port, upload the receiver, and open its
   serial monitor at **115200 baud**. Wait for `Receiver ready`.
4. Select the Pulsar ESP32-H2 board and port, upload the transmitter, and
   open its serial monitor at **115200 baud**. Use separate IDE windows or
   serial terminals to watch both ports.
5. Confirm that the receiver repeatedly shows `ID: 0x100` and a counter
   advancing from 0, wrapping after 255. The transmitter should report
   queued frames at about one-second intervals.

Example receiver output (the library may also print an initialization line):

```text
Receiver ready
ID: 0x100  Counter: 0
ID: 0x100  Counter: 1
ID: 0x100  Counter: 2
```

If only the transmitter reports queued frames, communication has not been
verified. Check the receiver and bus using Section 5.6.

### 5.6 Troubleshooting

| Symptom | Check |
|---|---|
| No power LED or incorrect rail voltage | VIN 3.3 V to 5.0 V, GND continuity, supply capacity, EN not held LOW, and no rail short. |
| Library header missing or compilation fails | Install `DevLab_TCAN1051HVD`, select a compatible ESP32 board package, and confirm `driver/twai.h` is available. |
| `CAN initialization failed` | Board selection, GPIO availability, TWAI support, and whether another sketch or driver has claimed TWAI. |
| Transmitter queues frames but receiver prints nothing | Receiver running, CTX/TX and CRX/RX assignments, CANH/CANL polarity, common ground, 500 kbit/s at both nodes, and 3V3 VIO. |
| Bus errors or repeated retransmission | Second active node in normal mode, one 120 Ω terminator at each end (about 60 Ω with power off), and matching bit rates. `send()` success alone is not an ACK indication. |
| Intermittent frames | Twisted pair, short stubs, sound terminals, ground reference, and bus length appropriate to the bit rate. |
| CTX stays LOW and the node stops transmitting | Check the TX GPIO configuration. IC1's TXD dominant timeout releases its bus driver; returning CTX HIGH clears that condition. Also inspect bus shorts and VIO selection. |

For persistent faults, the library's `getStatus()` API can report TWAI state
and bus-error counters. Correct wiring and termination before attempting
bus-off recovery.
