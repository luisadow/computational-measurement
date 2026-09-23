# Computational Measurement

[![notebooks](https://github.com/luisadow/computational-measurement/actions/workflows/notebooks.yml/badge.svg)](https://github.com/luisadow/computational-measurement/actions/workflows/notebooks.yml)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

**Physics-informed machine learning for low-cost, sparse physical measurement systems.**

Can computation replace measurement hardware? This project investigates whether physics-informed inverse models can recover useful physical quantities from fewer, cheaper, or noisier sensors — with computational spectroscopy as the main application and an ESP32-S3 as the eventual deployment target.

```
physical state x ──► forward model F (optics, sensors) ──► sparse measurement y = F(x) + ε
                                                                   │
estimated state x̂ ◄──────────── inverse model (classical / NN / physics-informed)
```

## Status

**Exploration stage.** Before starting the actual research experiments, I am working through the required foundations — neural networks, PyTorch, automatic differentiation, ODEs, inverse problems and PINNs — one self-contained notebook per topic. The notebooks are written as step-by-step tutorials (in German), so they should also be useful to others learning the same material.

Research background, the planned experiments and the full roadmap are in [PROJECT_BRIEF.md](PROJECT_BRIEF.md).

## Notebooks

| # | Topic | Contents | View |
|---|-------|----------|------|
| 01 | [Neural network basics](exploration/01_neural_network_basics/nn_basics.ipynb) | Tensors, synthetic measurement signal, linear model, MSE loss, backpropagation, gradient descent by hand, MLP from scratch, tensor shapes, training loop, overfitting | [nbviewer](https://nbviewer.org/github/luisadow/computational-measurement/blob/main/exploration/01_neural_network_basics/nn_basics.ipynb) |
| 02 | [PyTorch deep dive](exploration/02_pytorch/pytorch_deep_dive.ipynb) | Memory layout & strides, broadcasting bugs, design matrix, `Dataset`/`DataLoader` as gradient estimation, optimisers in parameter space (reproducing MML Example 7.1), `nn.Module` internals, CPU vs. MPS, silent pitfalls | [nbviewer](https://nbviewer.org/github/luisadow/computational-measurement/blob/main/exploration/02_pytorch/pytorch_deep_dive.ipynb) |
| 03 | Automatic differentiation | *planned* | |
| 04 | ODEs & dynamical systems | *planned* | |
| 05 | Inverse problems | *planned* | |
| 06 | Physics-informed neural networks | *planned* | |

The notebooks contain interactive `ipywidgets` sliders. GitHub's preview renders the static outputs only; run them locally to use the sliders.

## Getting started

Requires Python ≥ 3.12.

```bash
git clone https://github.com/luisadow/computational-measurement.git
cd computational-measurement
python3 -m venv .venv
source .venv/bin/activate
pip install -r exploration/requirements.txt
jupyter lab
```

On Apple Silicon, notebook 02 also compares CPU and GPU (`mps`) execution; on other machines it falls back to CPU.

## Repository structure

```
├── PROJECT_BRIEF.md        research background, planned experiments, roadmap
├── exploration/            learning notebooks, one directory per topic
│   ├── 01_neural_network_basics/
│   ├── 02_pytorch/
│   ├── 03_autodiff/        (planned)
│   ├── 04_odes/            (planned)
│   ├── 05_inverse_problems/(planned)
│   ├── 06_pinns/           (planned)
│   └── requirements.txt
└── LICENSE
```

`exploration/` is intentionally kept separate from the future research code: the notebooks build intuition and are not meant as a reusable library. The research experiments (synthetic inverse spectroscopy, hardware-reduction study) will live in their own top-level directory.

## References

- M. P. Deisenroth, A. A. Faisal, C. S. Ong — [*Mathematics for Machine Learning*](https://mml-book.com/), Cambridge University Press, 2020. Notation in the notebooks follows this book.
- A. Karpathy — [*Neural Networks: Zero to Hero*](https://karpathy.ai/zero-to-hero.html).

## License

[MIT](LICENSE) © Luis Sadowski dos Santos
