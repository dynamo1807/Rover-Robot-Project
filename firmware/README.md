# Firmware

Production firmware has not been initialized yet. MR-011 selects the build
system and establishes a reproducible STM32G431 project before feature work
begins.

The intended layers, safety state machine, coding rules, and verification
strategy are documented in [`docs/FIRMWARE.md`](../docs/FIRMWARE.md).

Do not commit only generated IDE output. The repository must retain the inputs
needed to reproduce a clean build, including toolchain version and generation
boundaries.

