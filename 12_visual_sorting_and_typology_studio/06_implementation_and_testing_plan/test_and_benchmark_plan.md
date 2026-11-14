# Testing & Benchmark Evaluation Protocol

> **Subproject:** Visual Sorting & Typology Studio  
> **Section:** 06 — Implementation & Testing Plan  
> **Status:** Production Reference  

---

## 1. Test Corpus & Benchmark Datasets

To ensure rigorous scientific validation, the engine will be tested on three distinct archaeological datasets:

1. **Benchmark Set 1: Mediterranean Bronze Age Ceramics (1,200 images):**
   - 4 dominant wares (Red Slip, Grey Burnished, Painted Geometric, Coarse Cooking).
   - Ground truth: Manual expert typological classifications by senior specialists.
2. **Benchmark Set 2: Paleolithic Chipped Stone Lithics (800 images):**
   - Retouched tools vs. unretouched flakes vs. bladelet cores vs. angular debris.
   - Ground truth: Morphometric measurements and lithic drawing catalogs.
3. **Benchmark Set 3: Adversarial Field Noise Set (300 images):**
   - Extreme trench shadows, dirty muddy specimens, hands holding objects, broken scale bars.

---

## 2. Evaluation Metrics

| Metric | Target | Measurement Method |
|---|---|---|
| **Foreground Mask IoU (Intersection over Union)** | **$\ge 92.5\%$** | Overlap between automated segmentation mask and hand-annotated ground truth mask. |
| **Cluster Purity (Homogeneity)** | **$\ge 85.0\%$** | Percentage of items in a cluster that belong to the dominant ground truth class. |
| **Outlier Recall** | **$\ge 90.0\%$** | Percentage of genuine unique/anomalous finds correctly routed to Cluster -1. |
| **Human Ejections to Convergence** | **$< 5$ per 100 items** | Average number of `X` keystrokes required before a cluster achieves 100% purity. |
| **CPU Processing Latency** | **$< 45$ ms / image** | Total time for segmentation + DINOv2 embedding generation on Intel Core i7. |
| **Re-clustering Feedback Latency** | **$< 80$ ms** | Time between pressing `X` and rendering next-best recommendation in UI. |
