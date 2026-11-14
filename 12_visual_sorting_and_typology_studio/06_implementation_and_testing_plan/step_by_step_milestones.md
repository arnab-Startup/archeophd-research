# Step-by-Step Implementation Milestones

> **Subproject:** Visual Sorting & Typology Studio  
> **Section:** 06 — Implementation & Testing Plan  
> **Status:** Production Reference  

---

## 1. Phased Development Roadmap

The Visual Typology Studio will be delivered in four focused, verifiable phases:

```
+---------------------------------------------------------------------------------------------------+
| PHASE 1: Image Ingestion, Segmentation & Scale Calibration (Weeks 1–2)                            |
| - Ingest raw JPEG/PNG/TIFF folders with EXIF metadata parsing.                                    |
| - Integrate quantized U2-Net / MobileSAM ONNX model for background masking.                       |
| - Detect scale bar and calculate mm-per-pixel ratio.                                              |
| - Exit Criteria: Clean foreground artifact crops on neutral background generated locally on CPU.  |
+---------------------------------------------------------------------------------------------------+
                                                  │
                                                  ▼
+---------------------------------------------------------------------------------------------------+
| PHASE 2: Visual Embedding & HDBSCAN Density Clustering (Weeks 3–4)                                |
| - Integrate DINOv2-Small (INT8 ONNX) embedding session in C++ engine.                             |
| - Generate L2-normalized 384-dimensional feature vectors.                                         |
| - Implement C++ UMAP dimensionality reduction (384-d -> 15-d).                                    |
| - Implement C++ HDBSCAN clustering with automated Outlier (-1) tray generation.                   |
| - Exit Criteria: Automated grouping of 1,000 photos into preliminary clusters in <3 minutes.      |
+---------------------------------------------------------------------------------------------------+
                                                  │
                                                  ▼
+---------------------------------------------------------------------------------------------------+
| PHASE 3: Interactive Review UI & Active Learning Loop (Weeks 5–6)                                 |
| - Build 2D Light-Table Canvas view (hardware-accelerated WebGL/Canvas).                           |
| - Build Typology Tray Review deck with keyboard shortcuts (X = Eject, M = Move, N = New Type).     |
| - Implement Must-Not-Link constraint logic and Next-Best candidate re-routing (<100ms latency).   |
| - Exit Criteria: Specialist can review 100 items/minute with dynamic cluster centroid adaptation. |
+---------------------------------------------------------------------------------------------------+
                                                  │
                                                  ▼
+---------------------------------------------------------------------------------------------------+
| PHASE 4: Stratigraphic Cross-Checking & Publication Export (Weeks 7–8)                            |
| - Connect visual clusters to Harris Matrix DAG; flag stratigraphic/chronological contradictions.  |
| - Implement Publication Plate Generator (300 DPI PDF/TIFF with aligned scale bars).               |
| - Implement CIDOC CRM / CRMarchaeo JSON-LD export.                                                |
| - Exit Criteria: One-click export of print-ready plates and ISO-compliant semantic graphs.        |
+---------------------------------------------------------------------------------------------------+
```
