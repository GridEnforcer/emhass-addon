# PRD: EMHASS Add-on

Home Assistant add-on wrapper for the GridEnforcer EMHASS fork — packages the multi-battery optimization engine as a Docker container with HA ingress support.

## Behavioral Specification

### Build Process

- **When the Docker image is built**, it:
  1. Installs system dependencies (libopenblas, libhdf5, coinor-cbc, glpk, build tools).
  2. Installs UV package manager.
  3. Clones `GridEnforcer/emhass` fork at branch `feature/multiple-batteries-v0.16.2`.
  4. Creates Python venv via UV, installs all dependencies with `uv lock`.
  5. Pre-copies default data files (`opt_res_latest.csv`, `long_train_data.pkl`).
  6. Copies default config to `/share/config.json`.

- **When `CACHE_BUST` ARG is bumped**, Docker cache is invalidated and a fresh clone is performed.

### Runtime

- **When the container starts**, Gunicorn launches with Uvicorn workers, binding to 0.0.0.0:5000.
- **When HA accesses the add-on via ingress**, traffic is proxied to port 5000 and displayed as an HA sidebar panel.
- **The container has access to**: HA API (via token), `/share` mount (RW), `/config` mount.

### Configuration

- **When the user configures the add-on**, settings are provided via HA UI:
  - `hass_url`, `long_lived_token`: HA connectivity.
  - `time_zone`, `Latitude`, `Longitude`, `Altitude`: Location for PV forecasting.
  - `solcast_api_key`, `solcast_rooftop_id`, `solar_forecast_kwp`: PV forecast provider.
  - `data_path`, `config_path`: File locations.
  - `server_ip`: Bind address (0.0.0.0 or 127.0.0.1).

### Updating

- **When a new version is released** (bumped in `config.yml`), HA add-on store detects it.
- **When the user reinstalls**, a new Docker image is pulled/built.
- **The version format** is `{upstream_version}-ge{patch}` (e.g., `0.16.2-ge4`).

## Acceptance Criteria

1. Container builds successfully for both aarch64 and amd64 architectures.
2. EMHASS web server starts and responds to health check at `/`.
3. Optimization endpoint `/action/naive-mpc-optim` accepts and processes requests.
4. Ingress integration renders EMHASS web UI in HA sidebar.
5. Configuration values are passed to EMHASS process correctly.
6. Default config.json is available at `/share/config.json` after first install.
7. Version bump in config.yml triggers HA add-on update notification.

## Edge Cases

- Docker layer cache may serve stale git clone — bump `CACHE_BUST` to force fresh clone.
- HDF5 library symlink may break across base image updates — Dockerfile pre-generates it.
- UV lock file may become stale if dependencies change — `--frozen` flag prevents resolution at runtime.
- Multi-arch build requires platform-specific base images (bookworm variants).
- Shallow git clone (`--depth 1`) may fail if branch is force-pushed — fall back to full clone.
- Server binding to 127.0.0.1 prevents external access (ingress-only mode).
