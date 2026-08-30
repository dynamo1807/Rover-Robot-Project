# Project Roadmap

Progress is based on evidence and exit criteria, not only on task completion.
Later milestones may be refined as measurements replace current assumptions.

## M0 — Requirements and design baseline

**Outcome:** the first drive-base scope is unambiguous and technically
reviewable.

Exit criteria:

- functional and safety requirements are documented;
- current architecture and interfaces are documented;
- accepted and open decisions are visible;
- P0 backlog items have owners or a clear next action;
- no future autonomy feature is required to validate the drive base.

## M1 — Bench-validated drivetrain

**Outcome:** one representative motor channel and both encoder channels are
understood before custom-PCB release.

Exit criteria:

- selected motors have measured electrical, speed, and encoder data;
- DRV8872 current regulation and thermal margin are demonstrated;
- a G431 development board drives a motor through the intended command scheme;
- encoder direction and maximum-speed capture are verified;
- the power architecture and protection concept are frozen.

## M2 — PCB release

**Outcome:** reviewable manufacturing data for controller PCB revision A.

Exit criteria:

- MCU pin/timer allocation is frozen;
- schematic review and ERC are complete;
- layout review and DRC are complete;
- BOM, alternatives, fabrication outputs, and assembly notes are generated;
- bring-up sequence and test points are documented.

## M3 — Controller bring-up

**Outcome:** an assembled PCB is electrically safe and controllable.

Exit criteria:

- resistance checks and current-limited first power-up pass;
- all rails, reset, clock, SWD, and UART pass;
- both motor channels and both encoders pass open-loop tests;
- fault inputs and safe-stop behavior pass;
- bring-up deviations are recorded and schematic fixes are back-annotated.

## M4 — Closed-loop drive base

**Outcome:** two-wheel speed control operates reliably under representative
load.

Exit criteria:

- reproducible firmware builds and basic automated tests exist;
- both wheel-speed estimators are calibrated;
- PID response meets defined tracking and stability requirements;
- command timeout, watchdog, and injected-fault tests pass;
- thermal and runtime tests under representative load pass.

## M5 — Mechanical integration

**Outcome:** the verified electronics and drivetrain operate in the printed
chassis.

Exit criteria:

- CAD and print settings are versioned;
- battery, PCB, motors, wiring, and strain relief are safely retained;
- service access and cooling are adequate;
- straight-line, turning, braking, and endurance tests pass.

## M6 — Sensor-ready rover

**Outcome:** the drive base exposes stable interfaces for autonomy experiments.

Exit criteria:

- IMU and ToF interfaces are electrically and mechanically validated;
- timestamped telemetry and basic odometry are available;
- sensor faults do not compromise safe manual/bench operation;
- the next autonomy milestone has explicit requirements.

Potential later work includes obstacle avoidance, sensor fusion, wireless
control, camera integration, mapping/SLAM, and a manipulator. These are not
commitments until promoted into the active backlog.

