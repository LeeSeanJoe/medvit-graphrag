# medvit-graphrag

**GraphRAG-Augmented Zero-Shot Localization in Medical Vision Transformers**

Uses knowledge graphs and LLMs to improve zero-shot localization of chest X-ray findings in CLIP-style medical foundation models. Evaluates whether spatially-weighted GraphRAG prompting improves patch-level image-text alignment against radiologist ground truth segmentations.

---

## Project structure

```
medvit-graphrag/
├── 01_knowledge_graphs.ipynb   # Build pathology subgraphs (RadGraph schema)
├── 02_prompt_synthesis.ipynb   # Generate prompts for all 4 conditions via Claude API
├── 03_localization.ipynb       # Patch-text similarity localisation + evaluation
└── README.md
```

All data and results are saved to Google Drive at `$DRIVE_BASE = /content/drive/MyDrive/medvit-graphrag/`.

---

## Experimental conditions

| Condition | Label | Description |
|-----------|-------|-------------|
| A | `flat` | One-line concept label — baseline |
| B | `expanded` | LLM-expanded without graph — controls for prompt length |
| C | `graphrag` | Full graph (spatial + non-spatial edges) → LLM |
| D | `graphrag_spatial` | Spatial edges only → LLM — spatially-weighted GraphRAG |

---

## Datasets

- **CheXpert validation set** (234 images): `danjacobellis/chexpert` on HuggingFace, no gating
- **CheXlocalize** (187 annotated images): radiologist GT segmentations, Stanford AIMI portal

---

## Models

- **BiomedCLIP** (`microsoft/BiomedCLIP-PubMedBERT_256-vit_base_patch16_224`): primary backbone
- **RAD-DINO** (`microsoft/rad-dino`): secondary backbone for replication (notebook 04, WIP)

---

## Setup

1. Open notebooks in Google Colab (GPU runtime recommended)
2. Add `ANTHROPIC_API_KEY` to Colab secrets (🔑 icon) — required for notebook 02 only
3. Run notebooks in order: 01 → 02 → 03

---

## Knowledge graph sources

Graphs are sourced from 19 peer-reviewed radiology references:

**Pleural Effusion**
- Moskowitz et al. AJR 1973: https://ajronline.org/doi/10.2214/ajr.142.1.59
- Radiology Key: https://radiologykey.com/pleural-effusion-2/
- Mercer et al. Breathe (ERS) 2024: https://pmc.ncbi.nlm.nih.gov/articles/PMC10928554/
- Desai et al. RadioGraphics 2023: https://pubs.rsna.org/doi/full/10.1148/rg.230079

**Cardiomegaly**
- Amin & Siddiqui StatPearls 2022: https://www.ncbi.nlm.nih.gov/books/NBK542296/
- Truszkiewicz et al. PMC 2021: https://pmc.ncbi.nlm.nih.gov/articles/PMC8125954/
- NCBI Clinical Methods: https://www.ncbi.nlm.nih.gov/books/NBK355/
- Radiology Key: https://radiologykey.com/recognizing-adult-heart-disease/

**Edema**
- Radiology Masterclass: https://www.radiologymasterclass.co.uk/tutorials/chest/chest_pathology/chest_pathology_page8
- Lichtenstein et al. PMC 2020: https://pmc.ncbi.nlm.nih.gov/articles/PMC7607415/
- Sorin et al. Radiology Advances 2024: https://academic.oup.com/radadv/article/1/1/umae003/7630768
- Ketai & Godwin RadioGraphics 1999: https://pubs.rsna.org/doi/abs/10.1148/radiographics.19.6.g99no211507

**Lung Opacity**
- Radiology Key Basic Patterns: https://radiologykey.com/3-basic-patterns-in-lung-disease/
- StatPearls Lung Imaging 2023: https://www.ncbi.nlm.nih.gov/books/NBK558976/
- EMCrit Consolidation 2023: https://emcrit.org/ibcc/consolidation/
- Radiology Assistant: https://radiologyassistant.nl/chest/chest-x-ray/lung-disease

**Knowledge Graph Schema**
- Jain et al. RadGraph NeurIPS 2021: https://openreview.net/forum?id=pMWtc5NKd7V
- Delbrouck et al. RadGraph-XL ACL 2024: https://physionet.org/content/radgraph-xl/1.0.0/

---

## Citation

If you use this work, please cite:

```
@misc{medvit-graphrag-2026,
  title  = {GraphRAG-Augmented Zero-Shot Localization in Medical Vision Transformers},
  author = {Sean},
  year   = {2026},
  note   = {MIT AI+X PBL Project}
}
```
