# Link Prediction: Comparative Study on Cora and Congress

## Overview

This repository contains experimental code for link prediction comparing five classes of methods:

- **Local heuristics**: Common Neighbors (CN), Adamic-Adar (AA)
- **Path-based**: Katz index
- **Random walk embeddings**: DeepWalk
- **Graph neural networks**: GCN, GraphSAGE
- **Specialized**: SEAL (only for undirected graphs)

Experiments are conducted on two datasets:

- **Cora** (undirected citation network, 2,708 nodes, 10,556 edges) — with node features
- **Congress Twitter Network** (directed retweet/mention network, 475 nodes, 13,289 edges) — no node features

**Key improvements over previous versions:**

- No data leakage — all training structures are built exclusively from train edges
- Unified evaluation metrics: AUC-ROC and Average Precision (AP) for all methods
- Hyperparameter tuning via validation AUC
- Directed versions for Congress: `norm='right'` for GCN, directed random walks for DeepWalk

---

## Contents

```
.
├── experiments.ipynb               # Main Jupyter notebook (all experiments)
├── congress_data/                  # Congress Twitter Network dataset
│   └── congress_network/
│       └── congress_network_data.json
├── requirements.txt                # Python dependencies
├── final_results.csv               # Aggregated results table
└── *.png                           # Generated plots:
    ├── katz_tuning_cora.png
    ├── katz_tuning_congress.png
    ├── deepwalk_tuning_cora.png
    ├── deepwalk_tuning_congress.png
    ├── gcn_training_cora.png
    ├── gcn_training_cora_no_features.png
    ├── gcn_training_congress.png
    └── gcn_training_congress.png
```

---

## Setup

```bash
pip install -r requirements.txt
```

## Running

```bash
jupyter lab experiments.ipynb
```

Run cells sequentially. All random seeds are fixed (`seed=42`) for reproducibility.

---

## Results

### Cora (undirected)

| Method | AUC | AP |
|---|---|---|
| CN | 0.7452 | 0.7403 |
| AA | 0.7463 | 0.7448 |
| Katz | 0.9735 | 0.9730 |
| DeepWalk | 0.9792 | 0.9735 |
| GCN (with features) | 0.9995 | 0.9994 |
| GCN (no features) | 0.7600 | 0.7514 |
| GraphSAGE (with features) | 0.9979 | 0.9972 |
| GraphSAGE (no features) | 0.5000 | 0.5000 |
| SEAL | 0.9181 | — |

### Congress (directed, no node features)

| Method | AUC | AP |
|---|---|---|
| CN\_dir | 0.8459 | 0.8193 |
| AA\_dir | 0.8489 | 0.8359 |
| Katz | 0.8243 | 0.7314 |
| DeepWalk | 0.8031 | 0.7671 |
| GCN (norm='right') | 0.6385 | 0.6337 |
| GraphSAGE | 0.5000 | 0.5000 |

---

## Key Findings

- **Node features dominate on Cora**: GCN with 1433-d bag-of-words features achieves near-perfect AUC (0.9995)
- **Without features, structure-based methods shine**: DeepWalk (0.979) and Katz (0.973) outperform GCN without features (0.760)
- **Directed graphs are harder**: Best method on Congress is AA (0.849), GNNs underperform without features
- **GraphSAGE without features fails to converge**: AUC=0.5 (random) — likely due to low feature dimension (64) and missing normalization
- **SEAL is competitive but expensive**: AUC=0.918 on Cora, requires O(k³) per edge pair

---

## Hyperparameter Summary

| Method | Tuned | Fixed |
|---|---|---|
| CN/AA | — | threshold not needed (AUC) |
| Katz | β (validation AUC) | — |
| DeepWalk | walk\_length (10, 20, 40, 60, 80) | emb\_dim=64, window=5, neg=5, epochs=30 |
| GCN (Cora) | hidden\_dim (32, 64, 128), lr (0.001, 0.005, 0.01) | 2 layers, out=32, early\_stop=20 |
| GCN (Congress) | hidden\_dim (32, 64), lr (0.001, 0.005, 0.01) | norm='right' |
| GraphSAGE | fixed (hidden=64, lr=0.005, agg='mean') | for fair architecture comparison |
| SEAL | fixed (hops=2, hidden=32, layers=3) | from original paper, due to high complexity |

---

## Requirements

- Python 3.8+
- PyTorch 2.0+
- DGL 2.0+
- PyTorch Geometric 2.3+
- scikit-learn, numpy, pandas, matplotlib, networkx, scipy

See `requirements.txt` for full list.

---

## Data Sources

- **Cora**: Planetoid dataset from PyTorch Geometric (citation network)
- **Congress Network**: Fink et al., *"Quantifying the influence of US Congress members on Twitter"*, Physica A 2023

---

## Notes

- SEAL runs on Cora only (undirected, with node features)
- GraphSAGE without features on Cora and GraphSAGE on Congress did not converge (AUC=0.5) — this is reported as a limitation
- All experiments run on CPU (DGL CUDA support not required for these dataset sizes)

---

## License

MIT
