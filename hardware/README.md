# Hardware
<div align="center">

<a href="./unit_schematic_v_1_0_ue0085_TCAN1051HVD.pdf"><img src="./resources/Schematics_icon.jpg" width="500px"><br/> Schematics</a>

</div>

## Technical Specifications

<div align="center">

| **Parameter** |                  **Description**                   | **Min** | **Typ** | **Max** | **Unit** |
|:-------------:|:--------------------------------------------------:|:-------:|:-------:|:-------:|:--------:|
|      Vcc      |        Input voltage to power on the module        |   3.3   |    -    |    5    |    V     |
|      Vio      |             I/O Level shifting Voltage             |   2.8   |    -    |   5.5   |    V     |
|   Ioh(rxd)    |       RXD terminal HIGH level output current       |   -2    |    -    |    -    |    mA    |
|   Ioh(rxd)    |       RXD terminal LOW level output current        |    -    |    -    |    2    |    mA    |
|      Icc      |             Transduccer supply current             |    -    |    -    |   180   |    mA    |
|     I3v3*     |          Maximum current of 3V3 regulator          |    -    |    -    |   600   |    mA    |
|     I5v**     |          Maximum current of 5V regulator           |    -    |    -    |    1    |    A     |
|      Iio      | I/O supply current (RXD Floating, TXD= 0 or 5.5 V) |    -    |   90    |   300   |    uA    |
|      Vih      |              Input high level voltage              | 0.7xVio |    -    |    -    |    V     |
|      Vil      |              Input low level voltage               |    -    |    -    | 0.3xVio |    V     |
|      Vol      |              Output low level voltage              |    -    |    -    | 0.2xVio |    V     |
|      Voh      |             Output high level voltage              | 0.8xVio |    -    |    -    |    V     |
|   Voh(DOM)    |         CANH Bus output voltage (dominant)         |  2.75   |    -    |   4.5   |    V     |
|   Vol(DOM)    |         CANL Bus output voltage (dominant)         |  0.25   |    -    |  2.25   |    V     |
|   Vol(REC)    |    CANH and CANL Bus output voltage (recessive)    |    2    | 0.5xVcc |    3    |    V     |

</div>

*Optimal thermal management is required for the regulator to perform reliably at maximum output current.

**The output current may vary with the input voltage at VIN pin.



## Pinout

<div align="center">
    <a href="#"><img src="resources/unit_pinout_v_0_0_1_ue0094_icp10111_barometric_pressure_sensor_en.jpg" width="500px"><br/>Pinout</a>
    <br/>
    <br/>
    <br/>
    

| Pin Label | Function    | Notes                             |
|-----------|-------------|-----------------------------------|
| VCC       | Power Supply| 3.3V or 5V                       |
| GND       | Ground      | Common ground for all components  |

</div>

## Topology

<div align="center">
<a href="./resources/unit_topology_v_1_0_ue0085_TCAN1051HVD.png"><img src="./resources/unit_topology_v_1_0_ue0085_TCAN1051HVD.png" width="500px"><br/> Topology</a>
<br/>
<br/>
<br/>

| Ref. | Description                              |
|------|------------------------------------------|
| IC1  | CAN Transceiver                          |
| IC2  | AP2112K 3.3V Regulator                   |
| IC3  | TPS61023 5V Regulator                    |
| L1   | Power On LED                             |
| JP1  | 2.54 mm Castellated Holes                |
| JP2  | 2.54 mm Castellated Holes                |
| J1   | JST 1 mm pitch for CAN Data              |
| J2   | Terminal Screw Block for CAN Bus         |
| SB1  | Solder Bridge for VIO                    |

</div>

## Dimensions

<div align="center">

<a href="./resources/unit_dimensions_v_1_0_ue0085_TCAN1051HVD.png"><img src="./resources/unit_dimensions_v_1_0_ue0085_TCAN1051HVD.png" width="500px"><br/> Dimensions</a>

</div>

# References

- [TCAN1051 Datasheet]({{https://www.ti.com/lit/ds/symlink/tcan1051hv.pdf?ts=1762979634497&ref_url=https%253A%252F%252Fwww.ti.com%252Fproduct%252Fes-mx%252FTCAN1051HV%252Fpart-details%252FTCAN1051HVD}})
