# HRI-BloomBench-24: A Bloom's Revised Taxonomy Benchmark for Human-Robot Interaction NLP

[![Dataset](https://img.shields.io/badge/Dataset-HRI--BloomBench--24-blue)](https://github.com/stsbukhari/BloomTaxonomy)
[![License](https://img.shields.io/badge/License-CC%20BY%204.0-green)](LICENSE)
[![IEEE Access](https://img.shields.io/badge/Paper-IEEE%20Access-orange)](https://ieeeaccess.ieee.org/)
[![Sentences](https://img.shields.io/badge/Sentences-204%2C000-purple)]()
[![Classes](https://img.shields.io/badge/Classes-24-red)]()

> **HRI-BloomBench-24** is a large-scale NLP benchmark of 204,000 template-generated sentences for fine-grained cognitive complexity classification in Human-Robot Interaction (HRI) contexts, grounded in Bloom's Revised Taxonomy.

---

## Table of Contents

- [Overview](#overview)
- [Dataset Structure](#dataset-structure)
- [Column Descriptions](#column-descriptions)
- [Label Taxonomy](#label-taxonomy)
- [Statistics](#statistics)
- [Sample Sentences](#sample-sentences)
- [Template ID Format](#template-id-format)
- [Confusable Pair Subset](#confusable-pair-subset)
- [Usage](#usage)
- [Citation](#citation)
- [Authors](#authors)
- [License](#license)

---

## Overview

Classifying the cognitive complexity of natural language instructions in HRI scenarios is essential for context-aware robotic systems. HRI-BloomBench-24 provides a structured, balanced benchmark that maps HRI sentences to **Bloom's Revised Taxonomy** along two axes:

- **Knowledge Dimension (KD):** Factual · Conceptual · Procedural · Metacognitive  
- **Cognitive Process (CP):** Remember · Understand · Apply · Analyze · Evaluate · Create  

The 4 × 6 grid yields **24 fine-grained classification labels**. Every label class contains exactly **8,500 sentences**, ensuring a perfectly balanced benchmark. Sentences are generated from **594 linguistically diverse templates** spanning **71 action verbs**, **35 common HRI tabletop objects**, and **9 spatial positions**, across three difficulty tiers (easy / medium / hard).

This benchmark supports the development and evaluation of NLU models for intelligent HRI systems that must interpret operator instructions at the correct level of cognitive abstraction.

---

## Dataset Structure

The repository contains one primary file:

```
BloomTaxonomy/
└── HRI_BloomBench24_Dataset.csv   # 204,000 sentences, 15 columns (~48 MB)
```

---

## Column Descriptions

| Column | Type | Description |
|---|---|---|
| `id` | int | Unique sentence identifier (1–204,000) |
| `sentence` | str | The HRI natural language sentence |
| `kd` | str | Knowledge Dimension label (`Factual`, `Conceptual`, `Procedural`, `Metacognitive`) |
| `cp` | str | Cognitive Process label (`Remember`, `Understand`, `Apply`, `Analyze`, `Evaluate`, `Create`) |
| `label` | str | Combined class label in the form `KD_CP` (24 unique values) |
| `tier` | str | Difficulty tier (`easy`, `medium`, `hard`) |
| `syntax_form` | str | Sentence construction type (`declarative_imperative`) |
| `verb` | str | Primary action verb used in the sentence (71 unique verbs) |
| `verb_group` | str | Verb + KD combination (e.g., `describe_Factual`) |
| `template_id` | str | Unique template identifier encoding KD, CP, and tier (e.g., `FARE_E01`) |
| `object_name` | str | Target tabletop object (35 unique objects) |
| `kd_frame_id` | str | Internal KD frame identifier used in template construction |
| `spatial_id` | str | Spatial position of the object on the table (9 unique positions) |
| `confusable_pair_id` | str / NaN | Verb-level cross-KD confusable pair label (non-null for 9,000 sentences) |
| `split` | str | Dataset partition (`train` or `test`) |

---

## Label Taxonomy

The benchmark covers the full 4 × 6 Bloom's Revised Taxonomy matrix applied to HRI:

| | **Remember** | **Understand** | **Apply** | **Analyze** | **Evaluate** | **Create** |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| **Factual** | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| **Conceptual** | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| **Procedural** | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| **Metacognitive** | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

Each of the 24 cells contains **8,500 sentences** split across easy, medium, and hard tiers.

---

## Statistics

### Overall

| Property | Value |
|---|---|
| Total sentences | 204,000 |
| Classification labels | 24 |
| Knowledge Dimensions | 4 |
| Cognitive Process levels | 6 |
| Unique action verbs | 71 |
| Unique sentence templates | 594 |
| Unique tabletop objects | 35 |
| Spatial positions | 9 |
| Confusable pair subset | 9,000 sentences |

### Train / Test Split

| Split | Sentences | Percentage |
|---|---|---|
| Train | 165,513 | ~81% |
| Test | 38,487 | ~19% |

### Difficulty Tier Distribution

| Tier | Sentences | Description |
|---|---|---|
| Easy | 48,000 | Short, single-clause, unambiguous verb–object pairings |
| Medium | 120,000 | Moderate syntactic complexity; indirect references |
| Hard | 36,000 | Verb–KD ambiguity; longer constructions; confusable verbs |

### Per Knowledge Dimension

| Knowledge Dimension | Sentences |
|---|---|
| Factual | 51,000 |
| Conceptual | 51,000 |
| Procedural | 51,000 |
| Metacognitive | 51,000 |

### Per Cognitive Process

| Cognitive Process | Sentences |
|---|---|
| Remember | 34,000 |
| Understand | 34,000 |
| Apply | 34,000 |
| Analyze | 34,000 |
| Evaluate | 34,000 |
| Create | 34,000 |

### Tabletop Objects

The following 35 common objects appear in HRI task contexts:

`apple` · `ball` · `banana` · `book` · `bottle` · `bowl` · `box` · `can` · `cloth` · `cup` · `document` · `eraser` · `fork` · `glass` · `jar` · `knife` · `marker` · `mug` · `notebook` · `orange` · `pamphlet` · `pen` · `pencil` · `phone` · `plate` · `remote` · `rubik's cube` · `scissors` · `sponge` · `spoon` · `stapler` · `tablet` · `tape` · `towel` · `toy`

### Spatial Positions

Objects are located at one of 9 canonical table positions:

```
at_the_top-left_of_the_table        at_the_top_of_the_table        at_the_top-right_of_the_table
on_the_left_side_of_the_table       at_the_center_of_the_table     on_the_right_side_of_the_table
at_the_bottom-left_of_the_table     at_the_bottom_of_the_table     at_the_bottom-right_of_the_table
```

---

## Sample Sentences

One representative sentence per Knowledge Dimension × Cognitive Process combination:

| KD | CP | Example Sentence |
|---|---|---|
| Factual | Remember | *Document the robot's record of the orange at the bottom of the table.* |
| Factual | Understand | *Infer the robot's stored information about the pamphlet at the top of the table.* |
| Factual | Apply | *Execute the robot's recorded status for the stapler at the bottom-left of the table.* |
| Factual | Analyze | *Examine the robot's record of the document at the top-right of the table.* |
| Factual | Evaluate | *Score the robot's record of the toy at the center of the table.* |
| Factual | Create | *Design the robot's stored information about the cup at the bottom-right of the table.* |
| Conceptual | Remember | *Document the class of objects the pen at the top of the table represents.* |
| Conceptual | Understand | *Infer how the notebook at the center of the table is grouped with similar objects.* |
| Conceptual | Apply | *Deploy how the robot's system addresses the phone at the bottom-left of the table.* |
| Conceptual | Analyze | *Survey which group the rubik's cube at the top of the table falls under in the robot's object taxonomy.* |
| Conceptual | Evaluate | *Audit the class of objects the stapler at the center of the table represents.* |
| Conceptual | Create | *Derive the class of objects the bottle on the right side of the table represents.* |
| Procedural | Remember | *Locate the robot's planned action for the jar at the top-right of the table.* |
| Procedural | Understand | *Clarify the operational approach for the pamphlet on the right side of the table.* |
| Procedural | Apply | *Demonstrate the technique used to move the sponge at the top-left of the table.* |
| Procedural | Analyze | *Examine the required actions for picking up the eraser on the right side of the table.* |
| Procedural | Evaluate | *Test how the robot's system addresses the stapler at the bottom-left of the table.* |
| Procedural | Create | *Construct the handling method required for the jar at the center of the table.* |
| Metacognitive | Remember | *Name how the robot reflected on its handling of the book at the center of the table.* |
| Metacognitive | Understand | *Describe what the robot considered about its approach to the can on the left side of the table.* |
| Metacognitive | Apply | *Operate how the robot reflected on its handling of the document at the bottom-left of the table.* |
| Metacognitive | Analyze | *Contrast what the robot considered about its approach to the ball at the bottom-left of the table.* |
| Metacognitive | Evaluate | *Audit how the robot reflected on its handling of the remote at the top of the table.* |
| Metacognitive | Create | *Plan what the robot considered about its approach to the book at the bottom-left of the table.* |

---

## Template ID Format

Each `template_id` encodes KD, CP, and difficulty tier in a compact alphanumeric code:

```
FARE_E01
│├┘ │ ├┘
││  │ └── Template number (01–nn)
││  └──── Tier: E=Easy, M=Medium, H=Hard
│└─────── CP code: RE=Remember, UN=Understand, AP=Apply, AN=Analyze, EV=Evaluate, CR=Create
└──────── KD code: FA=Factual, CO=Conceptual, PR=Procedural, ME=Metacognitive
```

**KD codes:** `FA` (Factual) · `CO` (Conceptual) · `PR` (Procedural) · `ME` (Metacognitive)  
**CP codes:** `RE` (Remember) · `UN` (Understand) · `AP` (Apply) · `AN` (Analyze) · `EV` (Evaluate) · `CR` (Create)  
**Tier codes:** `E` (Easy) · `M` (Medium) · `H` (Hard)

Example: `COAN_M10` = **Co**nceptual + **An**alyze, **M**edium tier, template 10.

---

## Confusable Pair Subset

A dedicated evaluation subset of **9,000 sentences** is marked via the `confusable_pair_id` column. These sentences use action verbs that appear across two different Knowledge Dimensions, creating cross-KD classification challenges. There are **24 unique confusable verb–KD pairings**, for example:

| `confusable_pair_id` | Ambiguous Verb | KD Pair |
|---|---|---|
| `find_Conceptual_Factual` | *find* | Conceptual ↔ Factual |
| `describe_Metacognitive_Procedural` | *describe* | Metacognitive ↔ Procedural |
| `test_Factual_Procedural` | *test* | Factual ↔ Procedural |
| `review_Conceptual_Metacognitive` | *review* | Conceptual ↔ Metacognitive |
| `check_Conceptual_Procedural` | *check* | Conceptual ↔ Procedural |
| `validate_Conceptual_Factual` | *validate* | Conceptual ↔ Factual |

Rows where `confusable_pair_id` is `NaN` belong to the standard (non-confusable) portion of the dataset.

---

## Usage

### Loading the Dataset

```python
import pandas as pd

df = pd.read_csv("HRI_BloomBench24_Dataset.csv")
print(df.shape)         # (204000, 15)
print(df['label'].value_counts())
```

### Train / Test Split

```python
train_df = df[df['split'] == 'train']   # 165,513 sentences
test_df  = df[df['split'] == 'test']    #  38,487 sentences
```

### Filtering by Taxonomy Level

```python
# All Procedural sentences
procedural = df[df['kd'] == 'Procedural']

# Analyze-level only
analyze = df[df['cp'] == 'Analyze']

# Specific label
factual_create = df[df['label'] == 'Factual_Create']
```

### Working with Tiers

```python
easy_df   = df[df['tier'] == 'easy']    # 48,000
medium_df = df[df['tier'] == 'medium']  # 120,000
hard_df   = df[df['tier'] == 'hard']    # 36,000
```

### Confusable Pair Evaluation Subset

```python
# All sentences with cross-KD verb ambiguity
confusable = df[df['confusable_pair_id'].notna()]   # 9,000 sentences
print(confusable['confusable_pair_id'].unique())
```

### Quick Baseline with Hugging Face Transformers

```python
from transformers import AutoTokenizer, AutoModelForSequenceClassification
import torch

# Map 24 labels to integers
labels = sorted(df['label'].unique())
label2id = {l: i for i, l in enumerate(labels)}
id2label = {i: l for l, i in label2id.items()}

df['label_id'] = df['label'].map(label2id)
```

---

```

---

## Authors

| Name | Affiliation | Role |
|---|---|---|
| **Dr. Syed Tanweer Shah Bukhari** | Faculty of IT & CS, University of Central Punjab (UCP), Lahore, Pakistan | Principal Investigator |
| **Dr. Manzar Iqbal Malik** | University of Salford, UK | Co-author |
| **Faiqa Yaseen** | University of Central Punjab (UCP), Lahore, Pakistan | Co-author |
| **Prof. Andrew Ware** | University of South Wales, UK | Co-author |

Dr. Bukhari is a Senior Member of IEEE and leads the **Cognitive Robotics Group** at UCP.

---

## License

This dataset is released under the [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/) license. You are free to share and adapt the material for any purpose, provided appropriate credit is given.

---

## Related Work

This benchmark builds on prior work in cognitive robotics and Bloom's Taxonomy-grounded NLP for HRI:

- S. T. S. Bukhari *et al.*, "YOLOv3-Based Object Detection with Bloom's LSTM for HRI Task Classification," *Electronics*, 2021.
- S. T. S. Bukhari *et al.*, "Hierarchical Task Selection for Human-Robot Interaction Using NiHA Architecture," *IROS*, 2023.

---

*For questions, issues, or collaboration inquiries, please open a GitHub Issue or contact the corresponding author.*
