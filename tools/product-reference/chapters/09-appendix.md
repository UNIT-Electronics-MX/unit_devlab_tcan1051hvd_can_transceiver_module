## 9 Appendix

### **9.1 Schematic** {.section-page}

The complete revision 1 schematic is distributed with this product reference:

[Open the UE0085 TCAN1051HVD module schematic](https://unit-electronics-mx.github.io/unit_devlab_tcan1051hvd_can_transceiver_module/hardware/unit_schematic_v_1_0_ue0085_TCAN1051HVD.pdf)

![UE0085 revision 1 schematic, also available as the original PDF](hardware/resources/unit_schematic_v_1_0_ue0085_TCAN1051HVD.png){width=6.5in}

### **9.2 Design Notes** {.section-page}

- R1 provides the switchable 120 Ω termination.
- R2 and R3 form the 2 × 60 Ω split termination.
- C5 (4.7 nF) AC-couples the split-termination midpoint to ground.
- R4 and R5 (22 Ω) are in series with CTX and CRX.
- D1 protects CANH and CANL.
- IC1 pin S is unconnected in the revision 1 schematic. The TCAN1051HVD's
  internal pull-down selects normal mode by default; the module does not
  expose S as a user control. For noisy or transient-prone systems, review
  this reliance on the IC's internal bias during hardware qualification.

