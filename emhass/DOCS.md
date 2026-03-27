# EMHASS (GridEnforcer Fork)

EMHASS with multi-battery support for GridEnforcer.

Based on the `feature/multiple-batteries` branch of
[GridEnforcer/emhass](https://github.com/GridEnforcer/emhass).

Upgraded to v0.16.2

## Additional features over upstream v0.13.5

- **Per-battery SOC init/final** — each battery can start at a different state of charge
- **DC/AC bus routing** — `battery_is_dc_coupled_list` controls which batteries sit on the DC bus vs AC bus
- **Battery availability windows** — `batt_start_timestep` / `batt_end_timestep` per battery

## Configuration

Same as the official EMHASS add-on. See the
[EMHASS documentation](https://emhass.readthedocs.io/) for details.
