# Link Prediction Experiments

## Overview
This repository contains experimental code for link prediction on two graph datasets:
- **CiteSeer** (undirected citation network)
- **Congress Twitter Network** (directed influence network)

Implemented methods: CN, AA, Katz, DeepWalk, Node2Vec, GCN, GraphSAGE, SEAL.

## Contents
- `experiments.ipynb` - main Jupyter notebook with all experiments
- `congress_data/` - Congress Twitter Network dataset
- `*.png` - generated plots (loss curves, hyperparameter tuning)
- `final_results.csv` - aggregated results table
- `requirements.txt` - Python dependencies

## Setup

```bash
pip install -r requirements.txt
```

## Running
Start Jupyter Lab:

```bash
jupyter lab experiments.ipynb
```

## Results

| Dataset | Method | Value |
|---------|--------|-------|
| CiteSeer | CN | 3 |
| CiteSeer | AA | 2.19 |
| CiteSeer | Katz | 4.74 |
| CiteSeer | DeepWalk | 0.478 (loss) |
| CiteSeer | GCN | 0.753 (AUC) |
| CiteSeer | GraphSAGE | 0.617 (AUC) |
| CiteSeer | SEAL | 0.897 (AUC) |
| Congress | CN_dir | 11 |
| Congress | AA_dir | 2.46 |
| Congress | DeepWalk | 2.50 (loss) |
| Congress | GCN | 0.732 (AUC) |
| Congress | GraphSAGE | 0.566 (AUC) |

## Notes
- Congress Network is processed as directed (no symmetrization)
- SEAL runs on CiteSeer only
- GraphSAGE on CiteSeer: best aggregator = 'mean'
- Katz on CiteSeer: optimal beta = 0.45 (beyond 0.5 series diverges)

## Requirements
Python 3.8+, PyTorch 2.0+, DGL 1.0+, PyTorch Geometric 2.3+

See `requirements.txt` for full list.

## Data Sources
- CiteSeer: Planetoid dataset from PyTorch Geometric
- Congress Network: Fink et al., Physica A 2023

## License
MIT
