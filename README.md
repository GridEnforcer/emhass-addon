# GridEnforcer EMHASS Add-on

Home Assistant add-on for EMHASS with multi-battery support.

## Installation

1. In Home Assistant, go to **Settings → Add-ons → Add-on Store**
2. Click **⋮** (top right) → **Repositories**
3. Add: `https://github.com/GridEnforcer/emhass-addon`
4. Find "EMHASS (GridEnforcer)" in the store and install

> **Note:** First install takes 10-20 minutes as it builds from source.
> Subsequent starts are fast (image is cached).

## Updating

To pick up new changes from the EMHASS fork, bump the `version` in
`emhass/config.yml` and reinstall the add-on.
