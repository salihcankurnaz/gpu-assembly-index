# GPU Assembly Index Calculator

> **Research status:** experimental implementation for exact-search and learned/predictive Molecular Assembly Index workflows. Predictor throughput is not equivalent to exact MA computation.
**GPU-oriented research tooling for Molecular Assembly Index experiments.**

Assembly Index (MA) is an assembly-theory complexity measure based on construction/joining operations. High assembly values have been studied as potential biosignature-related signals, but this repository does not establish a universal life/non-life threshold.

## Execution modes and benchmarking

- **Exact CPU path:** molecular graph processing plus bounded fragment-search heuristics.
- **Predictive GPU path:** molecular fingerprints plus a learned/regression-style estimator.

These are different computational tasks. Predictor throughput must not be reported as an
exact-computation speedup. Historical local throughput figures previously shown in this
README are omitted until a reproducible benchmark artifact records the exact dataset,
hardware/software environment, accuracy metrics, and timing protocol.
## How It Works

1. **Exact computation** (CPU): RDKit molecular graph + branch-and-bound fragment search
2. **GPU prediction** (CuPy): Morgan fingerprint + ridge regression trained on exact values
3. **Validation**: use the repository validation scripts to compare exact-search outputs, predictor outputs, and selected reference values; commit raw results before making quantitative accuracy claims

## Validation

`validate.py` contains an exploratory comparison against a small set of hard-coded,
approximate literature reference values and additional drug-screening experiments.
The script itself notes that the greedy implementation may differ from those values.
No committed run artifact in the current repository establishes the previous
"14/14 validated correctly" headline, so that claim has been removed.

Treat literature comparisons, predictor accuracy, and screening thresholds as research
experiments that require rerunning and preserving raw outputs.
## Potential research uses

- studying exact versus approximate/predictive assembly-index computation;
- screening chemical datasets under explicitly stated assumptions;
- exploring molecular-complexity features in astrobiology or cheminformatics research;
- benchmarking graph-search and learned surrogate approaches.

These are research directions, not validated deployment or biosignature-detection claims.
## Requirements

- Python 3.11+
- RDKit 2025.9+
- CuPy 14+ (CUDA 12/13)
- NumPy 2.0+

## Quick Start

```python
from assembly_index import compute_ma, gpu_predict_ma
from rdkit import Chem

# Exact computation
mol = Chem.MolFromSmiles("CC(=O)OC1=CC=CC=C1C(=O)O")  # Aspirin
ma = compute_ma(mol)
print(f"Aspirin MA = {ma}")  # 9

# GPU batch prediction (millions of molecules)
smiles_list = [...]  # your SMILES
predicted_ma = gpu_predict_ma(smiles_list)
```

## License

No root `LICENSE` file is currently committed. Treat the repository source as unlicensed
until a separate provenance/license review is completed.
## Citation

If you use this tool, please cite:
- Assembly Theory: Marshall et al., Nature 2023
- This GPU implementation: github.com/salihcankurnaz/gpu-assembly-index
