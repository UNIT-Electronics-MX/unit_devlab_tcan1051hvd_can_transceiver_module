## 1 The Board

The module separates the controller-side logic interface from the differential
CAN bus. Controller signals are available at the lower castellated header and
the 4-pin connector, while CANH and CANL are available at the upper header and
the screw terminal.

![](hardware/resources/unit_topology_v_1_0_ue0085_TCAN1051HVD.png){width=5.2in}

### 1.1 Package Contents

- 1 × DevLab TCAN1051HVD CAN Transceiver Module (UE0085)

Headers, mating cables, and bus wiring are not included unless stated by the
product listing.

### 1.2 Main Components

| Reference | Component | Function |
|---|---|---|
| IC1 | TCAN1051HVD | CAN physical-layer transceiver |
| IC2 | AP2112K-3.3 | 3.3 V linear regulator |
| IC3 | TPS61023 | 5 V boost converter |
| D1 | PESD2CANFD24L-UX | CANH/CANL transient protection |
| D2 | Green LED | Power indication |
| J1 | 4-pin, 1 mm-pitch connector | VIN, GND, CTX, and CRX interface |
| J2 | 2-position, 3.81 mm terminal | CANH and CANL bus connection |
| JP1 | Termination selector | Connects the onboard split 120 Ω termination |
| SB1 / JP4 | VIO selector | Selects 3.3 V or 5 V logic levels |
