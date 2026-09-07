# Piphi Network Huawei Solar

Generated PiPhi integration runtime.

## Run locally

```bash
pdm install -G dev
pdm run uvicorn piphi_network_huawei_solar.main:app --reload --port 4213
pdm run pytest
pdm run python scripts/validate.py
```

The runtime listens on port `4213` by default and exposes the common PiPhi runtime route contract:

- `GET /health`
- `GET /diagnostics`
- `POST /discover`
- `POST /config`
- `POST /config/sync`
- `POST /deconfigure`
- `POST /deconfigure/{config_id}`
- `GET /state`
- `GET /contract`
- `GET /entities`
- `GET /events`
- `POST /events/device/{config_id}/example`
- `POST /telemetry/example`
- `POST /telemetry/device/{config_id}/example`
- `POST /command`

## Capability coverage

`capability-catalog.json` inventories inverter, PV string, meter, grid,
battery, optimizer, elevated control, and Modbus transport capabilities. Each
entry is implemented, planned, or excluded, and tests prevent planned register
features from leaking into the advertised runtime contract.

Capabilities will be negotiated by inverter model, firmware, unit ID,
installed subdevices, transport, and write permission. Raw register access and
unsafe protection changes are excluded.

## Manifest

`manifest.json` is a starter manifest. Before publishing, update:

- `image`
- `version`
- capabilities and commands
- config fields and identity fields
- entity metadata

## Docker

```bash
docker build -t docker.io/piphinetwork/piphi-network-huawei-solar:0.1.0 .
docker run --rm -p 4213:4213 docker.io/piphinetwork/piphi-network-huawei-solar:0.1.0
```
