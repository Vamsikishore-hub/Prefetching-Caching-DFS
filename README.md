# Frequent Pattern-Based Prefetching and Caching for Cloud Storage Systems

> Graph-based frequent pattern mining + LSTM machine learning to optimize read operations in Distributed File Systems — research 

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Vamsikishore-hub/Prefetching-Caching-DFS/blob/main/Prefetching_Caching_DFS.ipynb)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://python.org)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-2.12%2B-orange)](https://tensorflow.org)


---

## Results

| Metric | Value |
|--------|-------|
| Total weblog sessions | 9,787 |
| Frequent patterns mined | 129,830 |
| LSTM Architecture | LSTM(50) → Dropout(0.2) → Dense(1) |
| RMSE | 5.33 |
| MAE | 5.07 |
| LRU Cache Hit Rate | 41.30% |
| **Proposed Prefetch Hit Rate** | **43.21%** |
| **Improvement over LRU** | **+1.91%** |

---

## Overview

Modern distributed file systems (DFS) struggle with high read latency when handling large-scale, unpredictable data access patterns. This project proposes a three-stage solution:

1. **Graph-based Frequent Pattern Mining** — Convert real-world Amazon weblog data into weighted directed graphs; prune infrequent nodes and edges; extract high-frequency access patterns with support and frequency scores
2. **LSTM Prediction** — Train a Long Short-Term Memory model on mined patterns to predict future data block access sequences
3. **Intelligent Prefetching** — Use predicted patterns to proactively cache high-demand data blocks before they are requested, reducing mean read access time compared to traditional LRU caching

---

## Prerequisites

- Python 3.8 or above
- Google Colab (recommended — no setup needed) or Jupyter Notebook
- Git

---

## Quick Start (Google Colab)

1. Click the **Open in Colab** badge above
2. Click **Runtime → Run all**
3. Upload `logsmall.txt` when prompted in Step 3
4. All 10 steps run automatically — results and charts generated at the end

---

## Local Setup

### 1. Clone the Repository
```bash
git clone https://github.com/Vamsikishore-hub/Prefetching-Caching-DFS.git
cd Prefetching-Caching-DFS
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. Run the Notebook
```bash
jupyter notebook Prefetching_Caching_DFS.ipynb
```

---

## Pipeline Architecture

```
Amazon Weblog Data (logsmall.txt)
  RackID | AppID | UserID | DataNodeID | FileID | BlockIDs
        │
        ▼
  ┌─────────────────────┐
  │  Data Preprocessing │  Remove consecutive duplicate blocks
  │  Session Grouping   │  Group by RackID + DataNodeID
  └─────────┬───────────┘
            │
            ▼
  ┌─────────────────────┐
  │  Graph Construction │  Nodes=Blocks, Edges=Transitions
  │  Graph Pruning      │  Remove infrequent nodes/edges
  └─────────┬───────────┘
            │
            ▼
  ┌─────────────────────┐
  │  Pattern Mining     │  2-hop and 3-hop frequent patterns
  │  129,830 patterns   │  with frequency, length, support
  └─────────┬───────────┘
            │
            ▼
  ┌─────────────────────┐
  │  LSTM Training      │  50 units, Adam, Early Stopping
  │  RMSE: 5.33         │  Predicts future access sequences
  └─────────┬───────────┘
            │
            ▼
  ┌─────────────────────┐
  │  Prefetch Simulation│  LSTM Prefetch vs Traditional LRU
  │  +1.91% improvement │  Across cache sizes 5, 10, 20, 30, 50
  └─────────────────────┘
```

---

## Dataset

**File:** `logsmall.txt`

**Format:** `RackID, AppID, UserID, DataNodeID, FileID, BlockIDs, SessionID`

**Example:**
```
R1,A5,U465,D2,F33,B7 B10 B2 B41 B99 B15 B47,1
R5,A3,U786,D1,F987,B78 B13 B7 B1 B15 B2 B21,2
```

| Property | Value |
|---|---|
| Total sessions | 9,787 |
| Unique Racks | 10 |
| Unique DataNodes | 10 |
| Unique Files | 979 |
| Source | Amazon weblog data |

---

## Notebook Steps

| Step | Description | Output |
|------|-------------|--------|
| 1 | Install dependencies | — |
| 2 | Import libraries | — |
| 3 | Upload & parse weblog data | Session dataframe |
| 4 | Preprocessing & session grouping | Cleaned sessions |
| 5 | Graph construction & pruning | 100 pruned graphs |
| 6 | Frequent pattern mining | 129,830 patterns, patterns.csv |
| 7 | LSTM model training | Trained model, training_loss.png |
| 8 | Model evaluation | MSE, RMSE, MAE metrics |
| 9 | Prefetching simulation | LRU vs Prefetch comparison chart |
| 10 | Summary & export | All results + CSV files |

---

## Generated Output Files

After running the notebook, the following files are generated:

| File | Description |
|------|-------------|
| `patterns.csv` | All 129,830 mined frequent patterns |
| `simulation_results.csv` | Cache hit rates across all cache sizes |
| `session_distribution.png` | Sessions per Rack and DataNode |
| `graph_comparison.png` | Original vs pruned graph visualization |
| `pattern_distribution.png` | Pattern length and frequency distributions |
| `training_loss.png` | LSTM training vs validation loss |
| `predictions_vs_actual.png` | LSTM predictions vs actual values |
| `prefetch_comparison.png` | LRU vs proposed method comparison |

---

## Tech Stack

| Layer | Technology |
|-------|------------|
| Data Processing | Python, Pandas, NumPy |
| Graph Mining | NetworkX |
| Machine Learning | TensorFlow 2.x, Keras (LSTM) |
| Preprocessing | Scikit-learn (LabelEncoder, MinMaxScaler) |
| Visualization | Matplotlib, Seaborn |
| Environment | Google Colab / Jupyter Notebook |

---

## Research Publication

**Frequent Patterns-based Prefetching and Caching for Improving the Performance of Cloud Storage Systems**

Ms. Anusha Nalajala¹, Kolli Deepthi², Mediboena Lavanya Deepthi², Anusha Kandula², **Vamsi Kishore Nallagopu²**

¹ Department of Computer Science and Engineering, SRM University – AP *(Supervisor)*
² Department of Computer Science and Engineering, SRM University – AP



---

## Troubleshooting

**Step 6 takes too long:**
- The pattern mining uses efficient 2-3 hop edge traversal (O(E) complexity)
- Should complete in under 30 seconds

**Step 7 LSTM is slow:**
- Early stopping is enabled — training stops automatically when validation loss plateaus
- Typically finishes in 10–20 epochs out of max 50

**No patterns found:**
- Try reducing `min_support=2` to `min_support=1` in Step 6

**Upload error in Step 3:**
- Make sure you upload `logsmall.txt` exactly as downloaded from this repo

---

## Affiliation

Built by **Vamsi Kishore Nallagopu**
Under SRM University AP
[GitHub](https://github.com/Vamsikishore-hub) | [LinkedIn](https://www.linkedin.com/in/vamsi-kishore-nallagopu-097707240/)
