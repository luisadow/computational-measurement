# exploration/

Sandbox for the current Exploration / Learning Stage — see [../CLAUDE.md](../CLAUDE.md) and [../PROJECT_BRIEF.md](../PROJECT_BRIEF.md#11-learning-roadmap-exploration-stage).

Notebooks and scripts here are disposable by design: intuition over polish, throwaway experiments expected, no fixed architecture. Subdirectories follow the current roadmap and may be renamed, reordered, or added to as needed.

- `01_neural_network_basics/` — tensors, forward pass, loss, backprop, MLP, train/val split ([`nn_basics.ipynb`](01_neural_network_basics/nn_basics.ipynb))
- `02_pytorch/`
- `03_autodiff/`
- `04_odes/`
- `05_inverse_problems/`
- `06_pinns/`

## Setup

Dependencies for this stage are separate from any future research-project environment (see [../README.md](../README.md#repository-structure)):

```bash
cd exploration
python3 -m venv .venv
source .venv/bin/activate       # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter lab                     # or: jupyter notebook
```

`.venv/` is git-ignored.
