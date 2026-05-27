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
