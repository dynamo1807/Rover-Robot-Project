# Verification Plan

## Purpose

Verification converts claims into evidence. Each test has a controlled setup,
expected result, measured result, conclusion, and links to raw data where useful.
Tests involving a powered motor or battery start with current limiting and a
mechanically restrained setup.

## Requirement-level verification matrix

| ID | Requirement | Verification method | Planned phase |
| --- | --- | --- | --- |
| VR-001 | Firmware can command each motor independently in both directions and stop it | Bench demonstration and telemetry | M1/M3 |
| VR-002 | Encoder direction matches the commanded wheel convention | Target integration test | M1/M3 |
| VR-003 | Encoder capture loses no counts at maximum intended speed | Reference measurement and counter logs | M1 |
| VR-004 | Driver current regulation limits current to the designed value | Oscilloscope/current measurement | M1 |
| VR-005 | Driver and PCB temperatures remain within design limits | Worst-case load and thermal test | M1/M4 |
| VR-006 | All logic rails remain within tolerance during start, stop, and reversal | Oscilloscope capture | M1/M3 |
| VR-007 | A driver fault disables torque and is reported | Fault-injection test | M3/M4 |
| VR-008 | Command timeout or watchdog expiry leads to a safe stop | Firmware integration test | M4 |
| VR-009 | Wheel-speed control is stable and meets defined tracking limits | Step and disturbance response report | M4 |
| VR-010 | SWD and UART remain accessible on the assembled rover | Inspection and functional test | M3/M5 |
| VR-011 | Battery and wiring remain mechanically retained and protected | Inspection and motion test | M5 |
| VR-012 | The integrated drive base completes the defined endurance run without an unsafe fault | Endurance test | M5 |

Numerical tolerances for rail voltage, current, temperature, speed error,
settling time, and endurance duration are set in MR-001 after measurements make
them defensible.

## Bench safety checklist

- Use a current-limited laboratory supply for first power-up.
- Restrain the motor and keep wheels clear of the work surface.
- Provide a reachable power disconnect.
- Start with low voltage/current limits and disabled outputs.
- Confirm polarity and resistance before applying power.
- Monitor supply current and critical temperatures.
- Do not stall a motor longer than the defined test procedure allows.
- Record probe grounds and avoid accidental motor-rail shorts.

## PCB bring-up sequence

1. Visual inspection and assembly check.
2. Unpowered resistance checks on every rail.
3. Current-limited input power with motor outputs disconnected.
4. Verify logic rails, reset, and clock behavior.
5. Establish SWD connection and load minimal firmware.
6. Verify UART diagnostics and all safe default GPIO states.
7. Test driver logic and fault inputs without a motor.
8. Connect one motor at reduced limits and test open loop.
9. Validate one encoder, then the second channel.
10. Repeat at design voltage and representative load only after earlier gates pass.

## Test record template

```markdown
# Test: <identifier and title>

- Date / operator:
- Hardware revision:
- Firmware commit:
- Equipment:
- Setup and limits:
- Acceptance criteria:
- Procedure:
- Results:
- Raw evidence:
- Deviations:
- Conclusion: PASS / FAIL / BLOCKED
- Follow-up issues:
```

