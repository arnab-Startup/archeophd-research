# Light-Table Canvas View (Interactive Cluster Scatter Plot)

> **Subproject:** Visual Sorting & Typology Studio  
> **Section:** 04 — UI / UX Interaction Design  
> **Status:** Production Reference  

---

## 1. Concept: The 2D Landscape of an Excavation

The **Light-Table Canvas View** provides the global visual overview of the entire photographic corpus. Instead of browsing through thousands of disconnected file icons, the archaeologist sees an interactive 2D map:

```
+---------------------------------------------------------------------------------------------------+
|  [Canvas View: 5,000 Ingested Artifact Photos]                     [Filter: Stratum IV] [Zoom]    |
|                                                                                                   |
|         Cluster 1 (Red Slip Bowls)              Cluster 3 (Incised Storage Jars)                 |
|             (:::) (:::) (:::)                         (***) (***) (***)                           |
|           (:::) (:::) (:::) (:::)                   (***) (***) (***) (***)                       |
|             (:::) (:::) (:::)                         (***) (***) (***)                           |
|                                                                                                   |
|                                 [Outliers / Unique]                                               |
|                                    ( ? )   ( ! )                                                  |
|                                                                                                   |
|                    Cluster 2 (Chipped Flint Blades)                                               |
|                         (---) (---) (---)                                                         |
|                       (---) (---) (---) (---)                                                     |
|                                                                                                   |
|  [Status: 12 Clusters Discovered | 18 Outliers Isolated | 98.4% Segmented Cleanly]                |
+---------------------------------------------------------------------------------------------------+
```

---

## 2. Interaction Design & Controls

### 2.1 Smooth GPU-Accelerated Pan & Zoom
* Implemented via HTML5 Canvas with WebGL2 rendering.
* Handles up to **25,000 thumbnail points** at 60 FPS.
* As the user zooms in, points smoothly cross-fade into high-resolution cropped thumbnails.

### 2.2 Lasso Selection & Multi-Item Actions
* **Lasso Tool (`L`):** User can draw a freeform loop around a group of points.
* **Context Actions:**
  - *"Merge into Cluster..."*
  - *"Create New Type..."*
  - *"Tag as Stratigraphic Group..."*

### 2.3 Visual Filtering Overlays
* **Color by Stratigraphic Horizon:** Points change color according to their trench layer (e.g., Stratum II = Blue, Stratum III = Orange), allowing visual detection of typological evolution across time.
* **Highlight Chronological Anomalies:** Out-of-place artifacts (e.g., an Iron Age sherd found in an Early Bronze Age cluster) pulse in warning amber.
