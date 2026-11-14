# Active Learning & Must-Not-Link Constraints

> **Subproject:** Visual Sorting & Typology Studio  
> **Section:** 03 — Clustering & Active Learning  
> **Status:** Production Reference  

---

## 1. Overview of the Interactive Feedback Loop

The core promise of the Visual Typology Studio is that **the human specialist remains in total authority**:
* When an archaeologist inspects a proposed visual group (e.g., "Cluster 3: 40 Red Bowls") and spots an intrusive cooking pot sherd, they do not manually reconfigure model hyper-parameters.
* They simply click **"Reject" (or press `X`)**.
* The engine treats this human rejection as a formal **Must-Not-Link constraint** in semi-supervised clustering, instantly updating the classification of the entire batch.

---

## 2. Mathematical Formulation of Semi-Supervised Constraints

In metric space clustering, user feedback introduces two fundamental pairwise constraints:
1. **Must-Link Constraint ($\mathcal{M}$):** Indicates that artifact $i$ and artifact $j$ belong to the same typological class.
   $$\forall (i, j) \in \mathcal{M}, \quad \text{Cluster}(i) = \text{Cluster}(j)$$
2. **Must-Not-Link Constraint ($\mathcal{C}$):** Indicates that artifact $i$ and artifact $j$ must **never** be placed in the same typological class.
   $$\forall (i, j) \in \mathcal{C}, \quad \text{Cluster}(i) \ne \text{Cluster}(j)$$

### 2.1 Ejection as a Cluster-Level Must-Not-Link Rule
When an archaeologist rejects Image $X$ from Cluster $A$:
$$\mathcal{C} \longleftarrow \mathcal{C} \cup \{ (X, Y) \mid Y \in \text{Cluster } A \}$$
The affinity distance between $X$ and Cluster $A$ is penalized toward infinity:
$$D_{\text{penalized}}(X, A) = \infty$$
This guarantees that Image $X$ can never be re-assigned to Cluster $A$ in subsequent automated sorting iterations.

---

## 3. Metric Space Warping via Active Learning

To ensure the system learns the *reason* for rejection:
* If the user rejects an item and moves it to Cluster $B$ (e.g., "Coarse Ware"), the system computes the feature difference vector:
  $$\mathbf{\Delta} = \mathbf{v}_X - \mathbf{\mu}_A$$
* The system projects subsequent candidates onto this axis, dynamically down-weighting the features that caused the misclassification (e.g., ignoring surface burnishing gloss if the underlying fabric core is coarse).
* **Latency:** This metric update is executed in $<10\text{ ms}$ on CPU using local vector algebra, providing seamless, real-time visual feedback in the UI.
