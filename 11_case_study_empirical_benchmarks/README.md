# Research Module 11: Case Study Empirical Verification & Benchmark Protocol

> **Component:** Empirical Validation, Ground Truth Datasets & Evaluation Protocol  
> **Target System:** ArchaeoPhD AI Scientific Verification & Test Suite  
> **Status:** Production Reference  

---

## 1. Case Study 1: The Sinauli Royal Burials (Geochemical Carbonate Offset)

### 1.1 Archaeological Context
* **Site:** Sinauli, Baghpat District, Uttar Pradesh, India (Ganga-Yamuna Interfluve).
* **Excavations:** Archaeological Survey of India (ASI) under Dr. Sanjay K. Manjul.
* **Significance:** Uncovered anthropomorphic wooden coffins, solid-disk-wheel copper-sheathed chariots, copper antennae swords, and ritual pottery from the Copper-Bronze Age transition.
* **Primary Reference:** Shalini Sharma, Anil K. Pokharia, Sanjay K. Manjul, et al., *"Radiocarbon Dating of the Anthropomorphic Coffin and Associated Artifacts from Sinauli, India"*, published in *Radiocarbon* (Cambridge University Press).

### 1.2 The Empirical Dilemma
* **Sample 1 (`SNLRC-3`):**
  - Context: Carbonized organic seed (*Hordeum vulgare*) from a burial pot adjacent to Coffin 1.
  - Lab ID: **D-AMS 032053**.
  - Uncalibrated Determination: **$3457 \pm 31$ yr BP**.
  - Calibrated Age: $\sim 1880$–$1690$ cal BCE (IntCal20).
  - Concordance: Agrees with short-lived charcoal determination `SNLRC-1` ($3486 \pm 36$ yr BP).
* **Sample 2 (`SNLRC-2`):**
  - Context: Calcareous mineral coating recovered from the coffin grave sediment.
  - Measurement: Systematically older by thousands of years ($\sim 5000+$ BP).
* **Engine Diagnostic Pipeline:**
  - Standard keyword systems flag this as a major site contradiction.
  - ArchaeoPhD AI evaluates `CRMsci: S10 Material Substantial`. Seed = annual terrestrial organism absorbing atmospheric $^{14}\text{C}$; Calcareous coating = secondary inorganic precipitation incorporating ancient geological carbonates dissolved in groundwater (hard-water effect).
  - **Result:** Classified as a **Geochemical Material Offset**, correctly preventing a false contradiction alarm.

---

## 2. Case Study 2: Wonderwerk Cave Stratum 4aLH (Bioturbation Outlier)

### 2.1 Archaeological Context
* **Site:** Wonderwerk Cave, Kuruman Hills, Northern Cape, South Africa. Key stratified sequence for the Middle to Later Stone Age transition.
* **Primary Reference:** Michael Chazan, Liora K. Horwitz, Christopher Bronk Ramsey, et al., *"Radiocarbon Dates Constrain the Timing of Environmental and Cultural Shifts in the Holocene Strata of Wonderwerk Cave, South Africa"*, published in *Radiocarbon*.

### 2.2 The Empirical Dilemma
* **Sample (`OxA-30638`):**
  - Context: Excavation 1, Stratum 4aLH (Lower Hearth feature at base of Stratum 4a).
  - Material: Single-entity charcoal with acid-base-acid (ABA) pretreatment.
  - Determination: $28,000 \pm 220$ yr BP.
  - Sequence Modeling: When integrated into the Bayesian stratigraphic model in OxCal, it fails the chi-squared compatibility threshold:
    $$A_i = 51.7\% < 60\% \quad (\text{drives } A_{\text{model}} \text{ down to } 11.4\%)$$
  - Micromorphological analysis confirms sediment disturbance by burrowing micro-mammals (`CRMarchaeo: AP8 disturbed`).
* **Engine Diagnostic Pipeline:**
  - The sample is flagged as a **Taphonomic Bioturbation Outlier**.
  - Auto-compiles OxCal script routing `OxA-30638` to `Outlier_Model("SSimple", N(0,2), 0, "s")`, yielding a **53% posterior outlier probability** and restoring sequence model convergence without corrupting the site stratigraphy.

---

## 3. The Seven Reproducible Evaluation Metrics

To satisfy the Trustworthy AI guidelines of MAIA WG3, ArchaeoPhD AI reports performance against an open, reproducible 7-metric protocol:

```
+---------------------------------------------------------------------------------------------------+
|                           THE 7-METRIC REPRODUCIBLE EVALUATION PROTOCOL                           |
+===================================================================================================+
| Metric                             | Mathematical Formula         | Target & Interpretation       |
+------------------------------------+------------------------------+-------------------------------+
| 1. Candidate Recall (R_cand)       | TP / (TP + FN_missed)        | >= 98% Recall of all entities |
| 2. Top-1 & Top-3 Selection Acc.    | (1/N) * Sum(Target in Top-k) | 51% Top-1, 75% Top-3 (AviArch)|
| 3. Strict Tuple-Binding F1         | 2 * P_tuple * R_tuple / (P+R)| Zero tolerance for misbinding |
| 4. Citation Deduplication Acc.     | Correct (S4 vs I7) / Total   | Eliminates citation echoes    |
| 5. Discourse-Stance Accuracy       | Correct Stance / Total       | Asserted/Hedged/Refuted/Quoted|
| 6. Contradiction False-Alarm Rate  | False Conflicts / Total Pairs| Gated by the 4 preconditions  |
| 7. Human Review Speedup            | (t_manual - t_assisted) / t  | >= 70% reduction in time/page |
+---------------------------------------------------------------------------------------------------+
```
