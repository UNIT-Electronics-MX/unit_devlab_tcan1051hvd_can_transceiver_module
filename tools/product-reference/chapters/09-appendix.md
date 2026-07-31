## 9 Appendix

### 9.1 Schematic

The complete revision 1 schematic is distributed with this product reference:

[Open the UE0085 TCAN1051HVD module schematic](hardware/unit_schematic_v_1_0_ue0085_TCAN1051HVD.pdf)

### 9.2 Design Notes

- R1 provides the switchable 120 Ω termination.
- R2 and R3 form the 2 × 60 Ω split termination.
- C5 (4.7 nF) AC-couples the split-termination midpoint to ground.
- R4 and R5 (22 Ω) are in series with CTX and CRX.
- D1 protects CANH and CANL.
- The S (silent-mode) pin is fixed for normal transceiver operation on this
  module and is not exposed as a user control.

