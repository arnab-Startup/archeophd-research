# Research Module 08: Complete CIDOC CRM Ontological Specification

> **Component:** International Standard Ontological Data Model (ISO 21127)  
> **Target System:** ArchaeoPhD AI v2.0 JSON-LD Knowledge Graph  
> **Status:** Production Reference  

---

## 1. The 4-Tier Ontological Data Model

ArchaeoPhD AI v2.0 implements the complete 4-Tier Ontological Schema cross-verified with CIDOC CRM v7.1.3, CRMarchaeo v2.1, CRMsci v3.2, CRMdig v5.0, CRMinf v1.2.1, and the CIDOC CRM Periodic Table (Grillo 2026, *arXiv:2610.28650*):

```
+---------------------------------------------------------------------------------------------------+
| TIER 1: PHYSICAL MATERIAL REALITY (CIDOC CRM v7.1.3 & CRMarchaeo v2.1)                            |
+---------------------------------------------------------------------------------------------------+
| Classes:                                                                                          |
| - E18 Physical Thing: Persistent physical objects in the real world.                              |
| - A8 Stratigraphic Unit: Unified superclass representing any individual component of stratigraphy.|
| - A2 Stratigraphic Volume Unit: Anthropogenic deposits, fills, layers of soil, stone structures.   |
| - A3 Stratigraphic Interface: Surfaces of destruction, cuts of pits, foundation trench boundaries.|
| - S13 Sample: Material specimen physically removed from a stratigraphic unit for lab analysis.    |
| Properties:                                                                                       |
| - AP11 has physical relation to: Physical touching contact between two A8 units (IMMUTABLE).      |
| - AP12 confines: An A3 Interface forms the physical boundary of an A2 Volume.                     |
| - AP13 has stratigraphic relation to: Interpreted temporal ordering sequence (REVISABLE).        |
| - AP13.2 justified by: Formal citation of the law or reasoning justifying the AP13 relation.      |
| - AP21 contains: An A2 Volume contains physical artifacts or ecofacts.                            |
| - AP28 occurs before: Temporal sequence ordering between stratigraphic events.                    |
+---------------------------------------------------------------------------------------------------+

+---------------------------------------------------------------------------------------------------+
| TIER 2: FIELD OBSERVATION & LAB MEASUREMENT (CRMsci v3.2 & CRMarchaeo v2.1)                       |
+---------------------------------------------------------------------------------------------------+
| Classes:                                                                                          |
| - A9 Archaeological Excavation: The physical act of stratigraphic digging.                         |
| - S2 Sample Taking: The physical extraction event of an S13 Sample.                               |
| - S4 Single Observation: Qualitative field recording of a physical property.                      |
| - S21 Measurement: Quantitative scientific measurement (e.g., AMS, OSL, XRF).                     |
| - S10 Material Substantial: Compositional classification (charcoal, calcite, bone collagen).      |
| Properties:                                                                                       |
| - O3 sampled from: Links S2 Sample Taking to an A2 Stratigraphic Volume Unit.                     |
| - O8 observed: Links S4 Observation to an observable physical entity.                             |
| - O16 observed value: Links S4/S21 to an empirical recorded value or measurement range.           |
| - O24 measured: Links S21 Measurement to the S13 Sample being analyzed.                           |
+---------------------------------------------------------------------------------------------------+

+---------------------------------------------------------------------------------------------------+
| TIER 3: DIGITAL DOCUMENT & AI PIPELINE PROVENANCE (CRMdig v5.0)                                    |
+---------------------------------------------------------------------------------------------------+
| Classes:                                                                                          |
| - D1 Digital Object: Source excavation report PDF or image scan.                                  |
| - D7 Digital Machine Event: Hardware execution on CPU/GPU.                                        |
| - D10 Software Execution: Algorithmic run of OCR, table layout parser, or LLM extractor.          |
| - D14 Software: Specific software build, commit hash, and neural model weight version.            |
| - D29 Annotation Object: Bounding-box coordinates and extracted text tuple.                       |
| Properties:                                                                                       |
| - L10 had input: The raw document or image provided to the algorithm.                            |
| - L11 had output: The extracted JSON-LD candidate tuple produced.                                 |
| - L23 used software: Links execution event to the exact model version.                           |
| - L48 created annotation: Links D10 Software Execution to D29 Annotation Object.                 |
+---------------------------------------------------------------------------------------------------+

+---------------------------------------------------------------------------------------------------+
| TIER 4: SCHOLARLY ARGUMENTATION & BELIEF REASONING (CRMinf v1.2.1)                                |
+---------------------------------------------------------------------------------------------------+
| Classes:                                                                                          |
| - I1 Argumentation: The discursive reasoning process linking evidence to conclusions.             |
| - I2 Belief: The epistemic state of belief held by an E39 Actor.                                  |
| - I4 Proposition Set: A coherent set of archaeological claims.                                    |
| - I5 Inference Making: The cognitive or computational act of inferring a conclusion.              |
| - I6 Belief Value: Qualitative degree of belief (Asserted, Hedged, Refuted, Possible).            |
| - I7 Belief Adoption: Secondary citation of another scholar's prior conclusion.                   |
| - I12 Adopted Belief: Epistemic belief state resulting from citation adoption.                    |
| - I15 Provenance Assessment: Critical evaluation of a source document's reliability.              |
| - I16 Meaning Comprehension: Linguistic extraction of propositions without endorsing truth.       |
| - I17 One-Proposition Set: Atomic proposition (e.g., "Stratum IV dates to Late Bronze Age").      |
| Properties:                                                                                       |
| - J1 used as premise: Empirical evidence nodes used as premises for an inference.                 |
| - J2 concluded that: The proposition concluded from an I5 Inference Making event.                 |
| - J3 applied: The methodological rule or calibration curve applied.                               |
| - J4 that: Links I2 Belief state to the proposition being evaluated.                              |
| - J5 holds to be: Links I2 Belief to its I6 Belief Value.                                         |
| - J7 is based on evidence from: Traces citation adoption back to primary empirical proof.         |
+---------------------------------------------------------------------------------------------------+
```

---

## 2. Proof of Stratigraphic Revisability (AP11 vs. AP13)

In classical stratigraphy, an excavator observes that Layer B lies directly upon Layer C:
* **The Invariant Observation:**
  $$\text{Layer B } (\text{A8}) \xrightarrow{\text{AP11 has physical relation to}} \text{Layer C } (\text{A8})$$
  This physical touching contact is an unalterable empirical fact.
* **The Reversible Temporal Interpretation:**
  $$\text{Layer B } (\text{A8}) \xrightarrow{\text{AP13 has stratigraphic relation to}} \text{Layer C } (\text{A8})$$
  $$\text{with: } \text{AP13.2 justified by } \longrightarrow \text{Law of Superposition } (\text{CRMinf: I5 Inference Making})$$
* **The Post-Depositional Reversal:**
  If micromorphology reveals micro-mammal burrows connecting the two layers (`CRMarchaeo: AP8 disturbed`), the temporal sequence is inverted without corrupting the original physical recording:
  $$\text{Layer B } (\text{A8}) \xrightarrow{\text{AP28 occurs before}} \text{Layer C } (\text{A8}) \quad \text{[REVERSED]}$$
  The original physical contact (`AP11`) remains intact, and the revision is logged via `CRMinf: I15 Provenance Assessment`.

---

## 3. The 3-Axis Epistemological Vector

The flat "Verified/Contested/Speculative" tags are replaced by $\mathbf{V}_{\text{epistemic}} = \langle F_{\text{ext}},\, G_{\text{evid}},\, C_{\text{schol}} \rangle$:

1. **Axis 1: Extraction & Attribution Fidelity ($F_{\text{ext}}$):**
   - Level 4: `Human-Verified Span`
   - Level 3: `Exact Deterministic Match`
   - Level 2: `Ambiguous Table/OCR Parse`
   - Level 1: `Quoted Third-Party View`
2. **Axis 2: Evidential Grounding Quality ($G_{\text{evid}}$):**
   - Level 4: `Direct Radiometric/Archaeometric Measurement`
   - Level 3: `Stratigraphic/Typological Correlation`
   - Level 2: `Secondary Documentary Reference`
   - Level 1: `Speculative Unaccompanied Assertion`
3. **Axis 3: Scholarly Consensus ($C_{\text{schol}}$):**
   - Level 5: `Independently Corroborated` (multiple independent $S4/S21$ nodes)
   - Level 4: `Single-Source Uncontested`
   - Level 3: `Compatible Competing Interpretations`
   - Level 2: `Directly Refuted / Contested`
   - Level 1: `Superseded / Revised`
