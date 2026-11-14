# Centroid Adaptation & Next-Best Candidate Routing

> **Subproject:** Visual Sorting & Typology Studio  
> **Section:** 03 — Clustering & Active Learning  
> **Status:** Production Reference  

---

## 1. Automated Routing Mechanics Upon Rejection

When an archaeologist rejects Image $X$ from Cluster $A$, the system does not dump the image into an unorganized heap. It executes an automated **Next-Best Routing Routine**:

```
[User Ejects Image X from Cluster A]
                   │
                   ▼
[1. Recalculate Cluster A Centroid without Image X]
                   │
                   ▼
[2. Measure Cosine Similarity to All Other Existing Clusters]
                   │
                   ├─────────────────────────────────────────┐
                   ▼                                         ▼
[Max Similarity >= Tau (e.g., 0.78)]        [Max Similarity < Tau (Novel Form)]
                   │                                         │
                   ▼                                         ▼
[Propose Top-2 Best-Fitting Alternative]     [Spawn New "Candidate Type B" Tray]
(e.g., "Move to Cluster 5: Grey Ware?")      (Placed in Unassigned Review Queue)
```

---

## 2. Mathematical Routing Formulation

### 2.1 Dynamic Centroid Recalculation
Let Cluster $A$ have $N$ member vectors $\{\mathbf{v}_1, \dots, \mathbf{v}_N\}$. When vector $\mathbf{v}_X$ is ejected:
$$\mathbf{\mu}_A^{(\text{new})} = \frac{1}{N - 1} \sum_{i \ne X} \mathbf{v}_i = \frac{N \mathbf{\mu}_A^{(\text{old})} - \mathbf{v}_X}{N - 1}$$
$$\mathbf{\mu}_A^{(\text{normalized})} = \frac{\mathbf{\mu}_A^{(\text{new})}}{\|\mathbf{\mu}_A^{(\text{new})}\|_2}$$
This $O(1)$ computation updates the cluster centroid instantaneously without scanning the rest of the dataset.

### 2.2 Next-Best Candidate Selection
The engine computes the similarity to all other active cluster centroids $k \in \{1, \dots, K\} \setminus \{A\}$:
$$s_k = \frac{\mathbf{v}_X \cdot \mathbf{\mu}_k}{\|\mathbf{v}_X\|_2 \|\mathbf{\mu}_k\|_2}$$
Let the ranked similarities be $s_{(1)} \ge s_{(2)} \ge \dots$:
* If $s_{(1)} \ge \tau_{\text{threshold}}$ (default $\tau = 0.75$):
  - The UI highlights the Top-1 cluster: *"Suggested Move: Cluster $k_{(1)}$ (Similarity: 84%)"*.
  - A single click on `Enter` confirms the move.
* If $s_{(1)} < \tau_{\text{threshold}}$:
  - The item is recognized as a **New Morphological Type Candidate**.
  - A new tray is created automatically with Image $X$ as its founding centroid $\mathbf{\mu}_{\text{new}} = \mathbf{v}_X$.
