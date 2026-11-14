# Background Isolation & Foreground Artifact Segmentation

> **Subproject:** Visual Sorting & Typology Studio  
> **Section:** 02 — Computer Vision Architecture  
> **Status:** Production Reference  

---

## 1. The Challenge of Unconstrained Field Photography

Photographs taken in active archaeological trenches suffer from severe environmental noise that corrupts naive computer vision models:
* Variable soil backgrounds (reddish clay, yellow silt, dark organic midden earth).
* Direct harsh sunlight, cast shadows from trench walls, and clouds.
* Human fingers, gloves, trowels, and plastic specimen trays.
* Photographic scale bars (black/white cm scales, blue plastic scales, folding wooden rulers).

### The "Background Trap" in Unsupervised Clustering
If raw, unsegmented photographs are fed into visual embedding models (e.g., CLIP or ResNet):
* The neural network encodes the dominant visual surface area — which is usually the **trench soil or background tray**.
* As a result, the model clusters photos by **trench lighting condition and soil color** rather than the archaeological morphology or ceramic fabric of the artifact.

---

## 2. Automated Foreground Segmentation Pipeline

To eliminate background bias, ArchaeoPhD AI implements a pre-processing segmentation pass:

```
[Raw Field Photo (Trench Soil + Artifact + Scale Bar)]
                        │
                        ▼
         [Edge-Aware Saliency Model (BiRefNet / U2-Net)]
                        │
                        ▼
               [Binary Alpha Mask]
                        │
                        ▼
         [Alpha Matte Blending on Neutral Background]
                        │
                        ▼
[Isolated Artifact Image (RGB + Alpha Matte on Neutral #F8F9FA)]
```

### 2.1 Model Evaluation for Local CPU Execution

| Model Architecture | Parameter Size | Memory (RAM) | CPU Inference / Image | Edge Precision | Archaeological Suitability |
|---|---|---|---|---|---|
| **SAM-2 (Segment Anything 2)** | 308 MB | ~1.2 GB | ~350 ms | High | High, but heavy for 10k batch CPU |
| **MobileSAM (Quantized)** | 39 MB | ~180 MB | ~45 ms | Medium-High | Very Good for real-time triage |
| **BiRefNet (Bilateral Reference)** | 140 MB | ~500 MB | ~95 ms | **Exceptional** | **Gold Standard (used in AviArch)** |
| **U2-Net / rembg (ONNX INT8)** | **44 MB** | **~120 MB** | **~28 ms** | High | **Optimal for CPU Desktop Workstation** |

### 2.2 Preserving Scale-Bar Geometry
While background dirt must be removed, the photographic scale bar contains critical absolute metric dimensional data:
1. The segmentation engine detects the scale bar as a secondary high-contrast geometric bounding box.
2. The pixel-to-millimeter ratio is calculated from the scale ticks and stored in metadata (`ScaleRatio = mm_per_pixel`).
3. The scale bar is masked out of the typological embedding input so its color does not bias clustering, but its spatial calibration is retained for plate generation.
