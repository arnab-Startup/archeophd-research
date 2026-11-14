# Non-Functional Requirements Specification

> **Subproject:** Visual Sorting & Typology Studio  
> **Section:** 01 — Domain & Requirements  
> **Status:** Production Reference  

---

## 1. Performance & Latency Budgets (NFR-PERF)

* **NFR-PERF-01 (Throughput on Standard Hardware):** The visual embedding pipeline must process a minimum of **20 images per second** on a standard quad-core consumer laptop CPU without requiring a discrete GPU.
* **NFR-PERF-02 (Batch Ingestion Benchmark):** Ingesting, segmenting, and clustering a standard field batch of **1,000 photos** must complete within **under 3 minutes** on CPU.
* **NFR-PERF-03 (Interactive Re-clustering Latency):** When a user rejects or moves an item during review, the centroid recalculation and next-best candidate recommendation must render within **< 100 milliseconds** to prevent UI stutter.
* **NFR-PERF-04 (Memory Footprint):** Peak active RAM usage during 5,000-image clustering must remain strictly **under 1.5 GB**, allowing seamless co-existence with the Win32 desktop application.

---

## 2. Offline Sovereignty & Security (NFR-SEC)

* **NFR-SEC-01 (Zero External Network Sockets):** In the Local Air-Gapped Workstation edition, the entire vision, embedding, and clustering pipeline must run 100% locally with zero internet socket connections or external API calls.
* **NFR-SEC-02 (Zero Telemetry):** No photo thumbnails, embeddings, or metadata may be transmitted to external servers or used for model fine-tuning.
* **NFR-SEC-03 (Encrypted Cache):** Local thumbnail caches and vector feature stores must be persisted inside the user's encrypted local data root (`%APPDATA%/ArchaeoPhD/DataRoot/`).

---

## 3. Usability & Ergonomics (NFR-UX)

* **NFR-UX-01 (Keyboard-First Review):** The review interface must be fully operable via keyboard shortcuts (`X` = Reject, `M` = Move, `N` = New Type, `Arrow Keys` = Navigate) to maximize sorting velocity.
* **NFR-UX-02 (Undo / Redo Durability):** Every rejection or cluster reassignment must support an infinite undo/redo stack (`Ctrl+Z` / `Ctrl+Y`) stored in local memory.
* **NFR-UX-03 (Responsive Canvas Rendering):** The 2D cluster scatter plot must utilize hardware-accelerated Canvas/WebGL to render up to 25,000 interactive thumbnail points at 60 FPS.

---

## 4. Reliability & Reproducibility (NFR-REL)

* **NFR-REL-01 (Deterministic Re-clustering):** Given the identical image set and random seed, the dimensionality reduction and clustering algorithms must produce strictly deterministic cluster boundaries.
* **NFR-REL-02 (Graceful Degradation):** Corrupt, unreadable, or zero-byte image files must be flagged in an error log without crashing the batch ingestion pipeline.
