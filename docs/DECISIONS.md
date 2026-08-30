# Engineering Decision Log

This lightweight decision log records the design baseline without pretending
that unvalidated assumptions are final. A decision moves from **Proposed** to
**Accepted** only when its consequences and required evidence are understood.

| ID | Status | Decision | Rationale | Revisit trigger |
| --- | --- | --- | --- | --- |
| D-001 | Accepted | Use STM32G431 as the controller family; target STM32G431CBT6 on the custom PCB | Motor-control timers, analog capability, performance, and a practical Nucleo prototype path | Pin/resource conflict or unavailable part |
| D-002 | Accepted | Use one DRV8872 per motor | Independent bidirectional channels with current regulation and fault reporting | Measured motor/thermal limits fail |
| D-003 | Proposed | Use two 12 V GA25/JGA25-370 class metal gearmotors with AB Hall encoders at approximately 100–130 rpm | Appropriate scale, encoder availability, and simple differential drive | MR-002 measurements or chassis requirements fail |
| D-004 | Accepted | Use differential drive for the first platform | Mechanically simple and compatible with independent wheel-speed control | Terrain or payload requirement changes |
| D-005 | Accepted | Validate with a G431 development board before ordering the custom PCB | Reduces simultaneous hardware and firmware uncertainty | None; this is a risk-control measure |
| D-006 | Proposed | Reserve I2C/GPIO interfaces for IMU and ToF expansion | Supports later autonomy without coupling it to initial drive-base success | Pin/power budget cannot support it |
| D-007 | Open | Battery chemistry, cell count, protection, charging, and regulation | Insufficient verified load and runtime data | Resolve in MR-004 |
| D-008 | Open | Firmware build system and STM32 HAL/LL boundary | Reproducibility and testability requirements need evaluation | Resolve in MR-011 |

## Decision procedure

1. State the decision and viable alternatives.
2. Record constraints, evidence, and consequences.
3. Link the responsible GitHub Issue.
4. Mark the decision Accepted only after its acceptance criteria pass.
5. When superseded, retain the old row and link the replacement decision.

