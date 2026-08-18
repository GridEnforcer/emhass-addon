# Changelog

## 0.18.1-ge13 (unreleased)

- **Rebuild pulls the battery startup penalty (ge-jeh)** from `feature/ge-v0.18.1`: new `set_battery_startup_penalty` (scalar/per-battery, default 0.0 = off) + `battery_initial_active` runtime param. Opt-in — plans are unchanged until the plugin sends a nonzero penalty. CACHE_BUST ge12 → ge13.

## 0.18.1-ge12 (unreleased — deploy only with the ge-b9n cutover)

- **Pin bumped to the re-based fork `feature/ge-v0.18.1`** (upstream EMHASS v0.18.1 with native multi-battery + the two GridEnforcer ports: per-battery availability windows, per-battery `battery_is_dc_coupled`). CACHE_BUST ge11 → ge12. The baked `/share/config.json` keys were verified unchanged against v0.18.1 (gap analysis in ge-b9n); path env defaults are identical between 0.16.2 and 0.18.1, and the addon's `addon_config` mapping already matches the post-0.17 layout. New runtime files appear under `/data/` on first boot (`plan_latest.json`, last-run snapshot, `battery_identification.json`, `entities/`). The server now returns HTTP 200 (not 201) for `/action/*` and serves `GET /api/v1/plan`, `/api/v1/last-run`, `/healthz` — required by gridenforcer_emhass ≥ the ge-b9n phase-2 plugin, which no longer speaks the 0.16.2 fork protocol. **Do not install this addon version with the old plugin or vice versa** — the phase-4 shadow test/cutover ships both sides together.

# Changelog

See also [emhass/CHANGELOG.md](emhass/CHANGELOG.md) for add-on specific release notes.

## Unreleased

- Add CLAUDE.md and PRD.md

## 0.16.2-ge4

- Fix mixed timezone bug in EMHASS publish_data
- Add CACHE_BUST arg to force fresh git clone on rebuild

## 0.16.2-ge3

- Fix IndexError when soc_init/soc_final list is shorter than num_batteries
- Add SOC-by-departure constraint for battery availability windows

## 0.16.2-ge2

- Port multi-battery support to EMHASS v0.16.2
- Per-battery CVXPY variables, constraints, and stress cost
- Battery availability windows

## 0.13.5-ge1

- Initial add-on based on EMHASS v0.13.5
