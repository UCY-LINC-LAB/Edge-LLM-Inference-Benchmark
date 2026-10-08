# LLM edge continuum inference analysis

This repository contains the analysis artifact for the paper **A Measurement Study of LLM Inference Trade-offs Across Edge-Continuum Hardware**.

The paper studies how model choice, quantization, execution platform, latency, memory footprint, energy, and streamed-token delivery overhead affect LLM deployment decisions across the edge continuum. The analysis uses two result files produced by the benchmarking pipeline and recreates the main post-processing steps used for the paper figures.

## What is included

```text
.
├── data
│   ├── results.csv
│   └── results_chatgpt.csv
├── figures
├── analysis_utils.py
├── CITATION.cff
├── README.md
└── requirements.txt
```

## Analysis overview

The notebook focuses on four parts of the paper analysis.

1. Loading and validating the self-hosted and cloud-reference measurements.
2. Comparing accuracy, model size, latency, and energy across models and devices.
3. Computing accuracy-latency Pareto frontiers for the self-hosted deployments.
4. Recomputing the Pareto frontier after adding effective streamed-token delivery overhead to server-side deployments.

The main notebook is available at `notebooks/analysis.ipynb`. The helper functions are placed in `src/analysis_utils.py` so that the notebook stays readable and the same logic can be reused by scripts.

## Quick start

Create a Python environment and install the required packages.

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Validate the input data.

```bash
python scripts/validate_data.py
```

Generate all figures from the command line.

```bash
python scripts/generate_figures.py
```

Open the documented notebook.

```bash
jupyter lab notebooks/analysis.ipynb
```

The code is written to work when launched either from the repository root or from inside the `notebooks` directory.

## Data files

`data/results.csv` contains self-hosted measurements for Orin, Server GPU, and Server CPU deployments. `data/results_chatgpt.csv` contains the GPT-4o cloud-reference run. The cloud reference is used for accuracy and latency comparison, but it is excluded from energy analysis because the API does not expose hardware-level power or utilization metrics.

## Generated figures

Running `scripts/generate_figures.py` or the notebook writes the following files under `figures`.

```text
energy_per_trial.png
prefill_latency_per_token.png
decode_latency_per_token.png
orin_cloud_accuracy_size_duration.png
pareto_frontiers.png
```

## Citation

If you use this repository, its datasets, or its analysis code, please cite the following paper:

```bibtex
@inproceedings{khatib2026WIMS,
  title     = {A Measurement Study of LLM Inference Trade-offs Across Edge-Continuum Hardware},
  author    = {Khatib, Maysam and Symeonides, Moysis and Trihinas, Demetris and Pallis, George and Dikaiakos, Marios D.},
  booktitle = {Proceedings of the 16th International Conference on Web Intelligence, Mining and Semantics (WIMS)},
  year      = {2026}
}
```

## License

This repository is licensed under the Apache License, Version 2.0.
See the LICENSE file for details.
