# exploration/

Sandbox for the current Exploration / Learning Stage — see [../CLAUDE.md](../CLAUDE.md) and [../PROJECT_BRIEF.md](../PROJECT_BRIEF.md#11-learning-roadmap-exploration-stage).

Notebooks and scripts here are disposable by design: intuition over polish, throwaway experiments expected, no fixed architecture. Subdirectories follow the current roadmap and may be renamed, reordered, or added to as needed.

- `01_neural_network_basics/` — tensors, forward pass, loss, backprop, MLP, train/val split ([`nn_basics.ipynb`](01_neural_network_basics/nn_basics.ipynb))
- `02_pytorch/` — shapes & memory, broadcasting, design matrix, `Dataset`/`DataLoader`, optimisers in parameter space, `nn.Module` internals, CPU vs MPS ([`pytorch_deep_dive.ipynb`](02_pytorch/pytorch_deep_dive.ipynb))
- `03_autodiff/`
- `04_odes/`
- `05_inverse_problems/`
- `06_pinns/`

Notation follows *Mathematics for Machine Learning* (Deisenroth, Faisal, Ong — [mml-book.com](https://mml-book.com/)): $N$ data points, $D$ dimensions, $\boldsymbol{\theta}$ parameters, $\gamma$ step size. Notebooks cross-reference its chapters. The PDF itself is git-ignored (personal-use licence).

## Setup

The environment lives at the repo root in `.venv.nosync/` (the `.nosync` suffix keeps iCloud from syncing and corrupting it); `.venv` is a symlink to it:

```bash
source .venv/bin/activate       # -> .venv.nosync
pip install -r exploration/requirements.txt
jupyter lab                     # or: jupyter notebook
```

Both are git-ignored.
