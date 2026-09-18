# sam workspace

uv workspace for SAM3 OFF-period detection: the `samoffs` package with its
`train` extra, plus pinned siblings (`cnpix`, `ecephys`, `wisc_ecephys_tools`).
Nothing here is imported by the `gfys_workspace` environment.

## Getting started

See [`docs/SETUP.md`](docs/SETUP.md): clone, clone `samoffs` inside, `uv sync`.

## Layout

| Path | What it is |
| --- | --- |
| `samoffs/` | The package (gitignored checkout of CSC-UW/samoffs). Training code lives in `samoffs/src/samoffs/training/`. |
| `pyproject.toml` | Pins the siblings; `uv.lock` pins their commits. |
| `docs/SETUP.md` | Setup steps. |

## Running

```bash
uv run pytest -q
uv run python -m samoffs.training.fine_tune_sam3 --help
```
