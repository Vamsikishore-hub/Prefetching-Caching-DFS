<<<<<<< HEAD
# Frequent Pattern-Based Prefetching and Caching for Cloud Storage Systems

A research implementation of graph-based frequent pattern mining combined with LSTM machine learning to optimize read operations in Distributed File Systems (DFS).

Published research paper submitted to **ICCNT 2024** by Vamsi Kishore Nallagopu et al., SRM University – AP.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Vamsikishore-hub/Prefetching-Caching-DFS/blob/main/Prefetching_Caching_DFS.ipynb)

---

## Overview

Modern distributed file systems struggle with read latency due to high-volume, unpredictable data access patterns. This project proposes a solution:

1. **Mine frequent access patterns** from real-world Amazon weblog data using graph-based algorithms
2. **Train an LSTM model** to predict future data access sequences
3. **Prefetch high-demand data blocks** proactively into cache before they are requested
4. **Reduce read latency** significantly compared to traditional LRU caching

---

## Prerequisites

- Python 3.8 or above
- Google Colab (recommended) or Jupyter Notebook
- Git

---

## Quick Start (Google Colab — Recommended)

1. Click the **Open in Colab** badge above
2. Upload `logsmall.txt` when prompted in Step 3
3. Run all cells: **Runtime → Run all**

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

## Pipeline

```
Amazon Weblog Data (logsmall.txt)
        ↓
  Data Preprocessing
  (Rack ID, App ID, User ID, DataNode ID, File ID, Block IDs)
        ↓
  Graph Construction
  (Nodes = Blocks, Edges = Transitions, Weight = Frequency)
        ↓
  Graph Pruning
  (Remove infrequent nodes and edges)
        ↓
  Frequent Pattern Mining
  (Extract patterns with frequency, length, support)
        ↓
  LSTM Model Training
  (50 units, Adam optimizer, 200 epochs)
        ↓
  Prefetching Simulation
  (LSTM Prefetch vs Traditional LRU Cache)
        ↓
  Performance Evaluation
  (MSE, RMSE, MAE, Cache Hit Rate, Read Latency)
```

---

## Dataset

**File:** `logsmall.txt`

**Format:** `RackID, AppID, UserID, DataNodeID, FileID, BlockIDs, SessionID`

**Example:**
```
R1,A5,U465,D2,F33,B7 B10 B2 B41 B99 B15 B47,1
R5,A3,U786,D1,F987,B78 B13 B7 B1 B15 B2,2
```

**Size:** 9,786 weblog sessions across multiple racks and data nodes

---

## Results

| Metric | Value |
|--------|-------|
| MSE | 1066.49 |
| RMSE | 32.65 |
| MAE | 32.65 |
| Cache Hit Rate Improvement | LSTM Prefetch > LRU across all cache sizes |

---

## Notebook Structure

| Step | Description |
|------|-------------|
| 1 | Install dependencies |
| 2 | Import libraries |
| 3 | Upload and parse weblog data |
| 4 | Data preprocessing and session grouping |
| 5 | Graph construction and pruning |
| 6 | Frequent pattern mining |
| 7 | LSTM model training |
| 8 | Model evaluation (MSE, RMSE, MAE) |
| 9 | Prefetching simulation — LSTM vs LRU comparison |
| 10 | Final summary and export results |

---

## Tech Stack

| Component | Technology |
|-----------|------------|
| Data Processing | Python, Pandas, NumPy |
| Graph Mining | NetworkX |
| Machine Learning | TensorFlow, Keras (LSTM) |
| Visualization | Matplotlib, Seaborn |
| Preprocessing | Scikit-learn |

---

## Research Publication

**Frequent Patterns-based Prefetching and Caching for Improving the Performance of Cloud Storage Systems**
Ms. Anusha Nalajala, Kolli Deepthi, Mediboena Lavanya Deepthi, Anusha Kandula, Vamsi Kishore Nallagopu
Department of Computer Science and Engineering, SRM University – AP
Submitted to ICCNT 2024

---

## Affiliation

Built by **Vamsi Kishore Nallagopu**
M.S. Computer Science — California State University, San Bernardino
[GitHub](https://github.com/Vamsikishore-hub) | [LinkedIn](https://www.linkedin.com/in/vamsi-kishore-nallagopu-097707240/)
=======
# Prefetching-Caching-DFS
Graph-based frequent pattern mining + LSTM-driven prefetching to optimize read operations in Distributed File Systems | Research paper submitted to ICCNT 2024
>>>>>>> 9b5b6751af3fa3bf50f3b49b1866b79e03e1909a
