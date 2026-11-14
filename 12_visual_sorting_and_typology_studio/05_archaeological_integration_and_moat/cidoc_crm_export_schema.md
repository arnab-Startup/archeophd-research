# CIDOC CRM & CRMarchaeo Export Schema

> **Subproject:** Visual Sorting & Typology Studio  
> **Section:** 05 — Archaeological Integration & Moat  
> **Status:** Production Reference  

---

## 1. Transforming Visual Trays into ISO 21127 Knowledge Graphs

When an archaeologist finishes validating a visual cluster, the system does not just save a local folder of files. It automatically compiles a standard **CIDOC CRM / CRMarchaeo JSON-LD** knowledge graph:

```
[Raw Photo File] ────────► CRMdig: D1 Digital Object
                               │
                               ▼ (P138 represents)
[Physical Find]  ────────► CIDOC CRM: E22 Human-Made Object
                               │
                               ├─────────────────────────────────────────┐
                               ▼ (P2 has type)                           ▼ (AP21i is contained in)
[Typology Tray]  ────────► CIDOC CRM: E55 Type               [Stratum] ──► CRMarchaeo: A2 Volume Unit
```

---

## 2. Sample JSON-LD Triples Export

```json
{
  "@context": {
    "crm": "http://www.cidoc-crm.org/cidoc-crm/",
    "crmarchaeo": "http://www.cidoc-crm.org/crmarchaeo/",
    "crmdig": "http://www.cidoc-crm.org/crmdig/"
  },
  "@graph": [
    {
      "@id": "urn:archaeophd:photo:IMG_4021.JPG",
      "@type": "crmdig:D1_Digital_Object",
      "crm:P138_represents": {
        "@id": "urn:archaeophd:artifact:SNL-2026-B104"
      }
    },
    {
      "@id": "urn:archaeophd:artifact:SNL-2026-B104",
      "@type": "crm:E22_Human-Made_Object",
      "crm:P1_is_identified_by": "Inv. No. B104",
      "crm:P2_has_type": {
        "@id": "urn:archaeophd:typology:Type_3A_Carinated_Bowl",
        "@type": "crm:E55_Type",
        "crm:P3_has_note": "Carinated Red-Burnished Bowl with flaring rim"
      },
      "crmarchaeo:AP21i_is_contained_in": {
        "@id": "urn:archaeophd:stratum:TrenchB_Locus14",
        "@type": "crmarchaeo:A2_Stratigraphic_Volume_Unit"
      }
    }
  ]
}
```

### Institutional Value
This JSON-LD export directly integrates into:
* **The European Collaborative Cloud for Cultural Heritage (ECCCH)** via the Heritage Digital Twin Ontology (HDTO).
* Institutional museum repositories (ADS, Open Context, Ariadneplus).
