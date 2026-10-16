# Getting Started


<div align="center">
  <a href="#"><img src="https://img.shields.io/badge/version-1.0-blue.svg" alt="Version"></a>
  <a href="#"><img src="https://img.shields.io/badge/language-Python-lightgrey.svg" alt="Language"></a>
  <a href="#"><img src="https://img.shields.io/badge/language-C-lightgrey.svg" alt="Language"></a>
  <a href="#"><img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License"></a>
  <br>
</div>

# DevLab TCAN1051HVD — CAN Communication with ESP32

This guide explains how to install and use the **DevLab TCAN1051HVD** Arduino library to establish CAN communication between two ESP32-based development boards. The example uses a **Pulsar ESP32-H2** as the transmitter and an **ESP32-P4** as the receiver.

## Overview

The **Texas Instruments TCAN1051HVD** is a CAN physical-layer transceiver. It interfaces an ESP32's native **TWAI (Two-Wire Automotive Interface)** controller with the differential CAN bus through the **CANH** and **CANL** signals.

The transceiver does **not** implement the CAN protocol by itself. Message framing, arbitration, and error handling are managed by the ESP32 TWAI controller. The Arduino library provides a convenient abstraction over the underlying ESP-IDF TWAI driver.

> **Important:** This library targets the TCAN1051HVD transceiver used with an ESP32 that has a supported native TWAI controller. On the UE0085, the IC's TXD/RXD pins connect to module signals **CTX/CRX**; the module also exposes VIN, GND, CANH, CANL, power rails, and EN. IC pin **S** is unconnected in the module schematic and defaults to normal transceiver mode through its internal pull-down; it is not available as a software control.

## Requirements

### Hardware

- 1 × Pulsar ESP32-H2 development board
- 1 × ESP32-P4 development board
- 2 × TCAN1051HVD CAN transceiver modules (one per board)
- CANH/CANL wiring and a shared ground reference
- Appropriate CAN bus termination (typically 120 Ω at each physical end of the bus)
- 2 x USB cables for programming and serial monitoring

### Software

- Arduino IDE
- Compatible ESP32 board support package
- **DevLab TCAN1051HVD** library

## Library Installation

1. Open **Arduino IDE**.
2. Open the **Library Manager**.
3. Search for **DevLab_TCAN1051HVD** and install it if listed.
4. Otherwise, download the [library repository](https://github.com/UNIT-Electronics-MX/unit_devlab_tcan1051hvd_library) as a ZIP and use **Sketch > Include Library > Add .ZIP Library**.

Include the library in your sketch:

```cpp
#include <DevLab_TCAN1051HVD.h>
```

## Hardware Connections

Each ESP32 board must connect to its **own** TCAN1051HVD transceiver.

### Pulsar ESP32-H2 (Transmitter)

| TCAN1051HVD signal | ESP32-H2 connection |
| --- | --- |
| CTX (transceiver TXD) | GPIO12 |
| CRX (transceiver RXD) | GPIO22 |
| VIN | Regulated 3.3 V to 5.0 V supply |
| VIO selector | 3V3 position for ESP32 logic |
| GND | GND |

### ESP32-P4 (Receiver)

| TCAN1051HVD signal | ESP32-P4 connection |
| --- | --- |
| CTX (transceiver TXD) | GPIO20 |
| CRX (transceiver RXD) | GPIO21 |
| VIN | Regulated 3.3 V to 5.0 V supply |
| VIO selector | 3V3 position for ESP32 logic |
| GND | GND |

### CAN Bus Wiring

| Transmitter transceiver | Receiver transceiver |
| --- | --- |
| CANH | CANH |
| CANL | CANL |
| GND | GND |

**Electrical notes:**

- Connect **CANH to CANH** and **CANL to CANL**; do not cross them.
- Place **120 Ω termination across CANH and CANL at each physical end** of a conventional high-speed CAN bus. Check whether your modules already include termination before adding resistors.
- Supply the UE0085 through **VIN**. Its onboard converters generate the transceiver's 5 V supply and the 3.3 V rail; the exposed 5V and 3V3 contacts are outputs. Set the VIO selector to 3V3 for these ESP32 boards, and never bridge both VIO positions. Use a host 3.3 V rail only if it can supply the module.
- Both devices must use the **same CAN bit rate**. The library's current `begin()` default is 500 kbit/s; set the timing explicitly if changing it.
- Standard CAN transmission normally requires a second active node to acknowledge the frame. Power and initialize the receiver before testing the transmitter.

## Example 1 — Pulsar ESP32-H2 CAN Transmitter

The Pulsar ESP32-H2 queues a standard CAN frame with identifier `0x100`, containing a one-byte counter. The counter increments after each successful queue operation and wraps around after `255`.

```cpp
#include <DevLab_TCAN1051HVD.h>

#define CAN_TX_PIN GPIO_NUM_12
#define CAN_RX_PIN GPIO_NUM_22

DevLab_TCAN1051HVD can(CAN_TX_PIN, CAN_RX_PIN);

uint8_t counter = 0;

void setup() {
  Serial.begin(115200);
  delay(1000);

  Serial.println("Starting ESP32-H2...");

  if (!can.begin()) {
    Serial.println("Error initializing CAN");
    while (true) {
      delay(1000);
    }
  }

  Serial.println("CAN initialized successfully");
}

void loop() {
  uint8_t data[1] = {counter};

  if (can.send(0x100, data, 1, 0, 0, 1000)) {
    Serial.print("Queued: ");
    Serial.println(counter);
    counter++;
  } else {
    Serial.println("Unable to send CAN message");
  }

  delay(1000);
}
```

### Transmitter Behavior

- Initializes the serial monitor at **115200 baud**.
- Initializes the ESP32 TWAI controller through the library.
- Creates a CAN data payload containing one `uint8_t` value.
- Sends a CAN message with identifier `0x100` approximately once per second.
- Reports whether the driver accepted the frame into its transmit queue; receiver output confirms communication.

## Example 2 — ESP32-P4 CAN Receiver

The ESP32-P4 waits for incoming CAN frames and prints the received identifier, payload length, and first data byte (if present).

```cpp
#include <DevLab_TCAN1051HVD.h>

#define CAN_TX_PIN GPIO_NUM_20
#define CAN_RX_PIN GPIO_NUM_21

DevLab_TCAN1051HVD can(CAN_TX_PIN, CAN_RX_PIN);

void setup() {
  Serial.begin(115200);
  delay(1000);

  if (!can.begin()) {
    Serial.println("Error initializing CAN");
    while (true) {
      delay(1000);
    }
  }

  Serial.println("CAN initialized successfully");
  Serial.println("Waiting for messages...");
}

void loop() {
  TCAN1051_Frame frame;

  if (can.receive(frame, 100)) {
    Serial.print("ID: 0x");
    Serial.println(frame.id, HEX);

    Serial.print("Number of bytes: ");
    Serial.println(frame.length);

    if (frame.length > 0) {
      Serial.print("Received data: ");
      Serial.println(frame.data[0]);
    }

    Serial.println();
  }
}
```

### Receiver Behavior

- Initializes the TWAI controller with its specified TX and RX pins.
- Waits up to **100 ms** per receive call for a frame.
- Prints the incoming CAN identifier in hexadecimal format.
- Prints the number of bytes in the received payload.
- Displays the first payload byte when the message contains data.

## Running the Example

1. Connect both ESP32 boards to their respective TCAN1051HVD modules.
2. Connect the two transceivers over **CANH**, **CANL**, and **GND**.
3. Verify supply voltages, common CAN bitrate, and bus termination.
4. Upload the **receiver sketch** to the ESP32-P4.
5. Upload the **transmitter sketch** to the Pulsar ESP32-H2.
6. Open each board's serial monitor at **115200 baud**.
7. Confirm that the transmitter reports queued frames and the receiver displays identifier `0x100` with an increasing counter.

### Example Serial Output

**Transmitter:**

```text
Starting ESP32-H2...
CAN initialized successfully
Queued: 0
Queued: 1
Queued: 2
```

**Receiver:**

```text
CAN initialized successfully
Waiting for messages...
ID: 0x100
Number of bytes: 1
Received data: 0

ID: 0x100
Number of bytes: 1
Received data: 1

ID: 0x100
Number of bytes: 1
Received data: 2
```

The outputs above are illustrative; actual timing and delivery depend on the configured CAN bus and wiring.

## Understanding the CAN Frame

The transmitter uses this library call:

```cpp
can.send(0x100, data, 1, 0, 0, 1000);
```

Here, `0x100` is the message identifier, `data` points to the payload, and `1` is the payload length in bytes. The remaining arguments are library-specific options and a timeout; refer to the installed library's API definition to confirm their exact meanings.

In this example, each frame carries **one data byte**. The receiver can inspect `frame.id`, `frame.length`, and `frame.data[0]`.

## Troubleshooting

| Symptom | What to check |
| --- | --- |
| CAN initialization fails | ESP32 TWAI support, selected board, GPIO assignments, and library compatibility |
| Transmitter cannot send | Receiver online and acknowledging, common bit rate, valid termination, transceiver supply, and bus wiring |
| No frames appear on receiver | CANH/CANL polarity, shared ground, correct pins, compatible bitrate, and serial monitor settings |
| Intermittent or corrupted communication | Cable length, interference, termination placement, ground potential, and bit-rate suitability |
| Compilation fails | Installed library name/version, ESP32 board package, and supported chip APIs |

## Notes and Limitations

- These sketches demonstrate **Classic CAN**, not CAN FD.
- The example receiver prints only the **first byte** of each received frame.
- The example does not implement higher-level message sequencing, retransmission policies, or application-layer data integrity checks.
- The UE0085 does not expose IC pin **S / Silent Mode**. Its internal pull-down selects normal transceiver mode by default; TWAI software modes configure the ESP32 controller, not S.
- Confirm the exact **GPIO availability and electrical specifications** for your board revisions before wiring.

## References

- [Texas Instruments TCAN1051 product information](https://www.ti.com/product/TCAN1051)
- [Espressif ESP-IDF TWAI documentation](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/api-reference/peripherals/twai.html)
- Arduino IDE Library Manager — search for `DevLab TCAN1051HVD`

---

This README documents a basic two-node CAN communication example using the DevLab TCAN1051HVD Arduino library, a Pulsar ESP32-H2 transmitter, and an ESP32-P4 receiver.
