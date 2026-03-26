# Changelog

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
