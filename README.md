# breast-cancer-biomarker-docking
In Silico Identification, PPI Network Mapping, 3D Structural Profiling, and Molecular Docking of Breast Cancer Target EPCAM


# 🧬 In Silico Biomarker Discovery & Molecular Docking of EPCAM in Breast Cancer

An end-to-end, browser-based bioinformatics pipeline for identifying overexpressed transcriptomic biomarkers, constructing protein interaction networks, modeling 3D protein structures, and performing molecular docking simulations.

---

## 📌 Executive Summary
* **Target Disease:** Breast Carcinoma (Invasive & Epithelial Subtypes)
* **Dataset Analyzed:** NCBI GEO Accession [GSE15852](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE15852) (Paired Primary Tumor vs. Normal Tissue)
* **Primary Biomarker Target Identified:** **EPCAM** (Epithelial Cell Adhesion Molecule; UniProt ID: `P16422`)
* **Key Findings:** 
  1. GEO2R differential expression analysis revealed significant upregulation of **EPCAM**, **CD24**, **KRT19**, and **GATA3** ($logFC > 1.5, adj. P < 0.05$).
  2. PPI Network analysis confirmed **EPCAM** as a central hub protein interacting densely with membrane adhesion markers.
  3. AlphaFold 3D profiling demonstrated a highly stable extracellular globular domain ($pLDDT > 90$).
  4. SwissDock molecular docking with **Tamoxifen** produced a binding energy of **$-4.376\text{ kcal/mol}$**. The weak binding affinity indicates that small-molecule drugs like Tamoxifen do not target EPCAM directly, supporting clinical preferences for antibody-based therapies (e.g., Adecatumumab).

---

## 🛠️ Tools & Technologies Used

| Phase | Tool / Database | Description | Link |
| :--- | :--- | :--- | :--- |
| **Data Mining** | NCBI GEO2R | Differential Gene Expression Analysis | [ncbi.nlm.nih.gov/geo/geo2r](https://www.ncbi.nlm.nih.gov/geo/geo2r/) |
| **Network Biology** | STRING-db v12 | Protein-Protein Interaction (PPI) Mapping | [string-db.org](https://string-db.org/) |
| **Structural Modeling** | AlphaFold DB | AI-predicted 3D Structure & pLDDT Profiling | [alphafold.ebi.ac.uk](https://alphafold.ebi.ac.uk/) |
| **Molecular Docking** | SwissDock | Web-based AutoDock Vina Docking Server | [swissdock.ch](https://www.swissdock.ch/) |

---

## 📋 Step-by-Step Methodology & Results

### Step 1: Differential Gene Expression Analysis (GEO2R)
- **Dataset Selection:** Dataset `GSE15852` containing paired tumor and adjacent normal breast tissue.
- **Group Allocation:** Defined sample groups into `Tumor` ($n = 43$) and `Normal` ($n = 43$).
- **Statistical Parameters:**
  - Adjustment: Benjamini & Hochberg (FDR)
  - Log2 Fold Change Threshold: $1.5$
  - Cut-off $p$-value: $< 0.05$
- **Result:** Extracted top co-upregulated genes including *EPCAM*, *CD24*, *KRT19*, *GATA3*, *MUC1*, *SDC1*, *AGR2*, *TACSTD2*, and *CD9*.

---

### Step 2: Protein-Protein Interaction (PPI) Network Mapping
- Top candidate genes were mapped in **STRING-db** for *Homo sapiens*.
- **Network Statistics:**
  - Number of nodes: $9$
  - Number of edges: $21$
  - Average node degree: $4.67$
  - PPI enrichment $p$-value: $< 1.0 \times 10^{-16}$
- **Result:** Identified **EPCAM** and **KRT19** as central hub proteins with high edge connectivity.

![STRING Network](string_network.png)

---

### Step 3: 3D Structural & Domain Analysis (AlphaFold DB)
- Downloaded the high-confidence structure for human EPCAM (`AF-P16422-F1`).
- **pLDDT Structural Confidence Analysis:**
  - **Extracellular Globular Domain:** $pLDDT > 90$ (Dark Blue: Very high confidence, rigid core).
  - **Transmembrane Helical Domain:** $70 < pLDDT < 90$ (Light Blue: High confidence).
  - **Terminal Loops:** $pLDDT < 50$ (Orange: Flexible / unstructured loops).

![AlphaFold Structure](alphafold_structure.png)

---

### Step 4: Molecular Docking & Binding Affinity Analysis (SwissDock)
To test whether small-molecule breast cancer drugs bind directly to EPCAM, molecular docking was carried out using SwissDock (AutoDock Vina engine).

#### Docking Parameters:
- **Target Protein:** Human EPCAM (`AF-P16422-F1-model_v6.pdb`)
- **Ligand:** Tamoxifen (SMILES: `CCC(=C(C1=CC=CC=C1)C2=CC=CC=C2)C3=CC=C(C=C3)OCCN(C)C`)
- **Grid Box Center:** $(X=1, Y=8, Z=-3)$
- **Box Size:** $20 \times 20 \times 20 \text{ \AA}$
- **Sampling Exhaustivity:** $1$

#### Docking Results:

| Pose Model | Calculated Binding Affinity ($\Delta G$) | Interaction Profile |
| :---: | :---: | :--- |
| **Model 1 (Top Pose)** | **$-4.376\text{ kcal/mol}$** | Weak hydrophobic surface contacts |
| **Model 2** | **$-1.424\text{ kcal/mol}$** | Nonspecific external contact |

![SwissDock Results](swissdock_tamoxifen.jpg)

---

## 💡 Discussion & Biological Insights
1. **Target Suitability:** EPCAM is a cell surface adhesion glycoprotein, not an intracellular kinase or nuclear receptor.
2. **Docking Energy Evaluation:** Standard therapeutic small-molecule drugs require $\Delta G < -7.0\text{ kcal/mol}$ for high-affinity binding. The observed score of **$-4.376\text{ kcal/mol}$** confirms that Tamoxifen lacks strong direct affinity for EPCAM.
3. **Clinical Relevance:** These computational findings mirror clinical observations: because EPCAM lacks deep catalytic small-molecule binding pockets, **antibody-based biologics** (e.g., Adecatumumab) or antibody-drug conjugates (ADCs) are required for effective therapeutic targeting rather than traditional small-molecule drugs.

---

## 📂 Repository Contents
```text
├── AF-P16422-F1-model_v6.pdb   # AlphaFold 3D coordinates file for EPCAM
├── string_network.png          # High-res PPI interaction network
├── alphafold_structure.png     # Rendered 3D structural confidence view
├── swissdock_tamoxifen.jpg     # SwissDock binding energy pose visual
└── README.md                   # Full project documentation
