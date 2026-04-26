# FAISS ANN Benchmark – SIFT1M Vector Search

## 📌 Project Overview
This project implements a large-scale vector similarity search benchmark using FAISS on the SIFT1M dataset. It compares Exact Nearest Neighbor search (IndexFlatL2) with Approximate Nearest Neighbor (ANN) methods (IndexIVFFlat, IndexHNSW) in terms of speed, memory efficiency, and accuracy.

The goal is to analyze how different indexing strategies behave under large-scale (1M vectors, 128 dimensions) conditions.

---

## 🎯 Objective
To evaluate the trade-off between:
- Query latency (speed)
- Recall (accuracy)
- Index build time
- Memory efficiency

in high-dimensional vector search systems.

---

## 📊 Methods Used
- IndexFlatL2 (Brute-force exact search)
- IndexIVFFlat (Inverted File Index)
- IndexHNSW (Graph-based ANN)

---

## 📁 Dataset
- SIFT1M dataset (1 million vectors, 128-dimensional SIFT descriptors)
- Contains:
  - base vectors (xb)
  - query vectors (xq)
  - training set (xt / learn)
  - ground truth results

> Dataset is automatically downloaded and extracted during execution.

---

## ⚙️ Evaluation Metrics
- Build Time (index construction cost)
- Query Latency (search speed)
- Recall@10 (accuracy of ANN methods)

---

## 🔍 Key Insight
Exact nearest neighbor search (IndexFlatL2) becomes computationally infeasible at large scale due to linear complexity. ANN methods provide a practical solution by significantly reducing search time with a controlled loss in accuracy.

---

## ⚖️ Pareto Analysis & Decision

From a Pareto efficiency perspective, the following conclusions can be drawn:

- **High Speed Requirement:** IndexHNSW is the most suitable choice for real-time systems due to its extremely low query latency, despite higher index construction cost.

- **Memory-Efficient / Balanced Systems:** IndexIVFFlat provides a flexible trade-off between speed and accuracy, with tunable parameters such as `nlist` and `nprobe` controlling performance.

- **Maximum Accuracy Requirement:** IndexFlatL2 is used as a brute-force baseline to guarantee 100% accurate nearest neighbor results, but it does not scale to large datasets.

These results demonstrate that the optimal index selection depends on system constraints such as latency requirements, memory usage, and acceptable accuracy loss.

---

## 🛠️ Requirements
```bash
pip install faiss-cpu numpy matplotlib psutil


Conclusion

This project demonstrates that Approximate Nearest Neighbor (ANN) algorithms are essential for scalable vector search systems. While exact search guarantees perfect accuracy, it becomes impractical at scale. ANN methods provide a strong balance between performance and accuracy, making them the standard choice in modern large-scale retrieval systems.
