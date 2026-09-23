# exploration/

Learning notebooks for the Exploration Stage of the project — see the [learning roadmap](../PROJECT_BRIEF.md#11-learning-roadmap-exploration-stage).

Each notebook is a self-contained tutorial (in German) that builds one concept from scratch, runs it, and then changes something deliberately to show the effect. They are optimised for understanding, not reuse: the future research code will not import anything from here.

| Directory | Notebook | Topics |
|-----------|----------|--------|
| `01_neural_network_basics/` | [`nn_basics.ipynb`](01_neural_network_basics/nn_basics.ipynb) | tensors, forward pass, loss, backprop, gradient descent by hand, MLP, train/val split, overfitting |
| `02_pytorch/` | [`pytorch_deep_dive.ipynb`](02_pytorch/pytorch_deep_dive.ipynb) | shapes & memory, broadcasting, design matrix, `Dataset`/`DataLoader`, optimisers in parameter space, `nn.Module` internals, CPU vs. MPS |
| `03_autodiff/` | — | *planned* |
| `04_odes/` | — | *planned* |
| `05_inverse_problems/` | — | *planned* |
| `06_pinns/` | — | *planned* |

Notation follows *Mathematics for Machine Learning* (Deisenroth, Faisal, Ong — [mml-book.com](https://mml-book.com/)): $N$ data points, $D$ dimensions, $\boldsymbol{\theta}$ parameters, $\gamma$ step size. The notebooks cross-reference its chapters; the book is freely available from the authors' website.

## Setup

From the repository root:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r exploration/requirements.txt
jupyter lab
```

Every notebook is executed top to bottom in CI on each push (see `.github/workflows/notebooks.yml`), so they should run without hidden state.

> **macOS + iCloud Drive:** if the repository lives in a synced folder, create the environment as `.venv.nosync` and symlink `.venv` to it — the `.nosync` suffix stops iCloud from syncing (and corrupting) the environment.
