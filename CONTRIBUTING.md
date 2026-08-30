# Contributing

Contributions should improve the rover while preserving traceability between a
problem, a design decision, the changed source, and verification evidence.

## Workflow

1. Open or select a GitHub Issue with measurable acceptance criteria.
2. Confirm that blocking decisions and dependencies are resolved.
3. Create a focused branch such as `hardware/mr-007-schematic-review` or
   `firmware/mr-013-encoder-driver`.
4. Commit source files and documentation in small, coherent changes.
5. Verify the change using the applicable checklist or test plan.
6. Open a pull request that links the issue and includes evidence.

Direct commits to `main` should be limited to repository administration or an
initial project baseline. Product changes should use reviewable branches.

## Commit messages

Use an imperative subject and an optional scope:

```text
docs: establish architecture and verification baseline
hardware: add DRV8872 current-limit calculation
firmware: implement quadrature encoder capture
mechanical: add motor mount revision B
```

Mention the work-item ID in the body when the connection is not obvious.

## Source-of-truth rules

- Commit editable KiCad, CAD, and firmware sources.
- Do not replace source with screenshots or exported PDFs.
- Generated manufacturing artifacts belong in a clearly named release folder
  and must identify the source revision that produced them.
- Record measured values with units, setup, equipment, and uncertainty where it
  affects a decision.
- Never commit credentials, private SSH keys, tokens, or personal configuration.

## Hardware review checklist

- [ ] Requirements and assumptions are linked.
- [ ] Datasheet limits are checked at minimum and maximum conditions.
- [ ] Power and current budgets use worst-case values.
- [ ] Connector pinouts and polarity are documented.
- [ ] ERC/DRC output contains no unexplained item.
- [ ] Test points and bring-up access are adequate.
- [ ] BOM entries are orderable and include alternatives where practical.
- [ ] The verification or bring-up plan covers the changed circuitry.

## Firmware review checklist

- [ ] Public interfaces and units are clear.
- [ ] Error paths and initialization failures are handled.
- [ ] Actuator outputs are bounded and default safe.
- [ ] Interrupt paths are bounded and non-blocking.
- [ ] Relevant host or target tests pass.
- [ ] Compiler warnings are resolved.
- [ ] Telemetry or evidence demonstrates target behavior where required.
- [ ] Documentation reflects changed behavior or timing.

## Definition of Done

A change is done when:

- all issue acceptance criteria pass;
- required source, calculations, and evidence are committed or linked;
- affected documentation and decisions are current;
- review comments are resolved;
- verification is reproducible;
- no known P0 safety or release-blocking defect remains.

## Reporting safety concerns

Open an issue for design-level safety concerns that do not expose a security
secret. Do not include private credentials or sensitive personal information in
an issue, commit, or test log.

