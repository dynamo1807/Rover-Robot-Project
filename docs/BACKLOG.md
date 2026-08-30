# Engineering Backlog

This backlog converts the current design into reviewable work packages. GitHub
Issues are the execution record; this file preserves the planned order and the
relationship between workstreams.

Priority meanings:

- **P0:** blocks a safe or technically defensible next milestone.
- **P1:** required for the first integrated drive base.
- **P2:** valuable extension after the baseline is stable.

| ID | Priority | Milestone | Work item | Status | GitHub Issue |
| --- | --- | --- | --- | --- | --- |
| MR-001 | P0 | M0 | Freeze drive-base requirements and acceptance criteria | Ready | [#1](https://github.com/dynamo1807/Rover-Robot-Project/issues/1) |
| MR-002 | P0 | M1 | Characterize candidate 12 V encoder gearmotors | Ready | [#2](https://github.com/dynamo1807/Rover-Robot-Project/issues/2) |
| MR-003 | P0 | M1 | Validate DRV8872 current regulation and thermal margin | Blocked by MR-002 | [#3](https://github.com/dynamo1807/Rover-Robot-Project/issues/3) |
| MR-004 | P0 | M1 | Freeze battery, protection, and regulator architecture | Ready | [#4](https://github.com/dynamo1807/Rover-Robot-Project/issues/4) |
| MR-005 | P0 | M1 | Prototype one complete motor and encoder channel on STM32G431 | Blocked by MR-002/004 | [#5](https://github.com/dynamo1807/Rover-Robot-Project/issues/5) |
| MR-006 | P0 | M2 | Freeze STM32G431 pin, timer, and DMA allocation | Ready | [#6](https://github.com/dynamo1807/Rover-Robot-Project/issues/6) |
| MR-007 | P0 | M2 | Complete schematic capture, ERC cleanup, and design review | In progress | [#7](https://github.com/dynamo1807/Rover-Robot-Project/issues/7) |
| MR-008 | P0 | M2 | Route PCB revision A and pass layout review/DRC | Blocked by MR-003/004/006/007 | [#8](https://github.com/dynamo1807/Rover-Robot-Project/issues/8) |
| MR-009 | P1 | M2 | Produce an orderable BOM and sourcing alternatives | Blocked by MR-007 | [#9](https://github.com/dynamo1807/Rover-Robot-Project/issues/9) |
| MR-010 | P1 | M3 | Execute current-limited PCB bring-up and record results | Blocked by MR-008/009 | [#10](https://github.com/dynamo1807/Rover-Robot-Project/issues/10) |
| MR-011 | P1 | M4 | Establish reproducible firmware project and CI checks | Ready | [#11](https://github.com/dynamo1807/Rover-Robot-Project/issues/11) |
| MR-012 | P1 | M4 | Implement motor driver and deterministic fault handling | Blocked by MR-011 | [#12](https://github.com/dynamo1807/Rover-Robot-Project/issues/12) |
| MR-013 | P1 | M4 | Implement encoder capture and wheel-speed estimation | Blocked by MR-011 | [#13](https://github.com/dynamo1807/Rover-Robot-Project/issues/13) |
| MR-014 | P1 | M4 | Implement and tune bounded wheel-speed PID control | Blocked by MR-012/013 | [#14](https://github.com/dynamo1807/Rover-Robot-Project/issues/14) |
| MR-015 | P1 | M5 | Design and verify the printable drivetrain chassis | Blocked by MR-002/004 | [#15](https://github.com/dynamo1807/Rover-Robot-Project/issues/15) |
| MR-016 | P2 | M6 | Define and validate IMU/ToF expansion interfaces | Blocked by M4 | [#16](https://github.com/dynamo1807/Rover-Robot-Project/issues/16) |

## Recommended execution order

1. Complete MR-001, MR-002, MR-004, and MR-006 in parallel where possible.
2. Use those results to finish MR-003, MR-005, and MR-007.
3. Release the PCB through MR-008 and MR-009.
4. Bring up hardware with MR-010 while establishing firmware through MR-011.
5. Complete MR-012 through MR-014 before mechanical endurance testing.
6. Integrate the chassis in MR-015, then promote MR-016 and autonomy work.

## Definition of Ready

An item is ready when it has a clear problem statement, relevant inputs or
dependencies, bounded scope, measurable acceptance criteria, and no unresolved
decision that makes the implementation direction arbitrary.

## Definition of Done

An item is done when its acceptance criteria pass, source artifacts and evidence
are committed or linked, documentation reflects changed assumptions or
interfaces, review comments are resolved, and no known P0 safety defect remains.
