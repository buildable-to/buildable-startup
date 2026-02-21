# Buildable — Context Enrichment Resources

Resources to feed into Claude's context window for generating better structural drawings. Organized by priority and category.

---

## 1. PRECAST CONCRETE DESIGN MANUALS (Free PDFs)

**PCI (Precast/Prestressed Concrete Institute)** — 65+ free manuals available at pci.org after registration.

| Resource | URL | Why It Matters |
|----------|-----|----------------|
| PCI Manual for Hollow Core Slabs & Walls (MNL-126-15) | https://www.pci.org/ItemDetail?iProductCode=MNL-126-15 | Core reference — hollow core slab design, tolerances, diaphragm action, connection details. **Free PDF** |
| PCI Architectural Precast Concrete Manual (MNL-122-07) | https://www.universalconcrete.com/design/pci-arch-precast-concrete-3rd-ed.pdf | Panel design, finishes, connections, erection. **Free PDF** |
| PCI Guide Specifications — Structural Precast | https://www.pci.org/GuideSpecifications | Master spec for structural precast — can be distilled into drawing annotation rules |
| PCI Standard Design Practice (SDP) | https://www.pci.org/PCI_Docs/Design_Resources/Misc/PCI-SDP.pdf | Interpretations of ACI 318 for precast — the "how we actually do it" document. **Free PDF** |
| PCI All Free Guides & Manuals | https://www.pci.org/GuidesAndManuals | Full listing of 65+ free downloads |
| PCI Free Literature Index | https://www.pci-central.org/free-pci-literature | Curated list with direct links |

**PCI Design Handbook** (the bible — not free, but older editions available):
| Resource | URL | Notes |
|----------|-----|-------|
| PCI Design Handbook 5th Ed | https://normanray.files.wordpress.com/2011/03/pci_design_handbook_5th-ed_precast-prestressed-concrete.pdf | Free PDF — older but fundamentals still valid |
| PCI Design Handbook 6th Ed | https://www.rexresearch1.com/ConcreteManufacture2Library/PCIDesignHandbkPrecastPrestressedConcreteMartin.pdf | Free PDF |
| PCI Design Handbook 8th Ed (latest) | https://www.pci.org/PCI/PCI/Bookstore/Item_Detail.aspx?iProductCode=MNL-120-17 | Paid — $350, but the definitive reference |

---

## 2. BUILDING CODES & STANDARDS

### Eurocode (European / Georgian market)

| Resource | URL | Why It Matters |
|----------|-----|----------------|
| Eurocode 2 Worked Examples (EC2) | https://www.theconcreteinitiative.eu/images/ECP_Documents/Eurocode2_WorkedExamples.pdf | **Free PDF** — step-by-step design examples to EN 1992, load combinations, beam/column design |
| JRC Eurocode 2 — Design of Concrete Buildings (Worked Examples) | https://publications.jrc.ec.europa.eu/repository/handle/JRC89037 | **Free PDF** — official EU worked examples covering conceptual design through detailing |
| How to Design Concrete Structures using Eurocode 2 | https://icci.vn/storage/documents/November2023/How%20to%20design%20concrete%20structures%20using%20Eurocode%202.pdf | **Free PDF** — practical transition guide with tables, charts, detailing rules |
| Worked Examples to Eurocode 2: Volume 1 | http://ndl.ethernet.edu.et/bitstream/123456789/87977/66/Worked-Examples-Ec2%20Volume%20I.pdf | **Free PDF** — distilled design procedures |
| Precast Eurocode 2: Worked Examples (British Precast) | https://civilnode.com/download-book/10299854001657/precast-eurocode-2-worked-examples-for-the-design-of-precast-concrete-building-structures-to-bs-en | Specifically for precast to EC2 — 13 worked examples |
| Precast Eurocode 2: Design Manual | https://www.concrete.org.uk/fingertips/precast-eurocode-2-design-manual/ | Companion to above — summary of EC2 for precast |
| Design of Prestressed Concrete to EC2 (textbook) | https://icci.vn/storage/documents/December2024/Raymond%20Ian%20Gilbert,%20Neil%20Colin%20Mickleborough,%20Gianluca%20Ranzi%20-%20Design%20of%20prestressed%20concrete%20to%20Eurocode%202%20(2017,%20CRC%20Press).pdf | **Free PDF** — comprehensive prestressed concrete design |
| Eurocodes Homepage (JRC) | https://eurocodes.jrc.ec.europa.eu/ | Official portal — NDPs database, software list, worked examples per Eurocode part |

### ACI (American market)

| Resource | URL | Notes |
|----------|-----|-------|
| ACI 318 — Building Code for Structural Concrete | Purchase required | The foundational US code — distill key tables (cover, spacing, rebar ratios) |
| ACI ITG-7-09 — Tolerances for Precast Concrete | https://www.pa.gov/content/dam/copapwp-pagov/en/dli/documents/ucc/documents/2018-icc-code-review-public-comments/szoke-itg7_09.pdf | **Free PDF** — tolerance tables with figures for every precast element type |
| NPCA Guide Specifications for Precast Products | https://precast.org/wp-content/uploads/111423_Resources_NPCA-General-Guide-Specifications-for-Precast-Concrete-Products-061423V2.pdf | **Free PDF** — manufacturing standards, reinforcement, shop drawing requirements |

### Other Standards

| Resource | URL | Notes |
|----------|-----|-------|
| Hong Kong Precast Concrete Construction Handbook | https://www.hkie-st.org/wp-content/uploads/2022/06/50_PCC-Handbook-22-October-2015.pdf | **Free PDF** — practical guide with tables, figures, erection tolerances |
| Portland Precast Manufacturing Standards | https://www.portland.gov/bes/documents/manufacturing-standards-precast-concrete-products/download | **Free PDF** — reinforcement specs, QC standards |

---

## 3. FREECAD ECOSYSTEM

| Resource | URL | Why It Matters |
|----------|-----|----------------|
| FreeCAD Reinforcement Workbench | https://github.com/amrit3701/FreeCAD-Reinforcement | **Critical** — Python API for rebar generation (straight, U-shape, L-shape, stirrup, helical), BOM, bar bending schedules, rebar drawings. Study this API for your own detailing |
| FreeCAD Reinforcement Wiki | https://wiki.freecadweb.org/Reinforcement_Workbench | Documentation for all rebar tools |
| FreeCAD Arch Structure (presets) | https://wiki.freecadweb.org/Arch_Structure | Built-in precast concrete presets — Python scriptable via `Arch.makeStructure()` |
| FreeCAD Addons Directory | https://www.freecad.org/addons.php | Full addon listing — Reinforcement v0.5 (updated Feb 2026) |
| FreeCAD API Documentation | https://wiki.freecadweb.org/FreeCAD_Scripting_Basics | Python scripting reference |
| Rebaring in FreeCAD (tutorials) | https://cnirbhay.wordpress.com/category/rebaring-in-freecad/ | Practical walkthroughs with screenshots |

---

## 4. PYTHON LIBRARIES FOR STRUCTURAL ENGINEERING

Libraries Claude can reference or whose logic can inform drawing generation:

| Library | URL | Use Case |
|---------|-----|----------|
| **concreteproperties** | https://github.com/robbievanleeuwen/concrete-properties | RC section properties, moment-curvature, interaction diagrams. Eurocode stress-strain profiles built in |
| **concreteproperties-ACI** | https://github.com/Lomarandil/concrete-properties-ACI | Fork with ACI 318 design code |
| **Blueprints** | https://github.com/Blueprints-org/blueprints | **Eurocode implementations** (EN 1992, 1993, 1997) — material definitions, steel profile DB, section checks. MIT license |
| **sectionproperties** | https://github.com/robbievanleeuwen/section-properties | Cross-section analysis via FEM — area, centroid, moments of inertia |
| **PyNite** | https://github.com/JWock82/PyNite | 3D structural FEA — linear/non-linear, load combinations |
| **HollowRC** | https://github.com/Kleissl/HollowRC | Hollow RC section design under combined actions |
| **IfcOpenShell** | https://ifcopenshell.org/ | IFC file manipulation in Python — essential for BIM interoperability |
| **StruPy** | https://pypi.org/project/strupy/ | Structural engineering design package — concrete & steel |
| **handcalcs** | https://github.com/connorferster/handcalcs | Renders Python calcs as hand-written equations — useful for documentation |
| **awesome-structuralengineering** | https://github.com/brhenri-mr/awesome-structuralengineering | Curated list of all structural engineering libraries |
| **GitHub Topic: structural-engineering** | https://github.com/topics/structural-engineering | Browse all repos tagged structural engineering |
| **GitHub Topic: reinforced-concrete** | https://github.com/topics/reinforced-concrete | Browse all repos tagged reinforced concrete |

---

## 5. BIM & IFC INTEROPERABILITY

| Resource | URL | Why It Matters |
|----------|-----|----------------|
| IFC Standard (buildingSMART) | https://technical.buildingsmart.org/standards/ifc/ | Official IFC specification — entity definitions for IfcColumn, IfcBeam, IfcSlab, etc. |
| IFC Wikipedia Overview | https://en.wikipedia.org/wiki/Industry_Foundation_Classes | Quick reference for IFC schema, file formats, history |
| BIM-Enabled Automation for RC Slab Design (ResearchGate) | https://www.researchgate.net/publication/318427051 | Research using exactly your stack: IFC + FreeCAD + Python + IfcOpenShell for automated RC slab design and 2D rebar drawings |
| IFC Interoperability Assessment (MDPI) | https://www.mdpi.com/2076-3417/11/23/11430 | Benchmark study of CAD↔CAE interoperability via IFC — pitfalls to avoid |
| Automated Retaining Structure Design (ScienceDirect) | https://www.sciencedirect.com/science/article/pii/S2467967425000716 | Extends IFC entities, automates rebar detailing, generates 3D without 2D — validates forward-design approach |

---

## 6. CAD DRAWING DATASETS & RESEARCH

For future reference / potential training data if approach changes:

| Resource | URL | What It Contains |
|----------|-----|-----------------|
| ArchCAD-400K | https://arxiv.org/html/2503.22346v1 | 5,538 CAD drawings, 413K chunks, 27 categories including structural components |
| FloorPlanCAD | https://openaccess.thecvf.com/content/ICCV2021/papers/Fan_FloorPlanCAD_A_Large-Scale_CAD_Drawing_Dataset_for_Panoptic_Symbol_Spotting_ICCV_2021_paper.pdf | 10,000+ floor plans as vector graphics, 30 annotated categories |
| Eng_Diagrams | https://github.com/heyad/Eng_Diagrams | 2,432 engineering symbols from P&ID drawings |

---

## 7. INDUSTRY TOOLS TO STUDY (competitive intelligence + conventions)

| Tool | URL | What to Learn From It |
|------|-----|----------------------|
| ALLPLAN Precast | https://www.allplan.com/us_en/products/allplan-precast/ | Automated shop drawing generation, rule-based dimensioning — study their output conventions |
| ALLPLAN 2026 Release | https://www.engineering.com/allplan-launches-2026-releases-with-new-ai-and-bim-tools/ | Latest AI + BIM features — column reinforcement automation, precast fabrication workflows |
| ARKANCE Precast Concrete (Revit plugin) | https://agacad.com/products/precast-concrete | Automated detailing, connection placement, shop ticket generation in Revit |
| Civils.ai | https://civils.ai/ | AI for PDF CAD takeoffs — natural language measurement from drawings |

---

## 8. RESEARCH PAPERS ON RAG FOR CONSTRUCTION

Approaches directly applicable to context injection:

| Paper | URL | Key Insight |
|-------|-----|-------------|
| NVIDIA: RAG Guide for AEC | https://developer.nvidia.com/blog/a-guide-to-retrieval-augmented-generation-for-aec/ | Practical RAG architecture for construction — document retrieval, compliance checking |
| RAG4CM (Construction Management) | https://www.sciencedirect.com/science/article/abs/pii/S1474034625000515 | Hierarchical document parsing → knowledge pool, semantic retrieval with voting |
| CC-RAG (Construction Contracts) | https://www.sciencedirect.com/science/article/abs/pii/S2352710225004255 | Domain-adapted RAG — 7B model outperforms 671B with proper chunking |
| Hybrid RAG for Building Engineering | https://www.sciencedirect.com/science/article/abs/pii/S2352710225004255 | Property graph + vector hybrid index for building lifecycle knowledge |

---

## RECOMMENDED PRIORITY ORDER

### Immediate (distill into context files this week):
1. PCI Hollow Core Slab Manual (MNL-126) — the core element you're generating
2. PCI Standard Design Practice — how engineers actually interpret codes for precast
3. FreeCAD Reinforcement Workbench source code — align your Python with its API patterns
4. ACI ITG-7-09 tolerance tables — the numbers for dimensioning accuracy
5. Eurocode 2 Worked Examples — if targeting European/Georgian market

### Short-term (next 2-4 weeks):
6. PCI Design Handbook (5th or 6th ed free PDF) — connection details, design aids
7. Blueprints Python library — Eurocode implementations you can reference
8. concreteproperties library — section analysis logic
9. IFC schema documentation — ensure output interoperability

### Medium-term (next 1-3 months):
10. ALLPLAN/ARKANCE output study — understand professional drawing conventions
11. ArchCAD-400K dataset — for potential drawing understanding features
12. RAG research papers — if you move toward more sophisticated context management
