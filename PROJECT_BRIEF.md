# Project Brief: Physics-Informed Computational Measurement

Detailed research background and long-term vision for this project. For durable working instructions (communication style, teaching approach, current-stage rules), see [CLAUDE.md](CLAUDE.md) — that file takes precedence for how to work; this one explains *why*.

## 1. Background

Physics student at TU Berlin (8th semester). Academic interests: experimental/applied physics, optics and quantum systems, electrodynamics, physical measurement systems, machine learning / physics-informed ML.

Practical background: ~1 year of hardware development (STM32 firmware, embedded systems, electronics, drone systems, sensor systems), plus prior work with genetic algorithms for physics-related optimization.

New to: neural networks, deep learning, PyTorch, JAX, physics-informed ML, PINNs, scientific ML in general. Learning approach is learning-by-doing — implement first, pull in theory when the next practical step requires it, and understand what the code is actually doing rather than treating it as a black box.

## 2. Long-term research vision

Central question: **how much measurement hardware can physics-informed computation replace or augment?**

The core concept, "computational measurement":

```
Physical system → sensors → raw measurements → inverse physical/ML model → useful physical quantity
```

The eventual ESP32-S3 deployment is not the point in itself — it's a demonstration that a compact inverse computational model can become part of a real, inexpensive measurement instrument. The broader question is whether physics-informed ML enables useful measurements from fewer sensors, lower-quality sensors, noisier or sparser measurements, indirect measurements, or cheaper optical/electronic hardware.

## 3. Main application: computational spectroscopy

Instead of a conventional high-resolution spectrometer:

```
unknown spectrum S(λ) → optical encoding → small number of measurements → inverse model → reconstructed S_hat(λ)
```

Concretely: S(λ) with ~300 wavelength bins, encoded down to ~5–20 sensor measurements via an optical system (photodiodes, optical filters, diffraction gratings, LEDs, simple optical geometries, deliberately compressed measurements).

Order of work: simulate the inverse problem first. Only build the real optical setup once the computational inverse problem is understood.

## 4. Alternative framing: hardware reduction

```
100 measurement channels → 50 → 20 → 10 → 5
```

Measure how reconstruction quality degrades as channel count drops, and how it's affected by SNR, sensor calibration error, measurement uncertainty, and training data size. Compare three approaches: classical reconstruction, standard neural network, physics-informed ML. Do not assume physics-informed ML wins — the experiment must show it.

## 5. Generalizability question

Deeper question: which parts of computational measurement generalize across physically different measurement problems?

Eventual (not premature) software concept — generic measurement system + problem-specific forward physics + problem-specific sensor model + problem-specific inverse model:

- **Generic**: data acquisition, preprocessing, calibration, normalization, model loading, inference, uncertainty handling, evaluation, deployment.
- **Problem-specific**: physical forward model, sensor response, physical geometry, physical constraints, target quantity, inverse model.

This may eventually become a small Python library implementing that separation — but the architecture should emerge from actual experiments, not be designed in advance (see CLAUDE.md, Exploration Stage rules).

## 6. Possible second physical demonstration

Electrical measurement problem, to test whether the same architecture generalizes outside optics:

```
V(t), I(t) → inverse model → estimate R, L, C or other physical parameters
```

Not to be implemented until one physical problem (spectroscopy) works properly end-to-end.

## 7. Forward and inverse models

Keep this distinction explicit throughout the project.

**Forward model** — physical state → physical system → measurement. Example: `S(λ) → optical system → y`, i.e. `y = F(x) + noise`. Answers "what would the measurement system observe if the physical state were known?" May be analytical, numerical, experimentally calibrated, or learned.

**Inverse model** — measurement → estimated physical state. Example: `y → neural network → S_hat(λ)`. This is the model that may eventually run on the ESP32-S3.

Division of labor: PC handles training, simulation, evaluation, model selection. ESP32 eventually handles sensor acquisition, preprocessing, inference, and physical-quantity estimation.

## 8. First eventual computational experiment (post-Exploration)

Synthetic inverse spectroscopy problem:

- Generate synthetic S(λ) (~300 wavelength bins): single peaks, multiple peaks, Gaussian peaks, broad spectra, noisy spectra, mixtures.
- Define a measurement operator: `y = A S + ε`, with S ~300-dim and y ~20-dim — a deliberately underdetermined inverse problem.
- **(A) Classical reconstruction**: least squares, ridge regression, possibly sparse reconstruction.
- **(B) Standard neural inverse model**: `y → MLP → S_hat`.
- **(C) Physics-informed approach**: use the known forward model as a data-consistency term, e.g. `L = L_reconstruction + λ · L_physics` with `L_physics = ||F(S_hat) - y||²`. Exact formulation to be investigated, not assumed.

## 9. Experimental transition

Once simulation works: build a simple controlled optical setup, starting with known discrete wavelengths and an independent reference measurement where possible.

```
known source → optical system → sparse sensors → data acquisition → inverse model → estimated physical quantity → independent reference
```

Use the real experiment to calibrate the forward model, characterize sensor response, measure noise, identify systematic errors, and validate reconstruction.

## 10. Embedded deployment (ESP32-S3)

PC: training, evaluation, dataset generation, model selection. ESP32: sensor acquisition, preprocessing, neural inference, output. Things to investigate: model size, RAM usage, inference latency, quantization, numerical precision, accuracy degradation. Important engineering demonstration, but should not automatically become the main scientific contribution.

## 11. Learning roadmap (Exploration Stage)

Sequence can change based on what's actually difficult in practice. Corresponds to the `exploration/` subdirectories.

**Stage A — Neural network fundamentals**: tensors, datasets, MLPs, forward pass, loss functions, gradients, backpropagation, optimization, overfitting, train/val/test.

**Stage B — Scientific ML basics**: NumPy, PyTorch, JAX, automatic differentiation, vectorization, numerical optimization.

**Stage C — Dynamical systems**: ODEs, initial value problems, numerical integration, stability, phase space, simple physical dynamical systems. Refresh Newtonian/Lagrangian/Hamiltonian mechanics and conservation laws as needed — no need for a full undergraduate mechanics review up front.

**Stage D — Inverse problems**: forward vs. inverse models, ill-posed problems, regularization, noise, identifiability, classical reconstruction methods.

**Stage E — Physics-informed ML**: physics-based loss terms, boundary/initial conditions, PDEs, PINNs, limitations of PINNs, comparison with classical numerical methods.

**Stage F — Measurement applications**: sparse measurements, noisy measurements, sensor models, experimental calibration, inverse reconstruction.

**Stage G — Actual project**: only after sufficient intuition from A–F.

## 12. Eventual Bachelor thesis direction

Likely to focus deeply on one physical measurement problem. Candidate framings (title to be chosen only after initial experiments):

- "Physics-informed machine learning for low-cost computational spectroscopy"
- "Reducing measurement hardware through physics-informed inverse modeling"
- "Physics-informed computational measurement under sparse sensing"

Realistic structure: physical measurement problem → forward model → experimental calibration → classical inverse reconstruction → standard ML baseline → physics-informed ML → sparse/noisy measurement experiments → hardware reduction analysis → ESP32 deployment → generalizability discussion. Do not attempt to prove universal generalization — identify what's generic, what's problem-specific, where the approach works, and where it fails.

## 13. Transition: Exploration → Research

The Exploration Stage ends when the user has enough intuition to:

- explain what a neural network is
- explain backpropagation at a conceptual level
- use PyTorch or JAX comfortably
- understand automatic differentiation
- explain a forward model and an inverse problem
- understand ill-conditioning and regularization
- build a simple PINN
- understand basic limitations of PINNs

At that point (explicit, user-driven — not automatic), set up the actual research project structure: reproducible experiments, scientific documentation, experiment logs, literature references, and `docs/ai_usage.md` (see CLAUDE.md for the AI-documentation policy change that happens at this point).
