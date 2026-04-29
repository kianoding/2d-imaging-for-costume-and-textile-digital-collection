# Overview

This page provides a visual reference for the full imaging workflow — how items move through the system, what tools are used at each stage, and how the documentation is organized.

---

## Data Flow — Object to Digital Asset

```mermaid
flowchart TD
    A([📦 Physical Object\nin Storage]) --> B

    subgraph PLAN ["01 · PLANNING — Preparators / Catalogers"]
        B[Backlog Selection\nSelect & prioritize items] --> C
        C[Planning & Grouping\nClassify type · Assign setup · Confirm record]
    end

    subgraph PREP ["02 · PREPARATION — Preparators"]
        D[Prep Rack Staging\nOrganize into Zone A / B / C] --> E
        E[Mounting\nMannequin · Hanger · Lightbox · Flat Lay]
    end

    subgraph IMAGE ["03 · IMAGING — Photographer + Preparators"]
        F[Image Capture\nCapture required views: F · B · S · D · L · G] --> G
        G[Intake & Verification\nUpload RAW · Check completeness · Confirm naming]
    end

    subgraph POST ["04 · POST-PROCESSING — Photographer + Catalogers"]
        H[Image Processing\nSelect · Crop · Adjust in Adobe Bridge + Photoshop] --> I
        I[File Naming & Storage\nApply naming convention] --> J
        J[Metadata Entry\nGoogle Sheets · VRA Core · Costume Core fields] --> K
        K[Quality Control\nPass / Fail check on image + metadata]
    end

    subgraph OUTPUT ["05 · OUTPUT & STORAGE — Photographer + Catalogers"]
        L[Storage & Output\nMove to final folders · Confirm TIFF + JPG] --> M
        M[Physical Tagging & Labeling\nGenerate labels via Python script]
    end

    C --> D
    E --> F
    G --> H
    K --> L
    M --> N

    N([✅ Digital Object\nPreservation + Access Files\n+ Metadata Record])

    style PLAN fill:#f0f4ff,stroke:#6b7fc4
    style PREP fill:#fff8f0,stroke:#c49a6b
    style IMAGE fill:#f0fff4,stroke:#6bc47f
    style POST fill:#fff0f8,stroke:#c46ba0
    style OUTPUT fill:#f8f0ff,stroke:#9a6bc4
```

---

## Imaging Setup by Object Type

```mermaid
flowchart LR
    A[Item from\nSession List] --> B{Object Type?}

    B -->|Textile / Flat\ne.g. sash, obi, belt| C[📄 Flat Lay\nOverhead / Copy Stand]
    B -->|Accessory\ne.g. bag, hat, shoes| D[💡 Lightbox]
    B -->|Garment\ne.g. dress, jacket| E{Garment Type?}
    B -->|Ensemble\ne.g. suit, full costume| F[🧍 Studio\nFull Body Hanging Mannequin]

    E -->|Upper body / Dress| G[🧍 Studio\nStanding Mannequin]
    E -->|Bottoms / Full length| F
```

---

## Tools by Stage

| Stage | Tools Used |
|---|---|
| **Planning** | Google Sheets (inventory + catalog records) |
| **Preparation** | Google Sheets (session tracking), physical rack + mannequins |
| **Imaging** | Camera (fixed + handheld), color card, lightbox, copy stand |
| **Post-Processing** | Adobe Bridge (file management + batch rename), Adobe Photoshop (editing + export) |
| **Output & Storage** | Controlled folder structure, Python script (label generation), Google Colab (optional batch processing) |

---

## FADGI Imaging Specifications

The following specifications are drawn from the *Technical Guidelines for Digitizing Cultural Heritage Materials* (FADGI, 3rd ed., 2023) and adapted for costume and textile digitization.

| Parameter | Specification | Notes |
|---|---|---|
| **Preservation format** | TIFF (uncompressed) | Master file — never re-save as TIFF after editing |
| **Access format** | JPG | Derivative for sharing and viewing |
| **Resolution** | 400 PPI minimum | For textiles: 600 PPI recommended to capture weave detail |
| **Bit depth** | 24-bit color (8-bit per channel) | Minimum for color items |
| **Color profile** | sRGB or Adobe RGB 1998 | Consistent across all sessions |
| **Color card** | Required in first frame of each batch | Use to verify color accuracy; remove for final output files |
| **Camera position** | Fixed per setup type | Do not change position mid-batch |
| **Lighting** | Consistent, diffused, no harsh shadows | Two-light minimum for studio setup |
| **File naming** | Per naming convention (see File Naming section) | Applied at Intake & Verification stage |

> **Color card note:** Capture one frame with the color card visible at the start of each batch. This frame is used for calibration and quality verification — it is not included in the final output files.

---

## Repository Structure (GitHub)

```
2D-Imaging-Workflow-SOP/
│
├── README.md                          ← Entry point / handbook overview
├── SUMMARY.md                         ← Navigation index
├── OVERVIEW.md                        ← This page — diagrams, tools, specs
│
├── docs/
│   ├── 01_Planning/
│   │   ├── Backlog_Selection.md
│   │   └── Planning_and_Grouping.md
│   │
│   ├── 02_Preparation/
│   │   ├── Prep_Rack.md
│   │   └── Mounting.md
│   │
│   ├── 03_Imaging/
│   │   ├── Photography.md
│   │   └── Intake_and_Verification.md
│   │
│   ├── 04_Post_Processing/
│   │   ├── Image_Processing.md
│   │   ├── File_Naming_and_Storage.md
│   │   ├── Metadata.md
│   │   └── Quality_Control.md
│   │
│   └── 05_Output_and_Storage/
│       ├── Storage_and_Output.md
│       └── Physical_Tagging_and_Box_Labeling.md
│
├── assets/
│   ├── diagrams/                      ← Exported workflow diagrams
│   └── screenshots/                   ← Adobe Bridge, Google Sheets, etc.
│
├── templates/
│   ├── catalog_sheet_template.xlsx    ← Catalog + session tracking
│   └── photography_checklist.xlsx     ← Per-session QC checklist
│
└── scripts/
    ├── generate_labels.py             ← Physical label generator
    └── generate_tags.py               ← File tag automation
```

---

## Navigation

| Stage | Page |
|---|---|
| Start here | [README](README.md) |
| Stage 01 | [Backlog Selection](docs/01_Planning/Backlog_Selection.md) · [Planning & Grouping](docs/01_Planning/Planning_and_Grouping.md) |
| Stage 02 | [Prep Rack](docs/02_Preparation/Prep_Rack.md) · [Mounting](docs/02_Preparation/Mounting.md) |
| Stage 03 | [Photography](docs/03_Imaging/Photography.md) · [Intake & Verification](docs/03_Imaging/Intake_and_Verification.md) |
| Stage 04 | [Image Processing](docs/04_Post_Processing/Image_Processing.md) · [File Naming](docs/04_Post_Processing/File_Naming_and_Storage.md) · [Metadata](docs/04_Post_Processing/Metadata.md) · [QC](docs/04_Post_Processing/Quality_Control.md) |
| Stage 05 | [Storage & Output](docs/05_Output_and_Storage/Storage_and_Output.md) · [Physical Labeling](docs/05_Output_and_Storage/Physical_Tagging_and_Box_Labeling.md) |
