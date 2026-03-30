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
