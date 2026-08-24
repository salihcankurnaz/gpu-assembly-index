# GPU Assembly Index Calculator

> **Research status:** experimental implementation for exact-search and learned/predictive Molecular Assembly Index workflows. Predictor throughput is not equivalent to exact MA computation.

**GPU-oriented research tooling for Molecular Assembly Index experiments.**

Assembly Index (MA) is an assembly-theory complexity measure based on construction/joining operations. High assembly values have been studied as potential biosignature-related signals, but this repository does not establish a universal life/non-life threshold.

## Execution modes and benchmarking

- **Exact CPU path:** molecular graph processing plus bounded fragment-search heuristics.
- **Predictive GPU path:** molecular fingerprints plus a learned/regression-style estimator.

These are different computational tasks. Predictor throughput must not be reported as an exact-computation speedup. Historical local throughput figures previously shown in this README are omitted until a reproducible benchmark artifact records the exact dataset, hardware/software environment, accuracy metrics, and timing protocol.

## How it works

1. **Exact computation** (CPU): RDKit molecular graph + bounded/heuristic fragment search.
2. **GPU prediction** (CuPy): molecular fingerprint features + learned/regression-style prediction.
3. **Validation:** repository validation scripts can compare exact-search outputs, predictor outputs, and selected reference values; quantitative claims should preserve raw outputs and the exact evaluation protocol.

## Model provenance

The committed `ma_model.pt` artifact is documented in [`MODEL_PROVENANCE.md`](MODEL_PROVENANCE.md). That file should be read together with any result produced by the predictive path: a committed model artifact is not, by itself, evidence that a particular accuracy or throughput claim holds on a new dataset.

## Validation

`validate.py` contains an exploratory comparison against a small set of hard-coded, approximate literature reference values and additional drug-screening experiments. The script itself notes that the greedy implementation may differ from those values.

No committed run artifact in the current repository establishes the previous "14/14 validated correctly" headline, so that claim is not made here.

Treat literature comparisons, predictor accuracy, and screening thresholds as research experiments that require rerunning and preserving raw outputs.

## Continuous integration

GitHub Actions performs CPU-safe repository hygiene checks:

- Python source compilation on Python 3.10, 3.11, and 3.12;
- presence validation for [`MODEL_PROVENANCE.md`](MODEL_PROVENANCE.md).

The workflow intentionally does **not** claim to validate RDKit/CuPy runtime behavior, GPU performance, predictor accuracy, or exact Assembly Index correctness. Those require explicit environment/data-specific validation.

## Potential research uses

- studying exact versus approximate/predictive assembly-index computation;
- screening chemical datasets under explicitly stated assumptions;
- exploring molecular-complexity features in astrobiology or cheminformatics research;
- benchmarking graph-search and learned surrogate approaches.

These are research directions, not validated deployment or biosignature-detection claims.

## Requirements

- Python 3.11+
- RDKit 2025.9+
- CuPy 14+ for the GPU-oriented prediction path
- NumPy 2.0+

## Quick start

```python
from assembly_index import compute_ma, gpu_predict_ma
from rdkit import Chem

mol = Chem.MolFromSmiles("CC(=O)OC1=CC=CC=C1C(=O)O")
ma = compute_ma(mol)
print(ma)

smiles_list = [...]  # your SMILES
predicted_ma = gpu_predict_ma(smiles_list)
```

Any printed/example value should be treated as an output of the current implementation, not as a literature-ground-truth value unless independently verified.

## License

MIT License. See [`LICENSE`](LICENSE).

## Citation

If you use this tool, cite the relevant Assembly Theory literature and this repository/version used for your experiment:

- Marshall et al., *Nature* (2023) for Assembly Theory context;
- `https://github.com/salihcankurnaz/gpu-assembly-index` for this experimental implementation.
