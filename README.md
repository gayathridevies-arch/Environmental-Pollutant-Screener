# Environmental-Pollutant-Screener
An automated cheminformatics pipeline built with Python, RDKit, and Pandas to screen chemical datasets for hazardous structural alerts using custom SMARTS patterns.

## Overview
This tool processes a dataset of organic compounds, converts SMILES strings into 2D molecular structures, and evaluates them against defined toxicological substructures (such as halogenated groups, nitroaromatics, phenolics, and aromatic amines). Flagged compounds are automatically filtered and rendered into a visual grid gallery for rapid inspection.

## Features
- **Automated Parsing:** Converts SMILES to RDKit molecule objects using `PandasTools`.
- **Substructure Screening:** Matches molecules against specific SMARTS patterns.
- **Boolean Flagging:** Row-wise hazard tagging using dynamic Pandas operations.
- **Visual Export:** Generates an image grid (`MolsToGridImage`) of flagged compounds with metadata legends.
- **Defensive Handling:** Includes safety checks to prevent rendering errors on empty subsets.
---

## Tech Stack & Dependencies

* **Language:** Python 3.8+
* **Cheminformatics:** [RDKit] (`rdkit.Chem`, `rdkit.Chem.Draw`, `rdkit.Chem.PandasTools`)
* **Data Processing:** [Pandas]
* **Environment:** Jupyter Notebook / Google Colab

---

## Target Structural Alerts (SMARTS)

The screener evaluates input chemicals against key functional groups associated with environmental persistence, bioaccumulation, or aquatic toxicity:

| Hazard Category | Target Functional Group | SMARTS Pattern | Environmental Relevance |
| :--- | :--- | :--- | :--- |
| **Halogenated Compounds** | Organohalides | `[#6][F,Cl,Br,I]` | Persistent organic pollutants (POPs), halogenated solvents |
| **Nitroaromatic Groups** | Nitro-substituted aromatics | `c[N+](=O)[O-]` | Explosives residue, industrial intermediates |
| **Phenolic Structures** | Aromatic hydroxyl groups | `c[OH]` | Endocrine disruptors, industrial disinfectants |
| **Aromatic Amines** | Amino-substituted aromatics | `[c][NX3;H2,H1]` | Dye degradation products, carcinogenic hazards |

---
## Results & Performance Summary

When executed against the benchmark dataset of **20 representative organic compounds**, the automated pipeline successfully delivered the following performance:

* **Total Compounds Screened:** 20
* **Unique Hazardous Compounds Flagged:** 13 (65%)
* **Clean / Non-Flagged Compounds:** 7 (35%)

### Breakdown of Triggered Structural Alerts
| Hazard Category | SMARTS Pattern | Trigger Count | Toxicological Significance |
| :--- | :--- | :--- | :--- |
| **Halogenated Compounds** | `[#6][F,Cl,Br,I]` | **7** | Persistence in soil and groundwater, bioaccumulation |
| **Phenolic Structures** | `c[OH]` | **4** | Endocrine disruption, industrial disinfectant runoff |
| **Nitroaromatic Groups** | `c[N+](=O)[O-]` | **3** | High environmental mobility, toxicity/explosives residue |
| **Aromatic Amines** | `[c][NX3;H2,H1]` | **2** | Known/suspected carcinogens, dye industry byproducts |

