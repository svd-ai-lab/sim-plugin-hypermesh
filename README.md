# sim-plugin-hypermesh

[Altair HyperMesh](https://altair.com/hypermesh) driver for [sim-cli](https://github.com/svd-ai-lab/sim-cli), distributed as an out-of-tree plugin via Python `entry_points`.

HyperMesh is closed-source commercial FE pre-processor software from Altair. This plugin **does not bundle any vendor binaries, SDKs, or licenses** — users must install Altair HyperWorks Desktop separately and supply their own license. The `hm` Python API ships inside the HyperWorks installation, not on PyPI. See [LICENSE-NOTICE.md](LICENSE-NOTICE.md).

## Install

```bash
pip install git+https://github.com/svd-ai-lab/sim-plugin-hypermesh@main
```

After install, sim-cli auto-discovers the driver:

```bash
sim drivers | grep hypermesh
sim run --solver hypermesh path/to/script.py
```

## How it works

The plugin registers via two entry-point groups:

```toml
[project.entry-points."sim.drivers"]
hypermesh = "sim_plugin_hypermesh:HyperMeshDriver"

[project.entry-points."sim.skills"]
hypermesh = "sim_plugin_hypermesh:skills_dir"
```

`sim.drivers` exposes the driver class; `sim.skills` exposes a directory of skill files bundled inside the wheel.

The driver invokes `runhwx.exe -startwith HyperMesh -f script.py`, which launches HyperWorks Desktop and runs a user Python script that imports `hm` against the bundled HyperMesh Python runtime. Tcl-only batch (`hmbatch.exe`) is detected as a fallback but cannot run `.py` scripts.

## Develop

```bash
git clone https://github.com/svd-ai-lab/sim-plugin-hypermesh
cd sim-plugin-hypermesh
uv sync
uv run pytest
```

Tier-1 protocol-compliance tests (detect, lint, parse_output) run anywhere. Tests that exercise a real HyperMesh install require Windows or Linux with Altair HyperWorks Desktop on `PATH` (or `ALTAIR_HOME` set).

## License

Apache-2.0 for the plugin code itself. See [LICENSE](LICENSE) and [LICENSE-NOTICE.md](LICENSE-NOTICE.md).
