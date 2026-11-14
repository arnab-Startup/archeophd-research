# Visual Sorting & Typology Studio: Complete Architecture & Planning Library

> **Module:** 12 — Visual Sorting & Typology Studio  
> **Repository:** `d:\Prorgram\Project\ArcheoPhd\research\12_visual_sorting_and_typology_studio`  
> **Status:** Production Architecture, Product Strategy & Technical Specification  
> **Audience:** Co-Founders, Technical Lead, Vision Engineers, Field Specialists  

---

## Executive Summary

The **Visual Sorting & Typology Studio** is an interactive, computer-vision-augmented triage platform designed specifically for post-excavation archaeological field photography.

Rather than positioning AI as an autonomous, opaque classifier, the Studio operates on an **active learning, human-in-the-loop paradigm**:
1. Automatically isolates artifacts from trench background noise, soil, and shadows.
2. Generates domain-aware morphological and texture embeddings via self-supervised Vision Transformers (**DINOv2**).
3. Discovers organic typological groupings via density-based clustering (**HDBSCAN** over **UMAP**), keeping genuine outliers in a dedicated review tray.
4. Enables high-speed, keyboard-first human verification, dynamically adapting cluster boundaries as the specialist rejects or confirms items.
5. Cross-checks visual groups against the site's **Harris Matrix** to detect intrusive or residual stratigraphic anomalies.
6. Exports one-click publication-ready photographic plates and ISO-compliant **CIDOC CRM / CRMarchaeo** knowledge graphs.

---

## Directory Navigation

```
12_visual_sorting_and_typology_studio/
├── 01_domain_and_requirements/
│   ├── problem_statement.md             # The field triage bottleneck and cognitive fatigue
│   ├── user_stories_and_personas.md     # Ceramicists, lithic analysts, and project directors
│   ├── functional_requirements.md       # Ingestion, segmentation, clustering, active learning
│   └── non_functional_requirements.md   # Offline execution, CPU latency budget, data sovereignty
├── 02_computer_vision_architecture/
│   ├── background_isolation_and_segmentation.md # BiRefNet, MobileSAM, U2-Net background removal
│   ├── embedding_engine_dinov2.md       # DINOv2 self-supervised ViT patch and CLS embeddings
│   └── onnx_quantization_and_runtime.md # Int8 ONNX Runtime CPU integration in Win32 C++
├── 03_clustering_and_active_learning/
│   ├── hdbscan_and_dim_reduction.md     # Why K-Means fails; UMAP + HDBSCAN density clustering
│   ├── must_not_link_constraints.md     # Mathematical formulation of semi-supervised rejection
│   └── centroid_adaptation_and_routing.md # Top-2 next-best candidate routing and cluster adaptation
├── 04_ui_ux_interaction_design/
│   ├── light_table_canvas_view.md       # Interactive 2D scatter plot with WebGL/Canvas
│   ├── typology_tray_review_view.md     # High-speed masonry card deck with keyboard shortcuts (X, M, N)
│   └── publication_plate_generator.md   # Print-ready 300 DPI PDF plates with calibrated scale bars
├── 05_archaeological_integration_and_moat/
│   ├── stratigraphic_cross_check_engine.md # Cross-referencing visual clusters with Harris Matrix DAG
│   ├── cidoc_crm_export_schema.md       # JSON-LD mapping to E22, E55, A2, and D1 classes
│   └── offline_air_gapped_sovereignty.md # Zero telemetry, local storage, anti-looting GPS protection
└── 06_implementation_and_testing_plan/
    ├── step_by_step_milestones.md       # 4-phase delivery plan (Weeks 1 to 8)
    ├── cpp_engine_specification.md      # C++ VisualTypologyManager API and IPC endpoints
    └── test_and_benchmark_plan.md       # Mediterranean ceramics, Paleolithic lithics, metrics
```

---

## Direct File Links

### 01. Domain & Requirements
* [`01_domain_and_requirements/problem_statement.md`](file:///d:/Prorgram/Project/ArcheoPhd/research/12_visual_sorting_and_typology_studio/01_domain_and_requirements/problem_statement.md)
* [`01_domain_and_requirements/user_stories_and_personas.md`](file:///d:/Prorgram/Project/ArcheoPhd/research/12_visual_sorting_and_typology_studio/01_domain_and_requirements/user_stories_and_personas.md)
* [`01_domain_and_requirements/functional_requirements.md`](file:///d:/Prorgram/Project/ArcheoPhd/research/12_visual_sorting_and_typology_studio/01_domain_and_requirements/functional_requirements.md)
* [`01_domain_and_requirements/non_functional_requirements.md`](file:///d:/Prorgram/Project/ArcheoPhd/research/12_visual_sorting_and_typology_studio/01_domain_and_requirements/non_functional_requirements.md)

### 02. Computer Vision Architecture
* [`02_computer_vision_architecture/background_isolation_and_segmentation.md`](file:///d:/Prorgram/Project/ArcheoPhd/research/12_visual_sorting_and_typology_studio/02_computer_vision_architecture/background_isolation_and_segmentation.md)
* [`02_computer_vision_architecture/embedding_engine_dinov2.md`](file:///d:/Prorgram/Project/ArcheoPhd/research/12_visual_sorting_and_typology_studio/02_computer_vision_architecture/embedding_engine_dinov2.md)
* [`02_computer_vision_architecture/onnx_quantization_and_runtime.md`](file:///d:/Prorgram/Project/ArcheoPhd/research/12_visual_sorting_and_typology_studio/02_computer_vision_architecture/onnx_quantization_and_runtime.md)

### 03. Clustering & Active Learning
* [`03_clustering_and_active_learning/hdbscan_and_dim_reduction.md`](file:///d:/Prorgram/Project/ArcheoPhd/research/12_visual_sorting_and_typology_studio/03_clustering_and_active_learning/hdbscan_and_dim_reduction.md)
* [`03_clustering_and_active_learning/must_not_link_constraints.md`](file:///d:/Prorgram/Project/ArcheoPhd/research/12_visual_sorting_and_typology_studio/03_clustering_and_active_learning/must_not_link_constraints.md)
* [`03_clustering_and_active_learning/centroid_adaptation_and_routing.md`](file:///d:/Prorgram/Project/ArcheoPhd/research/12_visual_sorting_and_typology_studio/03_clustering_and_active_learning/centroid_adaptation_and_routing.md)

### 04. UI / UX Interaction Design
* [`04_ui_ux_interaction_design/light_table_canvas_view.md`](file:///d:/Prorgram/Project/ArcheoPhd/research/12_visual_sorting_and_typology_studio/04_ui_ux_interaction_design/light_table_canvas_view.md)
* [`04_ui_ux_interaction_design/typology_tray_review_view.md`](file:///d:/Prorgram/Project/ArcheoPhd/research/12_visual_sorting_and_typology_studio/04_ui_ux_interaction_design/typology_tray_review_view.md)
* [`04_ui_ux_interaction_design/publication_plate_generator.md`](file:///d:/Prorgram/Project/ArcheoPhd/research/12_visual_sorting_and_typology_studio/04_ui_ux_interaction_design/publication_plate_generator.md)

### 05. Archaeological Integration & Moat
* [`05_archaeological_integration_and_moat/stratigraphic_cross_check_engine.md`](file:///d:/Prorgram/Project/ArcheoPhd/research/12_visual_sorting_and_typology_studio/05_archaeological_integration_and_moat/stratigraphic_cross_check_engine.md)
* [`05_archaeological_integration_and_moat/cidoc_crm_export_schema.md`](file:///d:/Prorgram/Project/ArcheoPhd/research/12_visual_sorting_and_typology_studio/05_archaeological_integration_and_moat/cidoc_crm_export_schema.md)
* [`05_archaeological_integration_and_moat/offline_air_gapped_sovereignty.md`](file:///d:/Prorgram/Project/ArcheoPhd/research/12_visual_sorting_and_typology_studio/05_archaeological_integration_and_moat/offline_air_gapped_sovereignty.md)

### 06. Implementation & Testing Plan
* [`06_implementation_and_testing_plan/step_by_step_milestones.md`](file:///d:/Prorgram/Project/ArcheoPhd/research/12_visual_sorting_and_typology_studio/06_implementation_and_testing_plan/step_by_step_milestones.md)
* [`06_implementation_and_testing_plan/cpp_engine_specification.md`](file:///d:/Prorgram/Project/ArcheoPhd/research/12_visual_sorting_and_typology_studio/06_implementation_and_testing_plan/cpp_engine_specification.md)
* [`06_implementation_and_testing_plan/test_and_benchmark_plan.md`](file:///d:/Prorgram/Project/ArcheoPhd/research/12_visual_sorting_and_typology_studio/06_implementation_and_testing_plan/test_and_benchmark_plan.md)
