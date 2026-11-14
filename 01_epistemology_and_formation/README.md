# Research Module 01: Archaeological Epistemology & Formation Process Theory

> **Component:** Epistemological Foundation & Stratigraphic Reality  
> **Target System:** ArchaeoPhD AI v2.0 Ingestion & Ontology Layer  
> **Status:** Production Reference  

---

## 1. The Destructive Nature of Excavation & The Surrogate Record

### 1.1 The Epistemological Paradox
In natural sciences (chemistry, physics), empirical hypotheses are tested through repeatable experiments. In archaeology, stratigraphic excavation is fundamentally and irreversibly **destructive**:
* The primary physical deposit (soil, ash, architectural collapse) must be physically removed with spades, trowels, and brushes to expose and document the underlying strata.
* Once a stratum is excavated, its physical configuration is permanently erased. It cannot be reconstructed in the ground or excavated again by another researcher.

### 1.2 The Excavation Archive as a Surrogate (Edward C. Harris)
As Edward C. Harris formulated in *Principles of Archaeological Stratigraphy* (1979, 1989):
* Because the physical site is consumed by the act of excavation, **the excavation archive becomes the only surviving empirical surrogate of the site**.
* The archive (consisting of written locus sheets, section drawings, single-surface plans, photographs, total station coordinates, and Harris matrices) is not the site itself; it is an information model constructed by human observers.

### 1.3 Observer-Dependency (Martin Carver)
Martin Carver (*Field Archaeology*, *Making Alternative Histories*) demonstrated that the creation of the stratigraphic record is inherently observer-dependent:
* Distinguishing between two subtle stratigraphic units depends on soil moisture, ambient lighting in the trench, excavator skill, and perceptual biases.
* What an archaeologist records on a trench recording form represents an interpretation of physical boundaries.

### 1.4 The ArchaeoPhD AI v1.0 Architectural Error
In ArchaeoPhD AI v1.0, the lowest tier was labeled **"Layer A: Physical World Ground Truth"**. This was a category error:
* ArchaeoPhD AI does not ingest soil or physical artifacts; it ingests **published literature** (PDF excavation reports, articles, monographs).
* In CIDOC CRM terms, a publication is an `E73 Information Object` created by an `E39 Actor` (the author/excavator). Conflating an `E73 Information Object` with an `A8 Stratigraphic Unit` / `E18 Physical Thing` ignores the interpretive translation between the trench and the published page.

---

## 2. Formation Process Theory: Systemic Context vs. Archaeological Context (Michael B. Schiffer)

### 2.1 The Two Contexts
Michael B. Schiffer (1972, 1976, 1987) established the foundational framework for archaeological site formation:
1. **Systemic Context:** The dynamic condition of an artifact or material while it is participating in an ongoing human behavioral system. The artifact undergoes a life history:
   $$\text{Procurement} \longrightarrow \text{Manufacture} \longrightarrow \text{Use} \longrightarrow \text{Maintenance} \longrightarrow \text{Recycling} \longrightarrow \text{Discard/Deposition}$$
2. **Archaeological Context:** The static condition of material remains after they have exited the systemic context and are buried in the earth, subject to post-depositional natural and cultural transformations.

### 2.2 Cultural Transforms (C-Transforms)
Human behaviors that alter, transfer, or redeposit artifacts:
* **Primary Refuse:** Discarded at the immediate location of use (e.g., flint debitage around an anvil stone).
* **Secondary Refuse:** Swept up and dumped elsewhere (e.g., communal midden pits, street sweeps).
* **De Facto Refuse:** Usable objects left behind when a site is rapidly abandoned (e.g., Pompeii, sudden conflagration).
* **Reclamation / Plowing / Looting:** Subsequent populations digging into older layers to reuse building stones, loot burial goods, or till agricultural fields.

### 2.3 Non-Cultural / Natural Transforms (N-Transforms)
Environmental processes that alter the physical matrix and spatial positioning of finds:
* **Bioturbation:** Animal activity (burrowing rodents, termites, worms, ants) moving smaller finds (beads, small charcoals) vertically up or down through the stratigraphic column.
* **Floriturbation:** Tree roots penetrating strata, dislodging stones, and introducing modern organic carbon into ancient horizons.
* **Cryoturbation & Argilliturbation:** Freeze-thaw cycles and expanding/contracting smectite clays sorting artifacts by size.
* **Geochemical Leaching:** Groundwater movement dissolving bone collagen and precipitating secondary hard-water carbonates.

---

## 3. Epistemological Requirements for ArchaeoPhD AI v2.0

1. **Decouple Material Reality from Documentary Assertion:** An extraction from an excavation report must never be recorded as an immutable ground-truth fact about the soil. It is recorded as:
   $$\text{Author } (\text{E39}) \xrightarrow{\text{CRMinf: J5 holds to be}} \text{Proposition } (\text{I17}) \xrightarrow{\text{P67 refers to}} \text{Stratigraphic Unit } (\text{A8})$$
2. **Support Non-Destructive Scientific Reinterpretation:** If subsequent chemical assays, micromorphology, or Bayesian re-calibrations challenge an author's interpretation, the system records the revision via `CRMinf: I5 Inference Making`, maintaining full provenance of both the original field observation and the revision.
