# Stratigraphic Cross-Checking & Anomaly Detection

> **Subproject:** Visual Sorting & Typology Studio  
> **Section:** 05 — Archaeological Integration & Moat  
> **Status:** Production Reference  

---

## 1. Beyond Generic Photo Sorting: The Stratigraphic Moat

Generic computer vision tools (e.g., Google Photos, Roboflow) can group similar images, but they have zero understanding of archaeological time, space, or stratigraphy.

The **core competitive moat** of ArchaeoPhD AI is the tight coupling between the **Visual Typology Studio** and the **Stratigraphic DAG Engine (`engine/analysis/harris_matrix.hpp`)**:
* When an artifact photo is ingested, it carries a mandatory link to its provenience: `Trench_ID` and `Stratigraphic_Unit_ID` (`CRMarchaeo: A8`).
* As visual clusters are formed, the engine cross-references the stratigraphic distribution of each cluster across the site's Harris Matrix.

---

## 2. Detecting Chronological & Stratigraphic Contradictions

```
        VISUAL CLUSTER 3: "Early Bronze Age Painted Jars"
                     ├── Artifact A: Locus 12 (Stratum IV — EBA)  [NORMAL]
                     ├── Artifact B: Locus 14 (Stratum IV — EBA)  [NORMAL]
                     └── Artifact C: Locus 32 (Stratum I  — Iron Age) [ANOMALY!]
                                       │
                                       ▼
                 [Stratigraphic DAG Conflict Gating]
                 - Stratum I is separated from Stratum IV by 600 years.
                 - Artifact C has identical fabric and rim curvature to A & B.
                                       │
                                       ▼
                 [AUTOMATED STRATIGRAPHIC ALERT]
                 "Possible Residual Find or Unidentified Intrusive Pit:
                  Artifact C (Locus 32) is identical to EBA forms in Stratum IV."
```

### 2.1 The Two Archaeological Explanations
When an anomaly is flagged, the engine assists the specialist in determining the historical/taphonomic cause:
1. **Residual Artifact (Curated / Dug Up):** Earthworks or foundation trenches in the Iron Age cut into an Early Bronze Age deposit, redepositing an old sherd into a younger layer.
2. **Intrusive Pit (Infiltration):** A narrow unobserved intrusive pit dug in a later period penetrated down, dropping younger material into an older stratum.
3. **Typological Longevity:** The vessel form persisted across centuries longer than previously assumed in literature, prompting a scientific reassessment.
