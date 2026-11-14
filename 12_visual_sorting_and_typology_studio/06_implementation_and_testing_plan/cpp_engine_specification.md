# C++ Engine Architecture & IPC Endpoints

> **Subproject:** Visual Sorting & Typology Studio  
> **Section:** 06 — Implementation & Testing Plan  
> **Status:** Production Reference  

---

## 1. Engine Core: `visual_typology_manager.hpp`

The core vision analytics will be implemented in `desktop/engine/analysis/visual_typology_manager.hpp`:

```cpp
namespace archaeophd::analysis {

struct ArtifactImageRecord {
    std::string image_id;
    std::string original_file_path;
    std::string cropped_file_path;
    std::string trench_id;
    std::string locus_id;
    std::string stratigraphic_unit_id;
    double scale_mm_per_pixel = 0.0;
    std::vector<float> embedding_384d;
    std::pair<float, float> umap_coords_2d;
    int cluster_id = -1; // -1 = Outlier / Unclassified
    bool human_verified = false;
};

struct TypologyCluster {
    int cluster_id = -1;
    std::string user_label; // e.g. "Type 3A: Carinated Bowls"
    std::vector<float> centroid_384d;
    std::vector<std::string> member_image_ids;
    double intra_cluster_variance = 0.0;
};

class VisualTypologyManager {
public:
    explicit VisualTypologyManager(const std::string& data_root);

    // Pipeline Execution
    bool IngestImageBatch(const std::vector<std::string>& file_paths);
    bool SegmentArtifacts();
    bool GenerateEmbeddings();
    bool RunClustering();

    // Active Learning & Review Loop
    bool RejectItemFromCluster(const std::string& image_id, int current_cluster_id);
    std::vector<std::pair<int, float>> GetNextBestClusters(const std::string& image_id, int top_k = 2);
    bool ReassignItem(const std::string& image_id, int target_cluster_id);
    int SpawnNewCluster(const std::string& seed_image_id, const std::string& label);

    // Export Facilities
    bool ExportPublicationPlatePdf(int cluster_id, const std::string& output_pdf_path);
    std::string ExportCidocJsonLd(int cluster_id);
};

} // namespace archaeophd::analysis
```

---

## 2. IPC Dispatcher Integration (`native_ipc_dispatcher.hpp`)

The desktop WebView2 frontend communicates with the C++ engine via JSON messages:

| Action | Payload Parameters | Returns |
|---|---|---|
| `start_visual_clustering` | `{ "folder_path": "...", "locus_id": "L14" }` | `{ "status": "processing", "total_images": 1420 }` |
| `get_clustering_status` | `{}` | `{ "progress": 0.85, "clusters_found": 8, "outliers": 12 }` |
| `get_canvas_layout` | `{}` | `{ "items": [ { "id": "img1", "x": 12.4, "y": -4.2, "cluster": 3 }, ... ] }` |
| `get_tray_contents` | `{ "cluster_id": 3 }` | `{ "label": "Type 3A", "images": [ { "id": "img1", "thumb": "..." }, ... ] }` |
| `reject_tray_item` | `{ "image_id": "img1", "cluster_id": 3 }` | `{ "suggested_cluster": 5, "similarity": 0.82 }` |
| `confirm_tray_item` | `{ "image_id": "img1", "cluster_id": 5 }` | `{ "status": "confirmed" }` |
| `export_publication_plate` | `{ "cluster_id": 3, "format": "pdf", "dpi": 300 }` | `{ "output_path": "D:/Exports/Plate_IV.pdf" }` |
