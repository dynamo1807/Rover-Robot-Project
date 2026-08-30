# Electronics Design

## Design maturity

The electronics are in the schematic and validation phase. The component
families below form the current baseline, but the design is not ready for PCB
fabrication until the P0 measurements and reviews are complete.

## Baseline components

| Function | Current baseline | Validation required |
| --- | --- | --- |
| Main MCU | STM32G431CBT6, LQFP-48 | Pin/timer allocation, rail current, clock tree |
| Prototype MCU | NUCLEO-G431RB or equivalent | Map prototype pins to final MCU peripherals |
| Motor driver | 2 × DRV8872 | Current regulation, peak current, thermal margin |
| Motors | 12 V GA25/JGA25-370 class, AB Hall encoder | No-load/stall current, speed, encoder CPR, polarity |
| Debug | SWD and UART | Connector, pinout, protection, accessibility |
| Sensors | I2C/GPIO expansion | Voltage, pull-ups, connector, address conflicts |

## Power domains

The current concept contains at least these domains:

- a battery input domain;
- a nominal 12 V motor domain;
- a logic domain for the STM32;
- optional sensor rails.

The battery system and logic conversion are deliberately **not frozen**. The
power architecture task must define input range, reverse-polarity protection,
fuse or current protection, transient suppression, bulk and local decoupling,
logic regulators, power sequencing, battery monitoring, charging boundaries,
and a safe power switch.

## Motor channels

Each motor has a dedicated DRV8872 channel. Before the schematic is frozen:

1. measure motor no-load, loaded, and stall current at the intended voltage;
2. select and calculate the driver's current-regulation components;
3. demonstrate that current and thermal limits are acceptable;
4. verify PWM frequency and input truth-table behavior;
5. confirm recirculation, braking, coast, and fault behavior;
6. size copper, connectors, protection, and decoupling for measured current.

Motor connectors must not be placed or rated from nominal current alone.

## Encoder inputs

Each motor provides A/B Hall encoder signals. The final interface must document:

- encoder supply voltage and output topology;
- pull-up requirements;
- pulses/counts per motor and gearbox revolution;
- legal STM32 input voltage;
- timer channels and alternate functions;
- filtering or hysteresis needed for the actual cable length;
- connector pinout and motor/encoder polarity convention.

Quadrature timer mode is preferred. A bench test must show correct count sign,
no missed counts at maximum speed, and stable zero-speed behavior.

## Schematic conventions

Use explicit, consistent net names:

```text
M1_IN1      M1_IN2      M1_FAULT      ENC1_A      ENC1_B
M2_IN1      M2_IN2      M2_FAULT      ENC2_A      ENC2_B
MOTOR_12V   +3V3        GND
```

Global-label direction is ERC metadata, not an electrical diode. Mark a label
as an output where the local circuit drives it and as an input where the local
circuit receives it.

The DRV8872 `nFAULT` output must not be tied directly to GND. It must connect to
a named MCU fault input and use the pull-up arrangement required by the selected
driver configuration.

Use `PWR_FLAG` only where an external or otherwise passive source actually
drives a KiCad power net. Do not apply multiple competing names to the same
power net.

## Minimum MCU support circuitry

The final schematic review covers:

- every supply and ground pin from the STM32 datasheet;
- local decoupling and bulk capacitance;
- reset and boot configuration;
- SWD connector, ground reference, and optional reset;
- external clock only if justified;
- UART debug interface;
- accessible test points for every rail and critical control signal;
- unused-pin handling;
- ESD/transient protection appropriate to external connectors.

## PCB release gate

The PCB may be released only when:

- the motor/driver bench report is attached to its issue;
- the power budget and worst-case input range are reviewed;
- all MCU pins and timer resources are allocated;
- KiCad ERC has no unexplained error or warning;
- schematic pages have peer/self-review checklists completed;
- connector pinouts and polarities are documented;
- PCB design rules and net classes reflect actual currents;
- the manufacturing BOM contains orderable part numbers and alternatives;
- the bring-up plan in [VERIFICATION.md](VERIFICATION.md) is actionable.

