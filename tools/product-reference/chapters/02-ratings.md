## 2 Ratings and Electrical Characteristics

### 2.1 Recommended Operating Conditions

| Symbol | Description | Min | Typ | Max | Unit |
|---|---|---:|---:|---:|---|
| VIN | Module input voltage | 3.3 | — | 5.0 | V |
| VCC | TCAN1051HVD bus supply | 4.5 | 5.0 | 5.5 | V |
| VIO | Selected I/O level-shifting supply | 2.8 | 3.3 / 5.0 | 5.5 | V |
| IO(RXD) | Recommended CRX output-current range | −2 | — | 2 | mA |
| TA | IC operating free-air temperature | −55 | — | 125 | °C |
| CAN FD | Supported data rate for the TCAN1051HVD variant | — | — | 2 | Mbps |

VIN is the module-level input recommendation. VCC, VIO, I/O current, temperature,
and CAN FD values are TCAN1051HVD specifications. The complete assembled module
has not been independently qualified over the full IC temperature range.

### 2.2 Selected Transceiver Characteristics

Unless noted otherwise, values below are specified by Texas Instruments over
the recommended operating conditions.

| Symbol | Description | Min | Typ | Max | Unit |
|---|---|---:|---:|---:|---|
| VIH | CTX high-level input voltage | 0.7 × VIO | — | — | V |
| VIL | CTX low-level input voltage | — | — | 0.3 × VIO | V |
| VOH | CRX high-level output voltage at −2 mA | 0.8 × VIO | — | — | V |
| VOL | CRX low-level output voltage at 2 mA | — | — | 0.2 × VIO | V |
| VO(DOM), CANH | Dominant CANH output voltage | 2.75 | — | 4.5 | V |
| VO(DOM), CANL | Dominant CANL output voltage | 0.5 | — | 2.25 | V |
| VOD(DOM) | Dominant differential output, 50–65 Ω load | 1.5 | — | 3.0 | V |
| VCM | Receiver common-mode range | −30 | — | 30 | V |
| tPROP(LOOP) | Total loop delay | — | 100 / 110 | 160 / 175 | ns |

### 2.3 Absolute Maximum Ratings

Absolute maximum ratings are stress limits, not normal operating conditions.

| Symbol | Description | Min | Max | Unit |
|---|---|---:|---:|---|
| VCC | TCAN1051HVD 5 V supply | −0.3 | 7 | V |
| VIO | TCAN1051HVD I/O supply | −0.3 | 7 | V |
| VBUS | CANH or CANL, H-suffix device | −70 | 70 | V |
| VDIFF | CANH-to-CANL differential voltage, H-suffix device | −70 | 70 | V |
| IO(RXD) | CRX output current | −8 | 8 | mA |
| TJ | IC junction temperature | −55 | 150 | °C |
| TSTG | IC storage temperature | −65 | 150 | °C |

Do not apply the ±70 V bus-fault rating to VIN, CTX, CRX, EN, VIO, 3V3, or 5V.
