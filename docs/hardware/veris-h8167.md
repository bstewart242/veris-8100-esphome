# Veris H8167 Energy Meter

The H8167 is the meter used by this project. The installed H8163-CB
communications board makes its measurements available over Modbus RTU.

## Project notes

- Meter variants differ by service configuration and available phases.
- Phase C measurements may be unavailable on single- or split-phase models.
- The communications board receives its project-specific setup in
  [the H8163-CB guide](veris-h8163-cb.md).
- Register availability by model is recorded in the
  [Modbus register map](../software/modbus-registers.md).

## References

- [Manufacturer website](https://www.veris.com/)
- [Local H81xx installation guide](veris/h81xx_installation_guide.pdf)
- [Project photos](../../images/hardware/veris/)

The official installation guide controls for meter mounting, conductor routing,
voltage limits, and safety requirements.
