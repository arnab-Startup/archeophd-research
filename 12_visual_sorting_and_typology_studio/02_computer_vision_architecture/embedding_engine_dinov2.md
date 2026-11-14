# Visual Embedding Engine: DINOv2 Architecture

> **Subproject:** Visual Sorting & Typology Studio  
> **Section:** 02 — Computer Vision Architecture  
> **Status:** Production Reference  

---

## 1. Why Self-Supervised Vision Transformers (DINOv2)?

Standard supervised computer vision models (e.g., ImageNet-trained ResNets) fail on archaeological artifacts because ImageNet classes ("dog", "car", "toaster") do not encode archaeological features:
* They prioritize semantic object-level labels over fine-grained surface morphology and fracture patterns.

**DINOv2 (Vision Transformer trained via self-supervised learning with student-teacher distillation)** is uniquely suited for archaeological typology:
1. **No Human Class Labels Required:** Learns directly from visual patch correlations across 142M uncurated images.
2. **Dense Patch-Level Geometry:** Encodes sharp contour curvature (rim profiles, carination angles, flake scars) and micro-texture (paste inclusions, burnishing strokes, slip gloss).
3. **Robust to Illumination Variations:** Preserves invariant geometric representations across varying exposure levels.

---

## 2. Feature Extraction Mechanics

```
       [Segmented Artifact Image (224x224 RGB)]
                         │
                         ▼
        [Patch Tokenization: 16x16 Non-overlapping Patches]
                         │
                         ▼
   [Vision Transformer Blocks (Multi-Head Self-Attention)]
                         │
                         ├─────────────────────────────────────────┐
                         ▼                                         ▼
            [Global [CLS] Token (384-d)]               [Local Patch Tokens (196x384-d)]
                         │                                         │
                         ▼                                         ▼
           Encodes Overall Vessel Form                Encodes Fine Surface Paste,
           & Silhouette Morphology                    Slip Texture, & Retouch Scars
                         │                                         │
                         └───────────────────┬─────────────────────┘
                                             ▼
                          [Concatenated & L2-Normalized Embedding]
                                  Vector Dimension: 384-d
```

### 2.1 Model Profile: `dinov2_vits14` (Small)

* **Architecture:** Vision Transformer (ViT-Small, 14x14 patch size).
* **Parameters:** 22 Million.
* **Embedding Dimension:** 384 dimensions.
* **Quantized File Size (INT8 ONNX):** **~23 Megabytes**.
* **CPU Inference Latency:** **~18–25 milliseconds per image** (on Intel Core i7 / AMD Ryzen laptop CPU).
* **Throughput:** ~40 to 50 images per second in multi-threaded CPU batches.

---

## 3. Mathematical Vector Normalization

To ensure Euclidean distance directly maps to cosine angular similarity, all generated feature vectors $\mathbf{x} \in \mathbb{R}^{384}$ undergo L2-normalization:
$$\mathbf{v} = \frac{\mathbf{x}}{\|\mathbf{x}\|_2} = \frac{\mathbf{x}}{\sqrt{\sum_{i=1}^{384} x_i^2}}$$
For any two normalized artifact vectors $\mathbf{u}$ and $\mathbf{v}$, cosine similarity simplifies to the vector dot product:
$$\text{Sim}(\mathbf{u}, \mathbf{v}) = \mathbf{u} \cdot \mathbf{v} = \sum_{i=1}^{384} u_i v_i$$
This dot product is executed via vectorized AVX2/AVX-512 SIMD instructions inside the native C++ desktop engine, computing thousands of comparisons per millisecond.
