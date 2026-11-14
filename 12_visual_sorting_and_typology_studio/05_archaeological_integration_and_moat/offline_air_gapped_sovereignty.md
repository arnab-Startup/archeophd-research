# Offline Air-Gapped Execution & Data Sovereignty

> **Subproject:** Visual Sorting & Typology Studio  
> **Section:** 05 — Archaeological Integration & Moat  
> **Status:** Production Reference  

---

## 1. Ethical & Legal Safeguards in Archaeological Vision

Archaeological field photography is deeply sensitive. Uploading unexcavated field photos to generic cloud vision APIs violates core ethical principles and international antiquities laws:

### 1.1 Looting Prevention
* Field photos of gold jewelry, complete bronze vessels, or unexcavated funerary chambers carry high black-market value.
* If images or their embedded GPS coordinates leak, illicit treasure hunters and looters can target the trench coordinates before the excavation season concludes.

### 1.2 The CARE Principles & Indigenous Sovereignty
* Indigenous communities maintain inherent rights over images and analyses of ancestral sacred items and burial furniture (**CARE Principles**; Carroll et al. 2020).
* Under **NAGPRA** (25 U.S.C. 3001), digital imaging of funerary remains requires strict, audited access controls that public cloud platforms cannot guarantee.

---

## 2. Technical Implementation of the Offline Invariant

The Visual Typology Studio operates under strict air-gapped invariants in the desktop workstation:

1. **Local Neural Inference:**
   - Visual segmentation (U2-Net / MobileSAM) and embedding generation (DINOv2) run entirely inside the local C++ process via ONNX Runtime CPU.
   - Zero outbound TCP/HTTP socket connections.
2. **Encrypted Local Storage:**
   - Artifact vectors and thumbnail crops are saved to an encrypted local SQLite/DuckDB database located within the user's local profile (`%APPDATA%/ArchaeoPhD/DataRoot/`).
3. **No Central Model Training:**
   - User rejections and typological adjustments update only the *local* in-memory distance matrix for that specific session. No user images are ever scraped, collected, or transmitted for central AI fine-tuning.
