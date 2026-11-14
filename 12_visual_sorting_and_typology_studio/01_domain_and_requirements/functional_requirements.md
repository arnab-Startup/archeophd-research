# Functional Requirements Specification

> **Subproject:** Visual Sorting & Typology Studio  
> **Section:** 01 — Domain & Requirements  
> **Status:** Production Reference  

---

## 1. Batch Image Ingestion & Pre-processing (FR-INGEST)

* **FR-INGEST-01 (Supported Formats):** The system must accept batch ingestion of image folders containing JPEG, PNG, WebP, and TIFF files.
* **FR-INGEST-02 (EXIF & Metadata Harvesting):** The system must automatically read and index embedded EXIF metadata (capture timestamp, camera model, lens parameters, and GPS coordinates if present).
* **FR-INGEST-03 (Locus / Context Binding):** The system must allow users to associate ingested image batches with specific Trench and Stratigraphic Unit (`A8`) identifiers via folder naming conventions or CSV manifest import.
* **FR-INGEST-04 (Scale-Bar Detection):** The engine must detect the presence of standardized photographic scale bars (centimeter scales, checkerboards) and record their pixel bounding coordinates without allowing scale colors to bias typological clustering.

---

## 2. Visual Embedding & Density Clustering (FR-CLUSTER)

* **FR-CLUSTER-01 (Artifact Segmentation):** The system must automatically segment the foreground artifact from background soil, trench textures, hands, and shadows using a pre-trained edge-aware segmentation model.
* **FR-CLUSTER-02 (Morphological & Fabric Embedding):** The system must generate dense feature representations capturing contour shape, rim profiles, surface texture, and decorative color patterns using self-supervised Vision Transformer (DINOv2) embeddings.
* **FR-CLUSTER-03 (Dynamic Density Clustering):** The system must group embeddings into organic clusters using density-based algorithms (HDBSCAN over UMAP projection) without requiring the user to guess or hardcode $K$.
* **FR-CLUSTER-04 (Outlier Isolation):** Unclassifiable, heavily fragmented, or completely unique items must be automatically assigned to an explicit "Outlier / Unique Finds" tray (Cluster -1) rather than forced into an ill-fitting category.

---

## 3. Human-in-the-Loop Review & Active Learning (FR-REVIEW)

* **FR-REVIEW-01 (Cluster Masonry Review):** The system must display cluster contents in a responsive, high-density masonry card grid allowing rapid visual scanning of up to 100 artifacts per screen.
* **FR-REVIEW-02 (Rapid Single-Key Rejection):** Users must be able to eject a misclassified item from a cluster via mouse click or single keypress (`X` or `Delete`).
* **FR-REVIEW-03 (Automated Next-Best Routing):** When an item is rejected, the system must compute the cosine distance to all remaining cluster centroids and propose the Top-2 best-fitting alternative trays.
* **FR-REVIEW-04 (Boundary Adaptation):** Ejections and confirmations must dynamically recalculate the cluster centroid and variance, refining subsequent batch classification accuracy.
* **FR-REVIEW-05 (User-Defined Typological Naming):** Users must be able to rename clusters from generic IDs (e.g., "Cluster 4") to formal typological designations (e.g., "Type 3A: Carinated Red-Burnished Bowls").

---

## 4. Stratigraphic Cross-Checking & Reporting (FR-ANALYZE)

* **FR-ANALYZE-01 (Chronological Matrix Cross-Check):** When an artifact is confirmed in a typological class, the system must cross-check its stratigraphic unit (`A8`) against the site Harris Matrix DAG.
* **FR-ANALYZE-02 (Anomaly Flagging):** If two identical typological artifacts appear in non-contiguous, stratigraphically separated phases, the system must raise a **Stratigraphic Anomaly Alert** indicating possible bioturbation or residual deposition.

---

## 5. Catalog & Plate Export (FR-EXPORT)

* **FR-EXPORT-01 (Publication Plate Layout):** The system must export selected clusters as print-ready photographic plates (300 DPI, white background, auto-aligned scale bars, standardized numbering).
* **FR-EXPORT-02 (Tabular Inventory):** One-click export to CSV, Excel, and SQLite containing catalog numbers, locus IDs, dimensions, typological assignments, and crop thumbnails.
* **FR-EXPORT-03 (CIDOC CRM JSON-LD):** Export full semantic graphs mapping artifacts to `CIDOC CRM: E22 Human-Made Object`, `E55 Type`, and `CRMarchaeo: A2 Stratigraphic Volume Unit`.
