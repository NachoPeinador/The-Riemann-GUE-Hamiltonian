# First-Neighbor Connectivity Governs the Non-Ergodic Extended Phase in PRBM

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.19284510.svg)](https://doi.org/10.5281/zenodo.19284510)
[![License: MIT](https://img.shields.io/badge/Code-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![License: CC BY 4.0](https://img.shields.io/badge/Data-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Lean 4](https://img.shields.io/badge/Lean-4.34.1-purple.svg)](https://leanprover.github.io/)
[![Python](https://img.shields.io/badge/Python-3.12-yellow.svg)](https://www.python.org/)

**Author:** José Ignacio Peinador Sala ([ORCID: 0009-0008-1822-3452](https://orcid.org/0009-0008-1822-3452))  
**Manuscript:** *First-neighbor connectivity governs the non-ergodic extended phase in power-law random banded matrices with sparse hopping constraints*  
**Archived artifact:** [10.5281/zenodo.19284510](https://doi.org/10.5281/zenodo.19284510)  
**submission id:** EPJB-D-26-00793

---

## TL;DR

Contrary to the expectation that arithmetic structures (e.g., the coprime-to-6 mask or the Möbius function) generate distinct number-theoretic spectral signatures, this work provides numerical and formally certified evidence that the **Non-Ergodic Extended (NEE) phase is entirely governed by the preservation of first-neighbor connectivity ($d = 1$)**.

Suppressing the $d=1$ channel induces a topological collapse into strong spatial localization ($D_2 \approx 0.285 \to 0.045$, a factor of 6.4), representing a single-particle spatial analogue of **Hilbert Space Fragmentation (HSF)**. The deep arithmetic logic of the Möbius function acts as topological white noise, in compliance with the **Möbius Randomness Principle** (Sarnak conjecture): since $86.05\%$ of the interaction variance is concentrated in short-range bonds ($d \leq 5$), deeper arithmetic channels are buried beneath the finite-size GUE noise floor ($\sigma_{\text{GUE}} \sim 1/\sqrt{N}$).

---

## Repository structure

```
.
├── PRBM_Modular_Lean/              # Lean 4 verification suite (13 modules)
│   ├── WheelChannelStructure.lean
│   ├── UnitCellMeasure.lean
│   ├── ChiralPhaseAbsorption.lean
│   ├── KatoRellichRegime.lean
│   ├── LocalResonanceCoupling.lean
│   ├── ChannelDensityContraction.lean
│   ├── NonErgodicPhaseBound.lean
│   ├── PolyphaseFilterZ6.lean
│   ├── FirstNeighborPreservation.lean
│   ├── DihedralQuantization.lean
│   ├── BipartiteInterferenceBound.lean
│   ├── ExpectedDegreeBound.lean
│   ├── FractalDimensionUpperBound.lean
│   └── lakefile.lean
├── notebooks/
│   ├── PRBM_Modular_GPU_Experiments.ipynb   # Main computational suite
│   └── module17_bulk_data_M3.npz            # Bulk D2 data (M=3 seeds)
├── figures/                        # All manuscript figures (PDF/PNG 300 DPI)
├── data/                           # Numerical results (.npz files)
├── MANIFEST_SHA256.txt             # Cryptographic checksum manifest
├── LICENSE_CODE                    # MIT License (Lean 4, Python)
├── LICENSE_DATA                    # CC BY 4.0 (manuscript, figures, data)
└── README.md
```

---

## Theoretical and physical framework

- **Deterministic–stochastic hybrid Hamiltonian.** Combines an exact Riemann–von Mangoldt diagonal potential (inverted deterministically via the Lambert $W$ function) with Power-Law Random Banded Matrix (PRBM) off-diagonal disorder.
- **Sparse hopping constraints.** Hopping is filtered by deterministic arithmetic sieves (coprime-to-6 mask $\Xi_6$, square-free Möbius mask $\Xi_\mu$, Liouville mask $\Xi_\lambda$) and controlled random Bernoulli ensembles.
- **Single-particle HSF analogue.** Without $d=1$, adjacent spatial transitions ($i \to i+1$) require higher-order virtual paths ($i \to i+5 \to i+1$) that suffer severe energy detuning from the fluctuating diagonal potential. The one-dimensional metric graph shatters into decoupled spatial clusters.
- **Coupling variance dominance.** The power-law decay ($d^{-1.5}$ in variance) concentrates $86.05\%$ of the interaction weight in $d \in \{1, 2, 3, 5\}$.
- **Parameter-free operating point.** $\nu = 0.75$ (center of the critical window $0.5 < \nu < 1$); local resonance coupling $\epsilon_c = \pi\sqrt{2}$; Maslov phase $7/8$.

---

## Mechanized formal verification in Lean 4

The algebraic, topological, and connectivity constraints governing the model are certified **100% `sorry`-free** by the Lean 4 kernel (v4.34.1 with Mathlib4). The suite comprises **13 decoupled modules**, of which **10 are fully certified at Level N1** (zero `sorry` assertions):

| Module | Certified statement | Level |
|---|---|---|
| `WheelChannelStructure` | Confinement to active chiral sublattices ($d \equiv 1, 5 \pmod 6$) | N1 |
| `UnitCellMeasure` | Unit cell totient measure ($\sum_{d=1}^6 \Xi(d) = 2 \implies \varphi(6)/6 = 1/3$) | N1 |
| `ChiralPhaseAbsorption` | Invertibility of coprime residues modulo 6 | N1 |
| `KatoRellichRegime` | Self-adjointness domain window ($1/2 < \nu < 1$) | N1 |
| `LocalResonanceCoupling` | Hybridization resonance condition ($\epsilon_c = \pi\sqrt{2}$) | N1 |
| `ChannelDensityContraction` | Strict density hierarchy ($4/15 < 1/3 < 1/2 < 1$) | N1 |
| `NonErgodicPhaseBound` | Non-triviality of the bipartite ceiling ($1/4 < 1$) | N1 |
| `PolyphaseFilterZ6` | Complete stopband annihilation for non-coprime channels | N1 |
| `FirstNeighborPreservation` | Guaranteed base coordination degree ($w_1 = 2$) | N1 |
| `FractalDimensionUpperBound` | Generalized Jensen inequality for the IPR; universal bound $D_2 \leq \varphi(m)/m$ | N1 |
| `DihedralQuantization` | Reflection involution; percolation threshold bounds | N2 |
| `BipartiteInterferenceBound` | Certified upper bound $D_2 \leq 1/4$ under chiral equiprobability | N2 |
| `ExpectedDegreeBound` | Mean degree lower bound ($\langle \deg \rangle_{\text{local}} \geq 2$) | N2 |

*Empirical validation of the Lean 4 axioms.* Extensive GPU audits up to $N = 12\,000$ confirm that the chiral equiprobability axiom ($c_1 = c_5 = 1/2$) holds strictly at the ensemble level ($\langle W_1 - W_5 \rangle = -0.000048 \approx 0$), with local mass fluctuations decaying monotonically as $N \to \infty$.

---

## Experimental validation matrix

| Observable | Empirical result | Benchmark | Physical significance |
|---|---|---|---|
| Macroscopic alignment ($R^2$) | $> 0.999999$ | $R^2 \to 1$ | Autonomous Weyl law tracking; zero empirical rescaling |
| Bulk spacing ratio $\langle r \rangle$ | $0.5891 \pm 0.0024$ | GUE $0.5996$ / Poisson $0.3863$ | Intermediate non-ergodic extended statistics |
| SFF ramp exponent $\gamma$ | $0.6086 \pm 0.0103$ | GUE $\gamma = 1$ | Sub-diffusive spectral ramp characteristic of NEE |
| FSS thermodynamic limit $D_2^\infty$ | $0.113 \pm 0.003$ | Anderson $D_2 = 0$ | $39\sigma$ rejection of Anderson localization |
| Chalker scaling $\beta = 2D_2$ | $\beta = 0.5549 \pm 0.0020$ | $2D_2 = 0.5562 \pm 0.0054$ | $0.2\sigma$ agreement between transport and fractal support |
| Multifractal curvature $\Delta D$ | $D_0 - D_2 = 0.730$ | Ergodic $\Delta D = 0$ | Strict convexity of $D_q$ for $q \in [-3, 4]$ |
| First-neighbor removal | $D_2 = 0.0448 \pm 0.0009$ | Preserved: $0.2882$ | Sixfold collapse into strong localization (HSF analogue) |
| Short-range rescue ($d=1$) | $D_2 = 0.2849 \pm 0.0007$ | Unforced: $0.0556$ | Forcing $d=1$ restores the NEE phase in random masks |
| Topological pinning ($\varepsilon = \varepsilon_c$) | Ratio $D_2^{\text{no}}/D_2^{\text{with}} \approx 0.17$ | Healed ratio $\to 1$ | Collapse cannot be overcome at the critical resonance |
| Riemann zeros control (SFF) | $\gamma_{\text{zeros}} = 0.94 \pm 0.12$ | GUE $\gamma = 1$ | Real zeros are ergodic; NEE ramp is intrinsic to the mask |

---

## Reproducing the results

### Requirements

- Python ≥ 3.10 (tested on 3.12)
- NumPy ≥ 1.26, SciPy ≥ 1.11, PyTorch ≥ 2.0, Matplotlib ≥ 3.8
- Lean 4 v4.34.1 with Mathlib4 (pinned revision in `MANIFEST_SHA256.txt`)
- GPU: NVIDIA Tesla T4 (16 GB). A CPU fallback is available for $N \leq 2000$.

### Quick start

```bash
# 1. Clone the repository
git clone https://github.com/NachoPeinador/The-Riemann-GUE-Hamiltonian.git
cd The-Riemann-GUE-Hamiltonian

# 2. Install Python dependencies
pip install -r requirements.txt

# 3. Run the main computational notebook
jupyter notebook notebooks/PRBM_Modular_GPU_Experiments.ipynb

# 4. (Optional) Verify the Lean 4 suite
cd PRBM_Modular_Lean
lake build
```

All numerical experiments use a fixed random seed (`SEED = 42`) and double precision (`complex128` / `float64`) throughout. Every figure and table of the manuscript is regenerated automatically from a single run of the notebook.

### Module map

| Notebook section | Contents | Manuscript ref. |
|---|---|---|
| Modules 00a–00c | System setup, Riemann-zero audit, vectorized Hamiltonian engine | Sec. 2 |
| Modules 01–03 | Exact diagonalization ($N = 10\,000$), $P(s)$ and $\langle r \rangle$, SFF ensemble ($M=100$, $N=15\,000$) | Secs. 3.1–3.3 |
| Modules 04–06 | Channel-density scaling, FSS collapse, AIC/BIC model selection | Secs. 3.4–3.6 |
| Modules 07–09 | Anderson transition sweep, mask comparison suite, Möbius equivalence | Secs. 3.7–3.9 |
| Modules 10–12 | Multifractal spectrum $D_q, f(\alpha)$, microscopic GPU scan, quantum dynamics | Secs. 3.10–3.13 |
| Modules 13–16 | Riemann zeros control SFF, coupling sweep, chiral equiprobability audit, vector export | Secs. 3.14–3.15, App. B |

---

## Declarations

**Author contributions.** Conceptualization, methodology, software, formal analysis, formal verification, investigation, data curation, validation, writing (original draft and revision), visualization, project administration.

**Competing interests.** The author declares no competing interests, financial or otherwise.

**Funding.** No external funding was received for this research.

**Ethics.** Ethical approval was not required, as this research is theoretical and numerical and involves no human participants or animal subjects.

**Generative AI disclosure.** Google Gemini and DeepSeek were used exclusively as auxiliary tools for language editing, adversarial logical review ("red-teaming"), and code debugging. They were not used to produce any original scientific content: all model design, numerical experiments, theoretical derivations, and interpretations are the author's own work. Every AI-assisted output has been reviewed and validated by the author.

---

## Licensing

- **Source code** (Lean 4, Python, PyTorch): [MIT License](LICENSE_CODE)
- **Manuscript, figures, manifests, and data**: [CC BY 4.0](LICENSE_DATA)

---

## Citation

If you use this code or data in your work, please cite:

```bibtex
@article{PeinadorSala2026PRBM,
  title   = {First-neighbor connectivity governs the non-ergodic extended
             phase in power-law random banded matrices with sparse
             hopping constraints},
  author  = {Peinador Sala, Jos{\'e} Ignacio},
  journal = {Zenodo},
  year    = {2026},
  note    = {Artifact: \url{https://doi.org/10.5281/zenodo.19284510}}
}
```

---

## Contact

For questions, bug reports, or collaboration inquiries, please open an issue on GitHub or contact the author at `joseignacio.peinador@gmail.com`.
