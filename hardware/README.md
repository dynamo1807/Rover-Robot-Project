# Hardware

This directory is the source of truth for rover electronics.

Planned structure:

```text
hardware/
├── pcb/                  KiCad project and custom libraries
├── bom/                  reviewed BOM and sourcing alternatives
├── calculations/         power, current, thermal, and protection calculations
├── manufacturing/        revisioned release outputs
└── tests/                hardware test procedures and summarized results
```

Do not commit generated KiCad backups or editor-local settings. Manufacturing
outputs must identify the hardware revision and source commit from which they
were generated.

The electrical baseline and PCB release gate are defined in
[`docs/ELECTRONICS.md`](../docs/ELECTRONICS.md).

