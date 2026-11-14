# Research Module 03: The Four Contradiction Preconditions & Taphonomic Diagnostics

> **Component:** Contradiction Analysis & Diagnostic Gating Engine  
> **Target System:** ArchaeoPhD AI v2.0 Contradiction Engine (`engine/analysis/`)  
> **Status:** Production Reference  

---

## 1. Overview & Architectural Motivation

In generic NLP systems, two textual statements asserting different numerical values or periodizations for the same named entity are flagged as a contradiction. In archaeological science, this naive approach produces a crippling **False-Alarm Rate (FAR > 60%)**.

Archaeological data is shaped by human behavioral lifecycles (Schiffer's systemic context), depositional physics, taphonomic mixing (bioturbation), and disparate measurement frameworks. ArchaeoPhD AI v2.0 establishes **Four Gating Preconditions** that must be evaluated and passed before any divergence is classified as an empirical contradiction.

---

## 2. The Four Preconditions

### 2.1 Precondition 1: Entity & Event Coreference (Artifact Lifecycle Gating)
* **The Lifecycle Model:** An archaeological entity passes through multiple events separated in time:
  - $E_1 = \text{Procurement / Raw Material Formation}$ (e.g., tree ring growth in 1400 BCE).
  - $E_2 = \text{Manufacture / Production}$ (e.g., wooden beam carved in 1350 BCE; coin struck in 112 CE).
  - $E_3 = \text{Primary Use}$ (e.g., palace roof in use from 1350 to 1200 BCE).
  - $E_4 = \text{Destruction / Secondary Deposition}$ (e.g., palace burned and beam deposited in destruction layer in 1180 BCE).
* **The Terminus Post Quem (TPQ) Invariant:**
  $$\text{Age}(E_{\text{production}}) \le \text{Age}(E_{\text{deposition}})$$
* **Diagnostic Rule:**
  - If Author A dates a bronze sword to **1250 BCE** based on typological manufacture, and Author B dates the stratum in which the sword was found to **1100 BCE**, this is **not** a contradiction.
  - The sword is a curated heir-loom or durable find providing a *terminus post quem* for the stratum.
  - The engine flags a contradiction **only** if the deposition event is claimed to predate the production event ($E_{\text{deposition}} < E_{\text{production}}$), which violates physical causality.

### 2.2 Precondition 2: Sample Nature & Taphonomic Context
Apparent age discrepancies from the same archaeological feature must be diagnosed against sample composition and depositional disturbances before declaring author disagreement:
1. **Geochemical Carbonate Offset (The Sinauli Scenario):**
   - Two samples from Royal Burial Grave 1 at Sinauli:
     - Sample `SNLRC-3`: Carbonized seed (*Hordeum vulgare*) $\to$ **$3457 \pm 31$ yr BP** ($\sim 1880$–$1690$ cal BCE).
     - Sample `SNLRC-2`: Calcareous sediment coating $\to$ Apparent age $\sim 5000+$ BP.
   - *Diagnostic Rule:* Check `CRMsci: S10 Material Substantial`. Seed = short-lived seasonal organism absorbing atmospheric $^{14}\text{C}$; Calcareous coating = inorganic precipitation incorporating dissolved ancient carbonate minerals from groundwater (hard-water effect).
   - *Resolution:* Classified as a **Geochemical Offset**, not an empirical contradiction.
2. **Bioturbation & Sediment Mixing (The Wonderwerk Cave Scenario):**
   - Charcoal sample `OxA-30638` recovered from Stratum 4aLH (Lower Hearth) yields $28,000 \pm 220$ yr BP.
   - When modeled in OxCal with adjacent dates, its Individual Agreement Index drops to **$A_i = 51.7\% < 60\%$**, driving the overall model down to $A_{\text{model}} = 11.4\%$.
   - *Diagnostic Rule:* Check micromorphology records for sediment mixing (`CRMarchaeo: AP8 disturbed`). Small burrowing mammals (rodents) moved an older charcoal piece down into a younger hearth.
   - *Resolution:* Classified as a **Taphonomic Outlier Candidate** routed to Bayesian down-weighting (`Outlier_Model`), not an author contradiction.

### 2.3 Precondition 3: Scale & Framework Normalization
Disparate publications express chronology in fundamentally different mathematical and cultural scales:
1. **Uncalibrated vs. Calibrated Scales:**
   - $^{14}\text{C}$ yr BP (uncalibrated radiocarbon years before 1950, based on Libby half-life of 5568 years).
   - cal BP (calibrated calendar years before 1950, based on tree-ring calibration curves).
   - cal BCE / cal CE (calendar years Before Common Era / Common Era).
   - Conversion: $\text{cal BP} = 1950 - \text{BCE/CE}$ (with astronomical 0-year handling).
2. **Typo-Chronological Periods:**
   - Author A: *"Late Bronze Age II"*.
   - Author B: *"13th Century BCE"*.
   - *Diagnostic Rule:* Typological terms must be resolved through a regional gazetteer mapping cultural periods to calibrated calendar intervals prior to computing interval overlap.

### 2.4 Precondition 4: Compatible Competing Hypotheses
In archaeological interpretation, multiple functional explanations can account for the identical physical stratum without logical incompatibility:
* **The Ash Layer Scenario:**
  - Author A interprets a site-wide ash destruction stratum as an **earthquake followed by accidental urban fire**.
  - Author B interprets the same stratum as evidence of **military conquest and warfare**.
* **Diagnostic Rule:** Both authors agree on the physical stratigraphy (ash layer `A8` overlying floor `A8`, linked via `AP11 has physical relation to`). The interpretations diverge in the inferred historical agency (`CRMinf: I5 Inference Making`).
* **Resolution:** Both hypotheses are structurally compatible with the physical matrix. The system records them as **Competing Compatible Beliefs** held by distinct scholars (`E39 Actor`), preventing false contradiction alarms.
