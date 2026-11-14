# Problem Statement: The Post-Excavation Visual Triage Bottleneck

> **Subproject:** Visual Sorting & Typology Studio  
> **Section:** 01 — Domain & Requirements  
> **Target Audience:** Product Engineers, Domain Archaeologists, Grant Evaluators  
> **Status:** Production Reference  

---

## 1. The Context: From Trench Spoil to Museum Trays

At the conclusion of a standard 6-week archaeological excavation campaign, an expedition team typically brings back:
* **5,000 to 25,000 digital photographs** of material finds.
* Finds range across diagnostic ceramic sherds (rims, bases, handles), non-diagnostic body sherds, chipped stone lithics (cores, blades, flakes), small metal objects, glass beads, and faunal/botanical remains.
* Each find is tied to an archaeological context form (Trench, Locus, Stratigraphic Unit).

---

## 2. The Current Manual Workflow & Bottlenecks

### 2.1 The "Cardboard Tray" Ritual
Currently, field specialists (e.g., ceramicists, lithic analysts) must manually triage these items:
1. Photos are transferred from SD cards into generic nested Windows Explorer folders (e.g., `Trench_A/Locus_14/Photos/`).
2. The specialist opens photo viewers or Adobe Lightroom, inspecting each image individually.
3. Finds are manually sorted into typological bins (e.g., "Red Slip Bowl Rims", "Grey Ware Storage Jars", "Flint Bladelets").
4. Metadata is transcribed by hand into spreadsheet rows (photo filename, object type, dimensions, fabric).

### 2.2 Critical Pain Points
* **Extreme Time Sink:** A collection of 10,000 finds requires **150 to 300 hours of purely mechanical sorting** before scientific analysis can even begin.
* **Cognitive Fatigue & High Error Rates:** After reviewing 2,000 similar reddish-brown pottery fragments on a screen, visual attention decays sharply. Rare imports, intrusive modern sherds, or fine painted motifs are easily misclassified.
* **Lack of Cross-Trench Linking:** It is almost impossible for human memory to spot that a sherd in Trench A (Day 4) physically matches or stylistically duplicates a sherd from Trench G (Day 28).
* **Publication Formatting Lag:** Creating publication plates (arranging 12–20 sherd photos per page with uniform white backgrounds, scale bars aligned, and figure labels) takes additional weeks of tedious Adobe Photoshop work.

---

## 3. The Objective of the Visual Typology Studio

To transform this painful, weeks-long mechanical chore into an **intuitive, 2-to-3 hour interactive session**:
* The engine isolates the artifact and automatically clusters visually similar items into preliminary typological trays.
* The specialist acts as the editor and supervisor: reviewing trays at high speed, ejecting misfits with a single keypress, and watching the system dynamically update its classification in real time.
* Once verified, one click exports both formal publication plates and ISO-compliant CIDOC CRM knowledge graphs.
