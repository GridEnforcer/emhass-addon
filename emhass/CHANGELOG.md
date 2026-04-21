# Changelog

## 0.16.2-ge8

- Diagnostic: log `battery_is_dc_coupled_list` / charge-efficiency-list / min-max-soc-list presence in `plant_conf` before and after `_init_battery_param_lists()` broadcast. Investigating whether runtimeparams `_list` keys reach the solver or are dropped by `treat_runtimeparams` for lack of `associations.csv` entries.

## 0.16.2-ge7

- HTML overview now renders per-battery friendly names (`battery_display_name_list`) instead of raw `P_batt0` / `SOC_opt0` labels, and plots per-battery SOC in multi-battery setups

## 0.16.2-ge6

- Backport upstream DST-boundary fixes (forecast date range + `num_timesteps` override) to prevent CVXPY shape mismatches on DST transitions
- Backport upstream continual-publish timeout fix (Quart background task instead of raw thread)

## 0.16.2-ge5

- Per-battery cycle-cost weights (`weight_battery_charge_list` / `weight_battery_discharge_list`); scalar config remains backwards compatible

## 0.16.2-ge4

- Fix mixed timezone bug in EMHASS

## 0.16.2-ge3

- Fix IndexError when soc_init/soc_final list is shorter than num_batteries
- Add SOC-by-departure constraint: battery reaches target SOC by departure_time (not just horizon end)

## 0.16.2-ge2

- Port multi-battery support to EMHASS v0.16.2 (CVXPY-based optimizer)
- Per-battery CVXPY variables, constraints, and stress cost
- Battery availability windows (batt_start_timestep/batt_end_timestep)

## 0.13.5-ge1

- Based on EMHASS v0.13.5 feature/multiple-batteries branch
- Per-battery soc_init/soc_final (list support)
- DC-coupled vs AC-coupled battery bus routing
- Battery availability windows (batt_start_timestep/batt_end_timestep)
