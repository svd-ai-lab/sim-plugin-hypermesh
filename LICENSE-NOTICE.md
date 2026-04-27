# License Notice

This repository (`sim-plugin-hypermesh`) is licensed under [Apache-2.0](LICENSE) and contains **only** the open-source driver glue between sim-cli and Altair HyperMesh.

## What is NOT included

This repository does **not** contain, redistribute, or otherwise bundle:

- Altair HyperMesh / HyperWorks Desktop binaries or installers
- The `hm` Python API or any other Altair-bundled module
- Altair license files, license-server tooling, or activation tokens
- Any proprietary Altair schema, documentation, or example projects whose redistribution is restricted

## What you must supply

To use this plugin, you must independently:

1. Install **Altair HyperWorks Desktop** (which includes HyperMesh) on a Windows or Linux host with your own valid Altair license (Altair Units / site license / your organization's license server).
2. Configure the environment so that `ALTAIR_HOME` is set, or `runhwx` / `hmbatch` is on `PATH`. The driver auto-discovers common install locations on Windows (`C:\Program Files\Altair\<version>\...`) and Linux (`/opt/Altair/<version>/...`).

The `hm` Python API is **not on PyPI** — it is installed as part of HyperWorks Desktop and resolved at runtime by the bundled HyperMesh Python interpreter (invoked via `runhwx.exe -f script.py`). For this reason, this plugin's `pyproject.toml` does not declare `hm` as a dependency.

## Trademark notice

"Altair", "HyperMesh", and "HyperWorks" are trademarks of Altair Engineering, Inc. This project is not affiliated with or endorsed by Altair.
