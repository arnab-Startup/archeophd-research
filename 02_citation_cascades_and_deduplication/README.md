# Research Module 02: Citation Cascades & Bibliometric Deduplication

> **Component:** Epistemic Provenance & Citation De-duplication Engine  
> **Target System:** ArchaeoPhD AI v2.0 Literature Parsing & Consensus Scorer  
> **Status:** Production Reference  

---

## 1. The Bibliometric Echo-Chamber in Archaeological Literature

### 1.1 How Citation Cascades Distort Consensus
In historical, archaeological, and heritage sciences, primary empirical assays (such as radiocarbon dates or stratigraphic assignments) are expensive and rare. A single primary date published in an initial field report or preliminary monograph is frequently repeated across decades:
* Year 1 (1984): Primary excavator publishes an uncalibrated radiocarbon date $3200 \pm 45$ BP in a localized trench bulletin.
* Year 8 (1992): A regional ceramic survey cites the date as anchoring the local Middle Bronze Age.
* Year 15 (1999): A continental synthesis monograph incorporates the regional survey's timeline.
* Year 24 (2008): Three specialized doctoral dissertations cite the synthesis monograph.
* Year 35 (2019): Ten journal articles cite the dissertations and synthesis to support broader historical trade models.

### 1.2 The Naive Multi-Agent / NLP Failure
When generic search engines, vector similarity systems, or naive LLM extractors scan this corpus, they encounter 16 separate academic documents asserting that the site dates to the Middle Bronze Age:
* A naive counting heuristic concludes: **"16 independent sources corroborate this date — Consensus = High (95%+)"**.
* **Epistemic Reality:** There is only **one** empirical measurement ($n = 1$). The remaining 15 documents are secondary bibliographic echoes.
* If the original 1984 sample was contaminated by bitumen, affected by the old-wood effect, or calibrated with outdated curves, the 15 secondary citations provide **zero additional evidential weight**.

---

## 2. Formal Epistemic De-duplication Architecture via CRMinf v1.2.1

ArchaeoPhD AI v2.0 solves citation cascading by formalizing the epistemological distinction between **empirical observation** and **belief adoption**.

### 2.1 The Two Fundamental Epistemic Events
1. **Primary Empirical Recording:**
   $$\text{Excavator/Lab } (\text{E39 Actor}) \xrightarrow{\text{P14 carried out}} \text{CRMsci: S4 Single Observation / S21 Measurement}$$
   $$\text{yielding: } \text{CRMsci: O16 observed value} = 3200 \pm 45 \text{ BP} \quad (\mathbf{n = 1 \text{ independent empirical proof}})$$
2. **Secondary Belief Adoption (Bibliographic Citation):**
   $$\text{Secondary Author } (\text{E39 Actor}) \xrightarrow{\text{P14 carried out}} \text{CRMinf: I7 Belief Adoption}$$
   $$\text{resulting in: } \text{CRMinf: I12 Adopted Belief}$$
   $$\text{linked via: } \text{CRMinf: J7 is based on evidence from } \longrightarrow \text{Primary Publication } (\text{E73 Information Object})$$

```
+---------------------------------------------------------------------------------------------------+
|                                CITATION CASCADING DE-DUPLICATION                                  |
+===================================================================================================+
|                               PRIMARY EMPIRICAL ASSAY                                             |
|                      CRMsci: S4 Single Observation / S21 Measurement                              |
|                                       (Weight = 1.0)                                              |
+---------------------------------------------------------------------------------------------------+
                                         │
                                         ├─────────────────────────────────────────┐
                                         ▼                                         ▼
                     CRMinf: I5 Inference Making               CRMinf: I7 Belief Adoption (Citation)
                     (Original Primary Hypothesis)             (Secondary Scholar Cites Primary)
                                         │                                         │
                                         ▼                                         ▼
                                  CRMinf: I2 Belief                         CRMinf: I12 Adopted Belief
                                  (Weight = Anchored)                       (Weight = 0.0 Independent)
                                         │                                         │
                                         └───────────────────┬─────────────────────┘
                                                             ▼
                                                CRMinf: J7 is based on evidence from
                                                (Traverses back to primary S4/S21 anchor)
```

---

## 3. Consensus Scoring Algorithm

When calculating the **Axis 3: Scholarly Consensus ($C_{\text{schol}}$)** score for an archaeological proposition:
1. The engine constructs a directed graph of all literature citations claiming proposition $P$.
2. For each document $D_i$, the engine parses bibliographic references and citation phrases (e.g., *"following Smith 1984"*, *"as established by Sharma et al."*).
3. The graph is traversed backwards along the `J7 is based on evidence from` and `J13 adopted interpretation` edges until terminal empirical anchors (`CRMsci: S4` / `S21`) are reached.
4. **Independent Corroboration Condition:**
   $$\text{Corroboration Count } N_{\text{indep}} = |\text{Unique Primary } (S4 \cup S21) \text{ Observation Nodes}|$$
   If $N_{\text{indep}} = 1$, the claim is classified as **Single-Source Uncontested (Adopted)** regardless of whether it is cited by 1 or 1,000 papers.
   If $N_{\text{indep}} \ge 2$ with independent physical samples from distinct strata or laboratories, it is elevated to **Independently Corroborated**.
