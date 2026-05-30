# GFN2-xTB Investigation of Ultrashort to Long-Chain PFAS Adsorption on Activated Carbon Surface Models

[![Python](https://img.shields.io/badge/Python-3.10-blue.svg)](https://www.python.org/)
[![xTB](https://img.shields.io/badge/xTB-6.6.1-green.svg)](https://github.com/grimme-lab/xtb)
[![RDKit](https://img.shields.io/badge/RDKit-2023.09-orange.svg)](https://www.rdkit.org/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-Google%20Colab-red.svg)](https://colab.research.google.com/)

---

## Overview

This repository contains the complete computational workflow for the study:

> **"GFN2-xTB Investigation of Ultrashort to Long-Chain PFAS Adsorption on Pristine and Hydroxylated Activated Carbon Surface Models: Chain Length, Functional Group, and Surface Chemistry Effects"**

Per- and polyfluoroalkyl substances (PFAS) are persistent environmental contaminants of critical regulatory concern. Granular activated carbon (GAC) is the primary treatment technology for PFAS removal in drinking water, yet exhibits markedly diminished performance for ultrashort-chain PFAS (C1–C3). This study provides the **first systematic computational investigation** of ultrashort to long-chain PFAS adsorption on carbon surface models, employing the GFN2-xTB semi-empirical tight-binding method with implicit aqueous solvation (ALPB).

### Key Findings
- Adsorption energies range from −5.78 to −9.89 kcal mol⁻¹ across C1–C8 PFAS on pristine carbon
- Perfluorosulfonates adsorb more strongly than perfluorocarboxylates at every chain length
- C1–C4 PFAS exhibit pure physisorption (charge transfer < 0.01 e); C8 PFAS show partial chemisorption character (0.16–0.18 e)
- Surface hydroxylation universally weakens PFAS adsorption by 0.08–0.91 kcal mol⁻¹
- TFA (C2) shows the weakest adsorption (−5.98 kcal mol⁻¹), providing molecular-level rationale for GAC treatment failure for ultrashort PFAS

---

## Repository Structure

```
├── PFAS_Adsorption_GFN2xTB.ipynb     # Main Jupyter notebook (Google Colab)
├── README.md                          # This file
├── data/
│   └── results_summary.xlsx           # Adsorption energies and charge transfer data
├── figures/
│   ├── Figure1_pristine_surface.png   # Adsorption energies on pristine coronene
│   ├── Figure2_charge_transfer.png    # Dual-axis Eads + charge transfer plot
│   └── Figure3_surface_comparison.png # Pristine vs oxidized surface comparison
└── tables/
    └── PFAS_Manuscript_Tables.xlsx    # Formatted manuscript tables (Tables 1–3)
```

---

## Computational Details

### Software Requirements

| Software | Version | Purpose | Source |
|---|---|---|---|
| xTB | 6.6.1 | Semi-empirical tight-binding calculations | [Grimme Lab](https://github.com/grimme-lab/xtb) |
| RDKit | 2023.09 | SMILES to 3D structure generation | [RDKit](https://www.rdkit.org/) |
| PubChemPy | 1.0.4 | Surface model coordinate retrieval | [PubChemPy](https://github.com/mcs07/PubChemPy) |
| NumPy | 1.24+ | Numerical operations | [NumPy](https://numpy.org/) |
| Matplotlib | 3.7+ | Visualization | [Matplotlib](https://matplotlib.org/) |

### Method Summary

- **Level of theory:** GFN2-xTB (Bannwarth et al., *J. Chem. Theory Comput.* 2019)
- **Solvation:** Analytical linearized Poisson–Boltzmann (ALPB), water (ε = 80.2)
- **Geometry optimization convergence:** Energy 5×10⁻⁶ Eh; gradient 1×10⁻³ Eh/Bohr
- **Charge analysis:** Mulliken population analysis (`--pop` flag)
- **Conformational sampling:** 3 orientations per PFAS–surface pair (φₓ = 0°, 45°, 90°)
- **Adsorption energy:** Eads = E(complex) − E(PFAS) − E(surface)

### PFAS Compound Library

| Compound | Abbreviation | Chain Length | Class |
|---|---|---|---|
| Trifluoroacetic acid | TFA | C2 | Carboxylate |
| Trifluoromethanesulfonic acid | PFMS | C1 | Sulfonate |
| Perfluoropropionic acid | PFPrA | C3 | Carboxylate |
| Perfluoropropanesulfonic acid | PFPrS | C3 | Sulfonate |
| Perfluorobutanoic acid | PFBA | C4 | Carboxylate |
| Perfluorobutanesulfonic acid | PFBS | C4 | Sulfonate |
| Perfluorooctanoic acid | PFOA | C8 | Carboxylate |
| Perfluorooctanesulfonic acid | PFOS | C8 | Sulfonate |

### Surface Models

| Surface | Model | Atoms | Representative of |
|---|---|---|---|
| Pristine carbon | Coronene (C₂₄H₁₂) | 36 | Graphenic GAC basal plane |
| Oxidized carbon | 1-Hydroxypyrene (C₁₆H₉OH) | 27 | Hydroxylated GAC surface domains |

---

## Usage

### Running on Google Colab (Recommended)

This notebook is designed to run entirely on Google Colab — no local installation required.

1. Open [Google Colab](https://colab.research.google.com/)
2. Upload `PFAS_Adsorption_GFN2xTB.ipynb` or open directly from GitHub
3. Run cells sequentially from Cell 1 onward
4. All dependencies including xTB are installed automatically within the notebook

> ⚠️ **Important:** Google Colab resets the runtime environment on disconnection. All variables and files are lost. Always rerun from Cell 1 when starting a new session. The notebook is designed to handle this — each cell is self-contained and reproducible.

### Notebook Structure

| Cell | Description | Runtime |
|---|---|---|
| Cell 1 | Environment setup, xTB installation, library imports | ~2 min |
| Cell 2 | PFAS and surface structure generation (RDKit + PubChemPy) | ~1 min |
| Cell 3 | Geometry optimization of all monomers (xTB) | ~5 min |
| Cell 4 | Monomer energy extraction | <1 min |
| Cell 5 | Adsorption complex construction (3 orientations) | <1 min |
| Cell 6 | Complex geometry optimization (xTB) | ~15–20 min |
| Cell 7 | Adsorption energy calculation | <1 min |
| Cell 8 | Charge transfer analysis (Mulliken population) | ~5 min |
| Cell 9 | Oxidized surface calculations | ~20 min |
| Cell 10 | Final comparison plots | <1 min |

**Total runtime: approximately 50–60 minutes on Colab free tier**

### Running Locally

If you prefer local execution:

```bash
# Clone repository
git clone https://github.com/yourusername/pfas-adsorption-xtb.git
cd pfas-adsorption-xtb

# Install Python dependencies
pip install rdkit pubchempy numpy matplotlib

# Install xTB
# Linux/macOS:
wget https://github.com/grimme-lab/xtb/releases/download/v6.6.1/xtb-6.6.1-linux-x86_64.tar.xz
tar -xf xtb-6.6.1-linux-x86_64.tar.xz
export PATH=$PATH:$(pwd)/xtb-6.6.1/bin

# Launch notebook
jupyter notebook PFAS_Adsorption_GFN2xTB.ipynb
```

---

## Results Summary

### Adsorption Energies on Pristine Coronene Surface

| Compound | Chain | Group | Eads (kcal mol⁻¹) | Charge Transfer (e) | Mechanism |
|---|---|---|---|---|---|
| TFA | C2 | Carboxylate | −5.98 | +0.0010 | Physisorption |
| PFMS | C1 | Sulfonate | −7.52 | +0.0010 | Physisorption |
| PFPrA | C3 | Carboxylate | −7.09 | +0.0000 | Physisorption |
| PFPrS | C3 | Sulfonate | −7.71 | −0.0000 | Physisorption |
| PFBA | C4 | Carboxylate | −6.96 | −0.0000 | Physisorption |
| PFBS | C4 | Sulfonate | −9.28 | +0.0020 | Physisorption |
| PFOA | C8 | Carboxylate | −7.82 | +0.1620 | Partial chemisorption |
| PFOS | C8 | Sulfonate | −9.89 | +0.1830 | Partial chemisorption |

### Effect of Surface Hydroxylation

| Compound | Pristine (kcal mol⁻¹) | Oxidized (kcal mol⁻¹) | ΔEads (kcal mol⁻¹) |
|---|---|---|---|
| TFA | −5.98 | −5.78 | +0.20 |
| PFMS | −7.52 | −7.44 | +0.08 |
| PFPrA | −7.09 | −6.54 | +0.55 |
| PFPrS | −7.71 | −7.10 | +0.61 |
| PFBA | −6.96 | −6.45 | +0.51 |
| PFBS | −9.28 | −8.88 | +0.40 |
| PFOA | −7.82 | −7.32 | +0.50 |
| PFOS | −9.89 | −8.98 | +0.91 |

---

## Citation

If you use this code or data in your research, please cite:

```bibtex
@article{ubaidullah2026pfas,
  title   = {GFN2-xTB Investigation of Ultrashort to Long-Chain PFAS Adsorption 
             on Pristine and Hydroxylated Activated Carbon Surface Models},
  author  = {Ubaid Ullah, Hasan and Liu, Chao},
  journal = {Journal of Environmental Chemical Engineering},
  year    = {2026},
  note    = {Under review}
}
```

Please also cite the underlying methods:

```bibtex
@article{bannwarth2019gfn2,
  title   = {GFN2-xTB — An Accurate and Broadly Parametrized Self-Consistent 
             Tight-Binding Quantum Chemical Method with Multipole Electrostatics 
             and Density-Dependent Dispersion Contributions},
  author  = {Bannwarth, Christoph and Ehlert, Sebastian and Grimme, Stefan},
  journal = {Journal of Chemical Theory and Computation},
  volume  = {15},
  pages   = {1652--1671},
  year    = {2019},
  doi     = {10.1021/acs.jctc.8b01176}
}

@article{ehlert2021alpb,
  title   = {Robust and Efficient Implicit Solvation Model for Fast Semiempirical Methods},
  author  = {Ehlert, Sebastian and Stahn, Marcel and Spicher, Sebastian and Grimme, Stefan},
  journal = {Journal of Chemical Theory and Computation},
  volume  = {17},
  pages   = {4250--4261},
  year    = {2021},
  doi     = {10.1021/acs.jctc.1c00471}
}
```

---

## Related Work

This study is part of a broader research program on PFAS remediation and water treatment at the Research Center for Eco-Environmental Sciences, Chinese Academy of Sciences:

- PFAS adsorption on N-doped granular activated carbon (manuscript in preparation)
- Catalytic PFAS defluorination review (manuscript in preparation)
- Treatable-by-Design Screener (TbDS) for PFAS prioritization (in development)

---

## Author

**Hasan Ubaid Ullah**
M.Eng. Environmental Engineering
Research Center for Eco-Environmental Sciences, Chinese Academy of Sciences (RCEES-CAS)
Supervisor: Prof. Chao Liu

---

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

---

## Acknowledgments

The authors acknowledge the Grimme group at the University of Bonn for the open-source xTB program package, and the RDKit community for cheminformatics tools. Calculations were performed on Google Colaboratory infrastructure.
