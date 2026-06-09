# GFN2‑xTB Investigation of Ultrashort‑ to Long‑Chain PFAS Adsorption on Pristine and Hydroxylated Circumcoronene

[![Python 3.10](https://img.shields.io/badge/python-3.10-blue.svg)](https://www.python.org/)
[![RDKit](https://img.shields.io/badge/RDKit-2023.09-green.svg)](https://www.rdkit.org/)
[![xTB](https://img.shields.io/badge/xTB-6.6.1-orange.svg)](https://github.com/grimme-lab/xtb)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Hasaneve/GFN2-xTB_PFAS/blob/main/PFAS_benchmark.ipynb)

## Overview

This repository contains the complete computational workflow and results for the study:

> **"Investigation of Ultrashort‑ to Long‑Chain PFAS Adsorption on Pristine and Hydroxylated Circumcoronene Surface Models via GFN2‑xTB"**

Using the GFN2‑xTB semi‑empirical tight‑binding method with ALPB implicit water solvation, we systematically investigated the adsorption of eight PFAS compounds (C1–C8, both perfluorocarboxylates and perfluorosulfonates) on pristine circumcoronene (C₅₄H₁₈) and its hydroxylated derivative (C₅₄H₁₇OH). The study provides the first molecular‑level quantification of the thermodynamic basis for GAC treatment failure with ultrashort‑chain PFAS.

### Key Findings

- **Adsorption energies** range from **−11.3 kcal mol⁻¹** (TFA, C2 carboxylate) to **−18.3 kcal mol⁻¹** (PFOS, C8 sulfonate) on pristine circumcoronene.
- **Perfluorosulfonates** adsorb **1.5–4 kcal mol⁻¹ more strongly** than perfluorocarboxylates at every chain length.
- **C1–C4 PFAS** exhibit **pure physisorption** (charge transfer < 0.01 e), while **C8 homologs** show **partial chemisorption** (PFOA: +0.161 e, PFOS: +0.173 e).
- **Surface hydroxylation** imposes a **uniform penalty of +4.8 to +5.2 kcal mol⁻¹**, independent of chain length or headgroup.
- **Deprotonated PFOA⁻ and PFOS⁻** adsorb **3.8–5.9 kcal mol⁻¹ more strongly** than their neutral forms.
- **GFN2‑xTB** is benchmarked against B3LYP‑D3/6‑31G* on coronene, with a mean absolute deviation of **1.4 kcal mol⁻¹**.


## Computational Details

- **Software**: xTB 6.6.1 (GFN2‑xTB), RDKit 2023.09, PySCF 2.5.0, Python 3.10
- **Surface models**: Circumcoronene (C₅₄H₁₈, 72 atoms) and hydroxylated circumcoronene (C₅₄H₁₇OH, 73 atoms)
- **PFAS library**: TFA (C2), PFMS (C1), PFPrA (C3), PFPrS (C3), PFBA (C4), PFBS (C4), PFOA (C8), PFOS (C8) – neutral and deprotonated (PFOA⁻, PFOS⁻)
- **Solvation**: ALPB implicit water (ε = 80.2)
- **Conformational sampling**: Three initial orientations (planar, tilted, perpendicular) per complex
- **DFT benchmark**: B3LYP‑D3/6‑31G* on coronene (C₂₄H₁₂) using PySCF

## Usage

### Run the full analysis on Google Colab

1. Click the **Open In Colab** badge at the top of this README.
2. Run all cells sequentially. The notebook will:
   - Install all dependencies (xTB, RDKit, PySCF)
   - Generate and optimize all PFAS monomers and surface models
   - Build and optimize adsorption complexes (3 orientations per complex)
   - Extract adsorption energies and Mulliken charge transfer
   - Run the DFT benchmark (TFA, PFBS, PFOA)
   - Generate all figures (SVG, PDF, PNG)
   - Save results to Google Drive (optional)

**Total runtime**: ~60–90 minutes on Colab free tier.

### Run locally (Linux / macOS)

```bash
# Clone the repository
git clone https://github.com/Hasaneve/GFN2-xTB_PFAS.git
cd GFN2-xTB_PFAS

# Install dependencies
conda create -n pfas python=3.10
conda activate pfas
conda install -c conda-forge rdkit xtb
pip install pyscf pyscf-dispersion matplotlib ase pubchempy

# Run the notebook
jupyter notebook PFAS_benchmark.ipynb
