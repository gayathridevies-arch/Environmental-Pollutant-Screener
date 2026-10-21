# Environmental-Pollutant-Screener
An automated, pythonic cheminformatics pipeline built with **RDKit** and **Pandas** to screen organic chemical compounds for hazardous structural alerts. This tool processes molecular datasets, applies customizable SMARTS pattern filters to identify specific toxicological functional groups, and automatically renders a visual grid gallery of flagged pollutants.

---

## Key Features

* **Automated Structure Parsing:** Converts SMILES identifiers into RDKit 2D molecular objects using vectorized `PandasTools`.
* **SMARTS Pattern Matching:** Screens chemical structures against a curated dictionary of SMARTS expressions corresponding to environmental functional groups (e.g., nitroaromatics, halogenated hydrocarbons, phenolic groups, aromatic amines).
* **Multi-Criteria Hazard Flagging:** Employs dynamic Boolean row-wise aggregation (`.any(axis=1)`) to automatically tag compounds triggering one or more structural alerts.
* **Interactive Data Filtering:** Isolates hazardous molecules into dedicated subsets for downstream risk assessment.
* **Visual Grid Gallery:** Automatically renders high-resolution 2D molecular grid galleries (`MolsToGridImage`) complete with compound metadata legends.
* **Defensive Pipeline Design:** Implements safeguard logic (`len(matched_df) > 0`) to prevent visualization crashes during dry/clean data runs.

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
| **Aromatic Amines** | Amino-substituted aromatics | `c[NH2]` | Dye degradation products, carcinogenic hazards |

---


