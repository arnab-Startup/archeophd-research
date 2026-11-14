# Publication Plate Generator (High-Resolution Plate Export)

> **Subproject:** Visual Sorting & Typology Studio  
> **Section:** 04 — UI / UX Interaction Design  
> **Status:** Production Reference  

---

## 1. The Publication Bottleneck

Preparing photographic plates for excavation monographs and journal publications (*American Journal of Archaeology*, *Antiquity*, *Gallia*) currently requires weeks of tedious manual graphic work:
* Cropping artifacts in Photoshop.
* Pasting onto clean white canvases.
* Aligning scale bars so that 1 cm is uniform across all photos.
* Numbering each find (e.g., "1. Rim sherd from Locus 14; 2. Base from Locus 12").

---

## 2. Automated Plate Generation Workflow

The **Publication Plate Generator** automates this entire process with a single click:

```
[Validated Typology Tray: e.g., "Type 3: Incised Bowls"]
                         │
                         ▼
        [1. Normalize Scale & Resolution (300 DPI)]
        - Uses scale-bar pixel calibration ratio to normalize all artifacts
          to identical metric magnification (e.g., 1:1 or 1:2 scale)
                         │
                         ▼
        [2. Dynamic Masonry Grid Fitting]
        - Fits 12 to 24 artifacts onto standard page layout
          (A4, US Letter, Quarto 21x28 cm)
                         │
                         ▼
        [3. Standardized Typographic Labeling]
        - Adds non-obtrusive figure numbers (1, 2, 3...)
        - Renders uniform calibrated 5 cm / 1 cm metric scale bar in bottom corner
                         │
                         ▼
    [Export Options: Print-Ready PDF, Vector SVG, or 300 DPI TIFF]
    + Automated Caption Table (CSV & Word format)
```

---

## 3. Sample Plate Layout Output

```
+---------------------------------------------------------------------------------------------------+
|  PLATE XII: Middle Bronze Age Carinated Bowls (Trench B, Stratum IV)                             |
|                                                                                                   |
|     +-----------+         +-----------+         +-----------+         +-----------+               |
|     |           |         |           |         |           |         |           |               |
|     |  Photo 1  |         |  Photo 2  |         |  Photo 3  |         |  Photo 4  |               |
|     |           |         |           |         |           |         |           |               |
|     +-----------+         +-----------+         +-----------+         +-----------+               |
|          1.                    2.                    3.                    4.                     |
|                                                                                                   |
|     +-----------+         +-----------+         +-----------+         +-----------+               |
|     |           |         |           |         |           |         |           |               |
|     |  Photo 5  |         |  Photo 6  |         |  Photo 7  |         |  Photo 8  |               |
|     |           |         |           |         |           |         |           |               |
|     +-----------+         +-----------+         +-----------+         +-----------+               |
|          5.                    6.                    7.                    8.                     |
|                                                                                                   |
|                                                                       |=====| 5 cm                |
+---------------------------------------------------------------------------------------------------+
```

### Accompanying Caption Generator
Along with the graphic plate, the generator outputs a formatted caption table:
* *"Plate XII. Middle Bronze Age Carinated Bowls. 1. Inv. No. B-104 (Locus 14, Stratum IV); 2. Inv. No. B-112 (Locus 12, Stratum IV); 3. Inv. No. B-129 (Locus 18, Stratum IV)..."*
