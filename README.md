# ENG2440 Assignment 3 - blood-brain barrier penetration from molecular graphs

Mohamed Abdalla (25011148)

A Morgan fingerprint baseline and a bond-aware GNN (GINEConv) on the BBBP dataset,
compared under a random split and a Bemis-Murcko scaffold split.

This is coursework on a benchmark dataset. Nothing here says whether a real compound
crosses the barrier in a person.

## What is in here

| File | What it is |
| --- | --- |
| `A3_bbbp_gnn.ipynb` | The whole analysis, executed with outputs. All the code is in this one notebook. |
| `requirements.txt` | Pinned versions of everything the notebook imports. |

The BBBP data is not in the repo. PyTorch Geometric downloads it on the first run,
and `data/` is in `.gitignore`. The report PDF is submitted separately on Moodle.

## Running it

Python 3.11. From this folder:

```
python3.11 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter lab A3_bbbp_gnn.ipynb
```

Then run all cells top to bottom. It takes about two and a half minutes on a laptop CPU,
with no GPU needed. The first run needs internet so PyTorch Geometric can download BBBP
into `data/MoleculeNet/`; after that it uses the cached copy.

Start Jupyter from this folder, because all the paths in the notebook are relative to it.
The notebook creates `report/figures/` and `results/` as it runs and writes its figures and
tables there. Both are gitignored, so they appear locally but are not part of the repo.

## Seeds

Seed 42 for the splits and the baseline. Seeds 1, 2 and 3 for the three GNN runs.
Every setting is in the config cell near the top of the notebook, nothing is
hardcoded further down.

## Notebook sections

| Section | What it does |
| --- | --- |
| A | Loads BBBP, checks labels and class balance, canonicalizes the SMILES and removes duplicates and label conflicts. |
| B | Explains the graph format, encodes the categorical columns, batches the graphs and asserts nothing is lost. |
| C | Builds the random and scaffold splits, checks they are disjoint, and measures how close test molecules are to training ones. |
| D | Morgan fingerprints plus logistic regression, with C, class weight and threshold all chosen on validation. |
| E | The GINEConv model, the training loop, and three seeds per split. |
| F | Test metrics for both models under both splits, the curves, the confusion matrices and a bootstrap on the gap. |
| G | The most confident errors, their nearest training molecules, and the limitations. |
