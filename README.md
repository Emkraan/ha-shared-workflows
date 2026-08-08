# ha-shared-workflows

Shared GitHub Actions reusable workflows for [Emkraan](https://github.com/Emkraan) Home Assistant integrations.

## Why this repo exists

HACS enforces one integration per repository - it picks the first `custom_components/` subdirectory alphabetically and ignores the rest. The six Emkraan HA integrations must stay in separate repos. This repo provides canonical CI they all call, so there is one place to update instead of six.

## Workflows

### `validate-integration.yml`

Runs on every push, pull request, and weekly schedule (Sunday midnight UTC).

| Job | Tool | Purpose |
|---|---|---|
| `hassfest` | `home-assistant/actions/hassfest@master` | Validates integration manifest, config flow, strings, and type annotations against the HA core standard |
| `hacs` | `hacs/action@main` | Validates HACS metadata, repository structure, and release format |

**Usage** - add to `.github/workflows/validate.yml` in each integration repo:

```yaml
name: Validate

on:
  push:
  pull_request:
  schedule:
    - cron: "0 0 * * 0"

jobs:
  validate:
    uses: Emkraan/ha-shared-workflows/.github/workflows/validate-integration.yml@main
    with:
      hacs-category: integration
```

## Integrations using this workflow

| Repo | Integration |
|---|---|
| [homeassistant-hubspace](https://github.com/Emkraan/homeassistant-hubspace) | Hubspace smart home devices |
| [homeassistant-meater](https://github.com/Emkraan/homeassistant-meater) | MEATER smart meat thermometer |
| [homeassistant-familyhub](https://github.com/Emkraan/homeassistant-familyhub) | Samsung Family Hub refrigerator |
| [homeassistant-franklinwh](https://github.com/Emkraan/homeassistant-franklinwh) | Franklin WH energy system |
| [homeassistant-pitboss](https://github.com/Emkraan/homeassistant-pitboss) | Pit Boss pellet grill |
| [homeassistant-playstationnetwork](https://github.com/Emkraan/homeassistant-playstationnetwork) | PlayStation Network presence |
