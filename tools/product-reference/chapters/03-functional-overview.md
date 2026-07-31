## 3 Functional Overview

### 3.1 Signal Path

CTX drives the TCAN1051HVD TXD input. A logic LOW requests a dominant bus state,
and a logic HIGH requests a recessive state. The transceiver converts this logic
signal into the CANH/CANL differential output.

CRX is driven by the TCAN1051HVD RXD output. CRX is LOW when the receiver detects
a dominant bus state and HIGH when it detects a recessive state. The CRX output
level follows the selected VIO rail.

The TCAN1051HVD includes dominant-timeout, thermal-shutdown, and undervoltage
protection. The bus and logic pins present high impedance when the transceiver is
unpowered.

### 3.2 Power Architecture

VIN feeds the TPS61023 boost converter, which generates the 5 V transceiver
supply. The AP2112K then generates the 3.3 V rail. Both regulated rails are
exposed on the castellated headers.

The VIO selector connects the transceiver I/O supply to either 3.3 V or 5 V:

| Host logic | VIO selector |
|---|---|
| 3.3 V MCU or CAN controller | 3V3 |
| 5 V MCU or CAN controller | 5V |

Select exactly one side of the VIO solder selector. Bridging both sides shorts
the 3.3 V and 5 V rails and can damage the module or host.

EN controls the TPS61023 regulator. The onboard bias enables the regulator for
normal use; driving EN LOW disables the generated supply rails and transceiver.

### 3.3 Bus Termination

The onboard termination is a split 120 Ω network made from two 60 Ω resistors.
Its midpoint is AC-coupled to ground by 4.7 nF to reduce common-mode noise.

Close the **120R Termination** selector only when this module is installed at one
physical end of the CAN trunk. A correctly wired point-to-point bus normally has
one 120 Ω terminator at each end (approximately 60 Ω measured between CANH and
CANL with power removed). Leave the selector open at intermediate nodes.

### 3.4 Bus Protection

CANH and CANL are protected by a PESD2CANFD24L-UX device. The TCAN1051HVD
H-suffix transceiver provides a ±70 V bus-fault rating and a ±30 V receiver
common-mode range. These protections improve robustness but do not replace
correct grounding, cabling, termination, or system-level surge design.

