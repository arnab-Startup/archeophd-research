# Density-Based Clustering & Dimensionality Reduction (HDBSCAN over UMAP)

> **Subproject:** Visual Sorting & Typology Studio  
> **Section:** 03 — Clustering & Active Learning  
> **Status:** Production Reference  

---

## 1. Why Classical K-Means Fails in Archaeology

Most consumer clustering tools employ classical $K$-Means or Gaussian Mixture Models. In archaeological artifact analysis, $K$-Means produces severe analytical errors:

1. **Unknown Number of Classes ($K$):** An archaeologist never knows in advance how many pottery fabrics or lithic types exist in an unstudied trench. Forcing the user to pick $K=12$ forces real distinct types to artificially merge or split.
2. **Spherical Cluster Assumption:** $K$-Means assumes clusters are spherical and equal in diameter. Archaeological typologies have widely varying distributions (e.g., 500 coarse cooking pot sherds vs. 6 rare imported painted sherds).
3. **The Outlier Poisoning Effect:** $K$-Means forces *every single data point* into a cluster. When a unique, bizarre, or broken unidentifiable object appears, $K$-Means pulls the cluster centroid toward the noise, corrupting the entire group.

---

## 2. The Solution: UMAP + HDBSCAN

ArchaeoPhD AI couples **Uniform Manifold Approximation and Projection (UMAP)** with **Hierarchical Density-Based Spatial Clustering of Applications with Noise (HDBSCAN)**:

```
[384-dimensional DINOv2 Feature Vectors (N = 5,000)]
                          │
                          ▼
        [Metric Dimensionality Reduction (UMAP)]
        - Preserves local and global neighborhood topology
        - Reduces 384-d -> 15-d intermediate manifold
                          │
                          ▼
            [Density Clustering (HDBSCAN)]
            - Builds minimum spanning tree across mutual reachability distance
            - Condenses tree to extract stable clusters across density levels
                          │
                          ├─────────────────────────────────────────┐
                          ▼                                         ▼
            [Dense Clusters (Label >= 0)]             [Noise / Outlier Tray (Label = -1)]
            - Group 1: Red Slip Bowl Rims (n = 84)    - 14 Unique / Heavily Corroded Items
            - Group 2: Grey Burnished Jars (n = 42)     (Never forced into ill-fitting bins)
            - Group 3: Painted Geometrics (n = 19)
```

---

## 3. Mathematical Mechanics of HDBSCAN

### 3.1 Mutual Reachability Distance
For any two artifacts $p$ and $q$, the mutual reachability distance $d_{\text{mreach}}(p, q)$ is defined as:
$$d_{\text{mreach}-k}(p, q) = \max\left( \text{core}_k(p),\; \text{core}_k(q),\; d(p, q) \right)$$
Where $\text{core}_k(p)$ is the distance from point $p$ to its $k$-th nearest neighbor in embedding space. This spreads out sparse noise points while preserving dense clusters.

### 3.2 The "Outlier Tray" Advantage (Label = -1)
In archaeological science, **outliers are often the most scientifically significant finds** (e.g., a rare foreign trade import, a coin hoard, an unprecedented figurine).
* HDBSCAN naturally isolates these items into an explicit **"Unique Finds / Outliers"** tray.
* The specialist can review the outlier tray separately without having the main typological groups contaminated.
