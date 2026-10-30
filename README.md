# MET kinase DMS benchmark

Deep mutational scanning of the MET kinase domain against 11 inhibitors plus a
vehicle control, paired with predictions from 57 computational methods, and the
comparable DMS datasets for five other kinases.

The measurements are 5,434 MET missense variants x 12 conditions = 65,208 rows.
Conditions are DMSO (control) and the inhibitors A458, Cabo, Camp, Crizo, Gle,
Glu, Mere, NVP, Savo, Tepo, Tiv.

## Repository layout

```
MET_muteff_kinase_domain.csv    65,208 x 36   mutational effect, 287 aa domain context 
MET_muteff_full_length.csv      65,208 x 31   mutational effect, 1390 aa context
MET_affinity.csv                65,208 x 29   protein-ligand affinity and binding ddG 

kinases/                        five non-MET kinase DMS datasets, one CSV each, not split
  CDK4.csv                      11,476 x 34   CDK4,     DMSO + Pal
  CDK6.csv                      12,350 x 34   CDK6,     DMSO + Pal
  EGFR.csv                       4,911 x 34   EGFR,     DMSO + Afa, Osi
  FGFR.csv                      22,566 x 34   FGFR1-4,  DMSO + Fut, Pem
  SRC.csv                       16,943 x 34   SRC,      DMSO + Das, Inhib1, Inhib2, Inhib4

clean/                          experiment only -- no model predictions
  kinase_dms_combined.csv       133,454 x 10  every DMS measurement here in one table
  kinase_drug_pairs.csv              36 x 11  sequence + SMILES for each (kinase, inhibitor) pair

struc_prediction/               WT cofold structures, 12 conditions x 3 methods, all mmCIF
  af3_wt_cofold/                AF3,     <Condition>.cif
  boltz2_wt_cofold/             Boltz-2, <Condition>.cif
  chai1_wt_cofold/              Chai-1,  <Condition>.cif

diff-scores/                    compute change of fitness score over inhibitor conditions

diff-tail-scores/               identification of potential sensitizing and resistance mutations

raw-data/                       raw data from the literature

scripts/
  difference-scores.ipynb       codes of compute difference in fitness score 
  score-statistics.ipynb        statistical analysis of the fitness scores
  analysis.ipynb                figure notebook
```


## Annotation columns 

| column | meaning |
|---|---|
| `kv` | `key` + variant, the unique row id |
| `key` | condition (DMSO or inhibitor) |
| `variants` | variant, kinase-domain numbering (1-287); add 1058 for MET numbering |
| `position`, `mutation` | position and mutant residue |
| `type` | all `missense` |
| `mean` | measured DMS score in this condition (the target) |
| `mean_ctrl` | measured DMS score in DMSO for the same variant |
| `label_sensitized`, `label_resisted` | binary calls |
| `binding_region_label` | residue within 5 A of the drug in the cofold (5,333 True) |
| `min_dist`, `dist` | residue-to-drug distance in the per-condition cofold |


## Cite this work

If you use this data in your research, please cite the following paper:

