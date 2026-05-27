# Link Prediction: Comparative Study on CiteSeer and Congress Network

## Description
This repository contains experiments for link prediction on two graph types:
- **CiteSeer** (undirected citation network, 3,327 nodes, 9,104 edges)
- **Congress Twitter Network** (directed influence network, 475 nodes, 13,289 edges)

Implemented methods:
- Heuristics: Common Neighbors (CN), Adamic-Adar (AA)
- Katz Index with beta grid search
- DeepWalk (DGL implementation)
- Node2Vec (node2vec library)
- GCN (DGL GraphConv)
- GraphSAGE (DGL SAGEConv)
- SEAL (PyG implementation, CiteSeer only)

## Requirements
See `requirements.txt`. Python 3.8+ recommended.

## Installation
```bash
pip install -r requirements.txt
