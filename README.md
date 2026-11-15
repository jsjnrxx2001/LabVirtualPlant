# LabVirtualPlant

**A curated multi-crop leaf image dataset for healthy-reference anomaly detection.**

[7 crops](#3-dataset-statistics) · [35 abnormal categories](#4-abnormal-categories) · [11,008 image entries](#3-dataset-statistics) · [Download](#7-download-and-use) · [Companion dataset](https://github.com/jsjnrxx2001/RealworldPlant)

![Healthy and abnormal leaf examples](assets/samples.jpg)

*Figure 1. Representative samples from LabVirtualPlant. Each column shows one crop: a healthy leaf above and an abnormal leaf below. Category labels are inherited from the released dataset.*

## 1. Keywords

Plant leaf images; multi-crop dataset; anomaly detection; out-of-distribution detection; healthy reference samples; few-shot evaluation.

## 2. Dataset description and construction

LabVirtualPlant is a curated image collection for studying plant leaf anomaly detection with healthy reference samples. It covers bottle gourd, cashew, corn, lemon, papaya, tomato, zucchini, with **7 healthy crop categories** and **35 abnormal categories**. Images were selected and reorganized from public plant-image resources, with source links listed below.

The scene grouping is based on **the visual cleanliness of the image background**. This collection emphasizes relatively clean backgrounds and visually isolated leaf subjects. Its companion [RealworldPlant](https://github.com/jsjnrxx2001/RealworldPlant) supports evaluation under the complementary background condition. These names describe the curated image appearance rather than a standardized capture device or acquisition location.

The construction procedure organizes images by crop and original health-condition label, assigns healthy crop categories integer ID labels, and places selected non-healthy conditions in the OOD evaluation pool. Abnormal conditions include disease symptoms and, where present, insect damage, dry leaves, or nutrient-related abnormalities. Representative images in the current release are 256 × 256 RGB images.

The dataset provides a healthy training pool and an evaluation set containing both healthy and abnormal images. In a few-shot setting, the training pool supplies healthy references; the anomaly-detection task is to distinguish these healthy ID samples from abnormal OOD samples.

## 3. Dataset statistics

| Item | Number |
|---|---:|
| Healthy crop categories | 7 |
| Abnormal categories | 35 |
| Healthy training-pool images | 1,897 |
| Healthy test images | 475 |
| Abnormal test images | 8,636 |
| Combined test images | 9,111 |
| Total image entries | 11,008 |

![Image distribution across crops](assets/distribution.png)

*Figure 2. Image counts by crop and evaluation role, computed from the released JSON manifests. The healthy holdout is counted once.*

| Crop | Healthy train | Healthy test | Abnormal test | Abnormal categories |
|---|---:|---:|---:|---:|
| Bottle gourd | 208 | 52 | 1,398 | 6 |
| Cashew | 237 | 59 | 526 | 2 |
| Corn | 741 | 185 | 2,924 | 3 |
| Lemon | 168 | 42 | 119 | 8 |
| Papaya | 151 | 38 | 1,495 | 6 |
| Tomato | 322 | 81 | 1,274 | 2 |
| Zucchini | 70 | 18 | 900 | 8 |

## 4. Abnormal categories

![Examples of every abnormal category](assets/abnormal_categories.jpg)

*Figure 3. One released image from every abnormal category. These examples illustrate the repository labels; they are not additional diagnostic annotations. Figure-to-image mappings are recorded in [sample_manifest.json](assets/sample_manifest.json).*

<details>
<summary>Expand the complete abnormal-category inventory</summary>

| Category folder | Images |
|---|---:|
| `Batol_Gourd_Alternaria_Leaf_Blight` | 303 |
| `Batol_Gourd_Anthracnose` | 276 |
| `Batol_Gourd_Downy_Mildew` | 286 |
| `Batol_Gourd_Early_Alternaria_Leaf_Blight` | 179 |
| `Batol_Gourd_Fungal_Damage_Leaf` | 39 |
| `Batol_Gourd_Mosaic_Virus` | 315 |
| `Cashew_leaf_miner` | 327 |
| `Cashew_red_rust` | 199 |
| `Corn_Cercospora_leaf_spot_Gray_leaf_spot` | 513 |
| `Corn_Common_rust` | 1,192 |
| `Corn_Northern_Leaf_Blight` | 1,219 |
| `Lemon_anthracnose` | 10 |
| `Lemon_bacterial_blight` | 11 |
| `Lemon_citrus_canker` | 19 |
| `Lemon_curl_virus` | 12 |
| `Lemon_deficiency` | 20 |
| `Lemon_dry_leaf` | 19 |
| `Lemon_sooty_mould` | 16 |
| `Lemon_spider_mites` | 12 |
| `Papaya_Bacterial_Blight` | 183 |
| `Papaya_Carica_Insect_Hole` | 318 |
| `Papaya_Curled_Yellow_Spot` | 538 |
| `Papaya_Mosaic_Virus` | 119 |
| `Papaya_Pathogen_symptoms` | 286 |
| `Papaya_Yellow_Necrotic_Spots_Holes` | 51 |
| `Tomato_septoria_leaf_spot` | 601 |
| `Tomato_verticulium_wilt` | 673 |
| `Zucchini_Angular_Leaf_Spot` | 120 |
| `Zucchini_Anthracnose` | 129 |
| `Zucchini_Downy_Midew` | 153 |
| `Zucchini_Dry_Leaf` | 67 |
| `Zucchini_Insect_Damage` | 78 |
| `Zucchini_Iron_Chlorosis_Damage` | 65 |
| `Zucchini_Xanthomonas_Leaf_Spot` | 86 |
| `Zucchini_Yellow_Mosaic_Virus` | 202 |

</details>

## 5. Data partition and label format

Healthy images are split **within each crop category** into approximately 80% training-pool samples and 20% held-out samples, using random seed **1**. The per-class holdout size is `round(0.2 * class_size)`. The selected abnormal images are assigned to OOD evaluation.

| File | Contents |
|---|---|
| `train.json` | Relative image paths mapped to integer healthy-class labels |
| `test.json` | Healthy holdout paths mapped to the same integer labels |
| `ood.json` | Abnormal image paths mapped to the string `"ood"` |
| `classnames.txt` | Healthy-class names and text descriptions |
| `summary.json` | Construction-time summary; its absolute paths describe the original preparation machine |
| `split_fewshot.bak/` | Existing healthy-reference selections for different shots and seeds |

Healthy test images are stored under `test/` and indexed by `test.json`. This release contains a healthy training pool, a healthy test set, and an abnormal test set. No separate validation set is provided. Few-shot files use seeds **1, 2, and 3**, with **2, 4, 8, and 16** samples per healthy category; files named with `shot_4096` represent the full training pool, capped by the available class size.

Original directory spellings are retained for compatibility with the manifests. In particular, `Batol_Gourd` denotes bottle gourd, `Corn`/`Maize` refer to maize, and `Patato` in some abnormal folders denotes potato. Use the released paths verbatim when loading files.

## 6. Repository structure

```text
LabVirtualPlant/
├── README.md
├── assets/                    # Documentation figures and image mappings
├── train/<crop>_healthy/      # Healthy training images
├── test/<crop>_healthy/       # Healthy test images
├── ood_<crop>/<condition>/    # Abnormal evaluation images
├── train.json
├── test.json
├── ood.json
├── classnames.txt
├── summary.json
└── split_fewshot.bak/
```

## 7. Download and use

Clone the image repository:

```bash
git clone https://github.com/jsjnrxx2001/LabVirtualPlant.git
```

Alternatively, select **Code → Download ZIP** on GitHub. The image folders are part of this repository.

The JSON files can be read with standard Python. The following example loads one healthy reference image using Pillow (`pip install pillow`):

```python
import json
from pathlib import Path
from PIL import Image

root = Path("LabVirtualPlant")
with (root / "train.json").open(encoding="utf-8") as f:
    train = json.load(f)

relative_path, class_id = next(iter(train.items()))
image = Image.open(root / relative_path).convert("RGB")
print(relative_path, class_id, image.size)

with (root / "ood.json").open(encoding="utf-8") as f:
    abnormal = json.load(f)
print("Healthy references:", len(train))
print("Abnormal evaluation images:", len(abnormal))
```

## 8. Image sources and acknowledgments

We acknowledge the providers of the original image collections. The links below document the source resources identified for the corresponding subsets; they do not imply that every image in each original dataset is included here.

- [Agri-Vision4](https://data.mendeley.com/datasets/8t6k37ztxc/1) — Bottle gourd, papaya, and zucchini.
- [Multi-Crop Leaf Disease Dataset: Corn, Potato, Rice, Tomato, and Cashew](https://data.mendeley.com/datasets/z6jp232g5j/1) — Cashew, tomato, and a subset of maize leaf-blight images.
- [Multiple Plant Diseases](https://www.kaggle.com/datasets/samareshkumar/multipleplantdiseases) — Maize subsets.
- [Comprehensive Lemon Leaf Disease Dataset](https://data.mendeley.com/datasets/44nrn4593f/1) — Lemon subsets.

## 9. Citation

Please cite this dataset repository and the original image sources relevant to your work. A repository citation can be recorded as:

```bibtex
@misc{labvirtualplant_dataset,
  title = {LabVirtualPlant},
  howpublished = {\url{https://github.com/jsjnrxx2001/LabVirtualPlant}},
  year = {2026},
  note = {Curated plant leaf anomaly detection dataset}
}
```

For reproducible experiments, also record the commit used to obtain the images and split files.

## 10. License and usage

Original images remain subject to the licenses, terms of use, attribution requirements, and citation requirements of their respective providers. The source references above should be consulted before reuse or redistribution. This README does not replace those upstream terms or assign a single new license to all images.

Questions about this collection can be raised through [GitHub Issues](https://github.com/jsjnrxx2001/LabVirtualPlant/issues).
