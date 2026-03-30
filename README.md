# GridEnforcer EMHASS Add-on

Home Assistant add-on for the GridEnforcer EMHASS fork with multi-battery support.

## Overview

This add-on packages the [GridEnforcer EMHASS fork](https://github.com/GridEnforcer/emhass) as a Home Assistant add-on. It builds from source, installing the `feature/multiple-batteries-v0.16.2` branch which adds per-battery SOC, DC/AC coupling, availability windows, and stress cost to the EMHASS optimizer.

The add-on runs a Gunicorn + Uvicorn web server on port 5000, accessible via Home Assistant ingress or direct HTTP for the GridEnforcer EMHASS plugin.

## Installation

1. In Home Assistant, go to **Settings > Add-ons > Add-on Store**
2. Click the menu (top right) > **Repositories**
3. Add: `https://github.com/GridEnforcer/emhass-addon`
4. Find "EMHASS (GridEnforcer)" in the store and install

> **Note:** First install takes 10-20 minutes (builds from source). Subsequent starts are fast.

## Configuration

The add-on is configured through the Home Assistant add-on UI. Configuration options map to EMHASS parameters (solar panels, battery specs, location, etc.). See the add-on's DOCS.md for details.

## Updating

1. Bump `version` in `emhass/config.yml`
2. Update `emhass/CHANGELOG.md`
3. Commit and push — HA add-on store picks up the new version
4. Bump `CACHE_BUST` in the Dockerfile if Docker layer cache needs busting

## Structure

```
emhass/
    config.yml      # Add-on metadata (version, ports, ingress, schema)
    config.json     # Default EMHASS configuration
    build.yml       # Docker build targets (aarch64, amd64)
    Dockerfile      # Clones fork, installs via UV, runs Gunicorn
    DOCS.md         # User-facing documentation
    CHANGELOG.md    # Version history
```

## License

MIT
