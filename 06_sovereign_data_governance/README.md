# Research Module 06: Sovereign Data Governance & Dual-Edition Architecture

> **Component:** Data Sovereignty, Ethics & Deployment Topologies  
> **Target System:** ArchaeoPhD AI Local Air-Gapped Workstation & Enterprise VPC  
> **Status:** Production Reference  

---

## 1. Archaeological Data Sovereignty & Ethical Mandates

Archaeological research data is subject to strict legal, ethical, and safety constraints that make generic public SaaS architectures non-compliant:

### 1.1 Looting Prevention & Geospatial Embargoes
* Excavation reports and field databases contain high-precision total station and GPS coordinates of subterranean features (royal tombs, temple treasury deposits, unexcavated hoards).
* Transmitting unexcavated site coordinates to public multi-tenant cloud servers exposes sensitive heritage sites to data leaks, enabling illicit antiquities looting and black-market trafficking.

### 1.2 Indigenous Data Sovereignty & The CARE Principles
* **The CARE Principles for Indigenous Data Governance** (Carroll et al. 2020; Global Indigenous Data Alliance):
  - **C — Collective Benefit:** Data ecosystems must enable Indigenous nations to derive tangible benefit from research.
  - **A — Authority to Control:** Indigenous peoples have the inherent right to control data concerning their cultural heritage, sacred sites, and ancestral remains.
  - **R — Responsibility:** Researchers must maintain respectful, accountable relationships.
  - **E — Ethics:** Minimizing harm and respecting tribal protocols.
* **NAGPRA Compliance (25 U.S.C. 3001):** The Native American Graves Protection and Repatriation Act mandates strict access controls over records, photographs, and bio-archaeological analyses of ancestral remains and funerary objects.

### 1.3 National Antiquities Legislation
* Many heritage-rich nations enforce strict data sovereignty laws:
  - **Italy:** *Codice dei Beni Culturali e del Paesaggio* (D.Lgs. 42/2004) mandates that preliminary excavation data remains under the jurisdiction of regional *Soprintendenze*.
  - **Egypt:** Law 117/1983 for Antiquities Protection restricts the foreign export of raw digital excavation archives.

### 1.4 Academic Pre-Defense Embargoes
* Doctoral candidates (PhDs) working on unpublished excavations cannot upload their primary field notes and dissertations to public cloud LLMs that scrape inputs for model training, which would violate institutional academic confidentiality and pre-defense embargoes.

---

## 2. Dual Deployment Topology

```
+---------------------------------------------------------------------------------------------------+
|                           ARCHAEOPHD AI DUAL DEPLOYMENT ARCHITECTURE                              |
+===================================================================================================+
| LOCAL AIR-GAPPED WORKSTATION (Win32 Sovereign Workstation)                                        |
| - Target: Solo PhD researchers, field trenches, national museums, sensitive archives.             |
| - Network Invariant: ZERO external network sockets; ZERO background telemetry.                   |
| - Local AI Execution: Bundled quantized GGUF neural models (via llama.cpp / ONNX).                |
| - Local Analytics: Local headless OxCal binary execution via standard pipes.                      |
| - Storage: Encrypted local SQLite/DuckDB files on user's machine.                                 |
| - Legal Compliance: Fully satisfies CARE, NAGPRA, Italian Codice, and anti-looting mandates.      |
+---------------------------------------------------------------------------------------------------+
                                                  ^
                                                  | (Optional Opt-In Synchronized Push)
                                                  v
+---------------------------------------------------------------------------------------------------+
| ENTERPRISE COLLABORATIVE EDITION (Private VPC / On-Premise Cloud)                                 |
| - Target: Large CRM firms (AECOM, WSP), preventive archaeology institutes (INRAP, MOLA).          |
| - Infrastructure: Deployed inside customer's secure AWS GovCloud, Azure, or on-prem servers.      |
| - Multi-User Workflows: Role-Based Access Control (RBAC), team review queues, audit logs.          |
| - Cloud Interoperability: Direct JSON-LD export to the European Collaborative Cloud (ECCCH).     |
+---------------------------------------------------------------------------------------------------+
```
