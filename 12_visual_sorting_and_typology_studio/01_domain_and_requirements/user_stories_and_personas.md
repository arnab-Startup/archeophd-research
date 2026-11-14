# User Stories & Personas

> **Subproject:** Visual Sorting & Typology Studio  
> **Section:** 01 — Domain & Requirements  
> **Status:** Production Reference  

---

## 1. Key User Personas

### Persona A: Dr. Elena Rostova — Senior Ceramic Specialist
* **Role:** Analyzes 15,000 pottery sherds per season for an international Mediterranean Bronze Age expedition.
* **Pain Point:** Spends 4 weeks every summer in a humid field house manually grouping sherds into diagnostic trays before drawing and cataloging them.
* **Goal:** Wants an automated visual clusterer that groups her sherd photos by rim curvature, slip color, and surface decoration, so she can review entire classes of 50 vessels at once.
* **Key Requirement:** Must have 100% human authority. If the AI suggests a group she disagrees with, she must be able to reject it instantly without arguing with the model.

### Persona B: Marcus Vance — PhD Candidate in Lithic Technology
* **Role:** Analyzing 8,000 chipped stone tools across a Paleolithic rock shelter sequence.
* **Pain Point:** Needs to identify specific retouch styles and flake reduction stages across 12 stratigraphic layers.
* **Goal:** Wants to spot rare tool types (e.g., burins, bifacial points) that are currently buried in thousands of non-diagnostic debitage photos.
* **Key Requirement:** The software must run 100% offline on his field laptop in remote mountainous locations with zero internet.

### Persona C: Jean-Luc Moreau — Preventive Archaeology Project Director (INRAP)
* **Role:** Directs large commercial developer-funded rescue excavations in France.
* **Pain Point:** Contract deadlines mandate rapid land release. If find cataloging delays the final synthesis report, his firm faces severe developer penalties.
* **Goal:** Needs to produce standardized, publication-grade photographic plates and validated artifact inventories in hours, not months.

---

## 2. Core User Stories

| ID | As a... | I want to... | So that... |
|---|---|---|---|
| **US-01** | Specialist | Drag-and-drop a folder of 5,000 unorganized artifact photos | The system automatically segments out the background and clusters them into preliminary visual categories. |
| **US-02** | Specialist | Inspect a suggested visual cluster on a light-table masonry grid | I can scan 50 similar items at a glance and spot any misfits within seconds. |
| **US-03** | Specialist | Mark a misclassified image with a single keypress (`X`) | The system removes it from the group, adapts the group's boundary, and moves the item to its next best candidate tray. |
| **US-04** | Specialist | Lasso-select multiple items and create a "New Typology Tray" | I can formalize a newly discovered rare ware or import style immediately. |
| **US-05** | Director | Cross-check visual groups against stratigraphic locus forms | The engine alerts me if two identical pottery types are recorded in stratigraphically incompatible horizons. |
| **US-06** | Author | Click "Export Publication Plates" | I receive high-resolution, print-ready PDF/TIFF plates with uniform white backgrounds, aligned scale bars, and figure numbers. |
| **US-07** | Researcher | Export the validated catalog to CIDOC CRM JSON-LD | My typological classifications become machine-actionable FAIR data linked to our institutional repository. |
