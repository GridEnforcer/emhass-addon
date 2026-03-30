# CLAUDE.md

Home Assistant add-on wrapper for the GridEnforcer EMHASS fork (multi-battery support).

## Structure

```
emhass/
    config.yml      # Addon metadata (version, ports, ingress, schema)
    config.json     # Default EMHASS configuration
    build.yml       # Docker build config (aarch64, amd64)
    Dockerfile      # Build script
    DOCS.md         # User-facing docs
    CHANGELOG.md    # Version history
```

## How It Works

- Dockerfile clones `GridEnforcer/emhass` fork, branch `feature/multiple-batteries-v0.16.2`
- Uses UV for Python venv + dependency installation
- Entrypoint: `uv run --frozen gunicorn emhass.web_server:app -k uvicorn.workers.UvicornWorker -b 0.0.0.0:5000`
- Ingress support for HA panel integration
- `CACHE_BUST` ARG forces fresh clone on version bumps

## Updating

1. Bump version in `emhass/config.yml`
2. Update `CHANGELOG.md`
3. Commit and push — HA addon store picks up new version
4. Use `CACHE_BUST` arg or bump it in Dockerfile if Docker cache needs busting

## Definition of done

A feature is complete when:

1. The specified behavior works correctly across all described scenarios
2. Edge cases identified in the specification are handled
3. A corresponding unit test exists and passes
4. No linting errors are introduced
5. A oneline summary of the feature is added to CHANGELOG.md
6. README.md and PRD.md is updated to reflect the changes and user approved the updates
