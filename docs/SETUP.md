# Setting up the sam workspace

Three steps on any machine with `uv` and `git`. Steps 1 and 2 need GitHub
access to the CSC-UW organisation.

## 1. Clone the workspace and the package

```bash
git clone https://github.com/CSC-UW/samoffs-workspace.git ~/projects/samoffs-workspace
cd ~/projects/samoffs-workspace
git clone https://github.com/CSC-UW/samoffs.git samoffs
```

`samoffs/` is gitignored here: it is its own repository, and you commit to it
from inside `samoffs/`. If you already have a `samoffs` checkout elsewhere,
symlink it instead of cloning: `ln -s /path/to/samoffs samoffs`.

## 2. Create the environment

```bash
uv sync --group dev
```

This installs `samoffs` (editable) with its `train` extra: torch 2.9.1, the
CSC-UW SAM3 fork, pycocotools, hydra, OpenCV. The first sync downloads several
GB of wheels; later syncs reuse the uv cache.

## 3. Point it at the data

These variables are read by `samoffs.training.paths` (added in the training code
plan's Task 3; they have no effect on older checkouts). Add to `~/.bashrc`
(values for tononi-2):

```bash
export SAMOFFS_DATA_ROOT=/nvme/neuropixels/samoffs/data    # rendered PNGs + COCO, regenerable
export SAMOFFS_RUNS_ROOT=/nvme/neuropixels/samoffs/runs    # training runs
# SAMOFFS_MODELS_ROOT defaults to the `samoffs` WNE project's models/ directory.
```

## Check

```bash
uv run python -c "import samoffs, sam3, torch; print(torch.cuda.is_available())"
uv run pytest -q
```

## Updating

- `git -C samoffs pull` updates the package.
- `uv lock --upgrade-package cnpix` (or `ecephys`, `wisc-ecephys-tools`) moves a
  sibling pin to its branch head; commit the new `uv.lock`.
