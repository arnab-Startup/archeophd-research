# Research Module 04: Scientific NLP & The Five Extraction Failure Modes

> **Component:** Document Intelligence & Visual-Language Extraction Pipeline  
> **Target System:** ArchaeoPhD AI v2.0 Extraction Engine (`engine/extraction/`)  
> **Status:** Production Reference  

---

## 1. Overview

Extracting quantitative and stratigraphic data from archaeological literature presents extreme challenges that break off-the-shelf LLMs and standard OCR pipelines. Academic excavation literature is characterized by:
- Scanned 300–600 DPI bitmap monographs with complex typography and yellowed paper.
- Dense multi-column layouts, interleaved footnote citations, and oversized foldout tables.
- Evidence fragmented across prose, appendices, and section drawings.

ArchaeoPhD AI audits the **Five Canonical Failure Modes** of scientific document parsing and implements formal architectural mitigations.

---

## 2. The Five Failure Modes & Mitigations

### 2.1 Failure Mode 1: OCR & Table Serialization Errors
* **The Vulnerability:** Standard OCR engines (Tesseract, legacy Abbyy) process scanned PDF pages sequentially. When encountering multi-column text or non-bordered tables, reading orders become scrambled. Degraded numerals are frequently misread (e.g., mistaking `3` for `8`, converting `$3457 \pm 31$` into `$8457 \pm 31$`).
* **ArchaeoPhD AI v2.0 Mitigation:**
  1. High-resolution vision-language layout analysis identifies tabular bounding boxes.
  2. Bounding-box pixel crops are stored permanently in `CRMdig: D29 Annotation Object`.
  3. Every extracted date retains a deep link to its exact raster crop in the desktop UI, enabling instant 1-click human verification.

### 2.2 Failure Mode 2: Incomplete Candidate Pool
* **The Vulnerability:** Deterministic regex pipelines capture standard ISO formats (`3450 +/- 30 BP`), but fail completely on qualitative, prose-based, or multilingual chronological descriptions:
  - French: *"daté de la fin du Bronze moyen"*
  - German: *"in die Spätbronzezeit einzuordnen"*
  - Italian: *"riferibile alla facies protoappenninica"*
* **ArchaeoPhD AI v2.0 Mitigation:**
  - Enforce Top-$k$ Candidate Generation ($k \ge 3$) with recall benchmark target $R_{\text{cand}} \ge 98\%$.
  - Provide an interactive UI allowing archaeologists to highlight missed text spans with a single click.

### 2.3 Failure Mode 3: Entity-Attribute Mis-Association
* **The Vulnerability:** Archaeological monographs frequently report multiple dates, lab identifiers, and strata within a single paragraph. LLMs suffer from "syntactic drifting," mistakenly binding the radiocarbon age of Sample A to the stratum of Sample B.
* **ArchaeoPhD AI v2.0 Mitigation:**
  - Enforce strict 6-tuple dependency parsing:
    $$\mathcal{T} = \langle \text{Sample\_ID},\; \text{Lab\_Code},\; \text{Age},\; \text{Error},\; \text{Material},\; \text{Stratigraphic\_Unit} \rangle$$
  - Evaluated on **Strict Tuple-Binding $F_1$ ($F_{1,\text{bind}}$)**: an extraction is scored as zero if any single attribute is mis-associated.

### 2.4 Failure Mode 4: Negation, Hedging & Discourse-Stance Misattribution
* **The Vulnerability:** Authors regularly cite hypotheses specifically to refute or hedge them. For example:
  > *"Contrary to Sharma (2018), Stratum IV cannot be attributed to the Painted Grey Ware horizon."*
  Naive keyword matching extracts "Stratum IV = PGW" as an affirmative claim made by the author.
* **ArchaeoPhD AI v2.0 Mitigation:**
  - 4-way discourse-stance classification (benchmarked against SciFact and BioScope datasets):
    1. `Asserted`: Author makes an affirmative claim.
    2. `Hedged`: Author introduces an uncertain hypothesis (*"may possibly indicate"*).
    3. `Refuted`: Author explicitly rejects a prior claim.
    4. `Quoted_Third_Party`: Author cites another scholar's position without endorsing it.
  - Mapped directly to **`CRMinf: I6 Belief Value`** and **`I16 Meaning Comprehension`**.

### 2.5 Failure Mode 5: Cross-Modal Argument Reconstruction
* **The Vulnerability:** In scientific reporting, evidence is rarely contained in one contiguous paragraph:
  - Stratigraphic context is described on page 14.
  - Section drawing is shown in Figure 4 on page 22.
  - Pretreatment chemistry is listed in Table S2 on page 65.
* **ArchaeoPhD AI v2.0 Mitigation:**
  - Build a multi-anchor knowledge hypergraph connecting distributed annotations into a single **`CRMinf: I4 Proposition Set`** / **`I5 Inference Making`** node.
