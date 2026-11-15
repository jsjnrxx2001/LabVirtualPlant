# LabVirtualPlant: image sources and construction provenance

Last checked: 2026-11-15.

## Scope

LabVirtualPlant is a curated collection assembled from existing public images. The source tables describe the upstream image resources identified for its subsets. They do not claim new field acquisition by the maintainers, inclusion of every upstream image, or inheritance of the upstream train/test assignments.

The mappings are supported by original folder and filename inspection and sampled image-content comparisons. The intermediate history from the upstream releases to the locally reorganized folders is not fully recorded. File renaming, resizing, and background processing mean that byte equality with original downloads is not required for image-content correspondence.

## Crop-to-source mapping

| Released crop | Source ID | Original folder or partition | Mapping details |
|---|---|---|---|
| Bottle gourd | S1 | `Orginal_Dataset/Batol_Gourd/` | Healthy and six abnormal categories; released paths retain `Batol_Gourd`. |
| Cashew | S2 | `Crops/Cashew/` | Healthy, leaf miner, and red rust subsets. |
| Maize / Corn | S3; S2 | `dataset/Corn___*`; `Crops/Corn/Maize leaf blight/` | S3 supplies the healthy, gray-leaf-spot, common-rust, and northern-leaf-blight subsets. The released northern-leaf-blight group also includes images matching S2 maize leaf blight. |
| Lemon | S4 | `Original Dataset/` | Healthy Leaf and eight non-healthy condition folders; released filenames were renamed. |
| Papaya | S1 | `Orginal_Dataset/papaya_main_dataset/` | Healthy and six abnormal categories. |
| Tomato | S2 | `Crops/Tomato/` | Healthy, septoria leaf spot, and verticulium wilt subsets. |
| Zucchini | S1 | `Orginal_Dataset/Zucchini_Original/` | Healthy and eight abnormal categories. |

## How the source images were reorganized

1. Select crop and condition subsets from the source image collections and organize them by background appearance. Source dataset names alone do not determine the scene assignment.
2. Retain or normalize crop/condition names into the released directory structure. Inherited spellings are retained where required by the image manifests. Class-level mappings are listed in [class_sources.csv](class_sources.csv).
3. Treat healthy crop categories as ID classes. Treat the selected non-healthy conditions, including disease, insect damage, and nutrient-related abnormalities where present, as OOD categories.
4. Divide the curated healthy pool within each crop into approximately 80% training and 20% testing with seed 1. Assign the selected abnormal pool to OOD evaluation. These are the curated collection's splits; they should not be described as the original providers' official splits.
5. Publish image paths and labels through `train.json`, `test.json`, and `ood.json`. The current release stores healthy test images in `test/` and does not provide a separate validation set. Representative released images are 256 × 256 RGB; the complete history of preprocessing parameters is not available.

## Evidence and reproducibility

- [source_examples.csv](source_examples.csv) gives checked target/upstream image pairs using repository-relative target paths. It is a sample-based record, not a full-image lineage map.
- [class_sources.csv](class_sources.csv) associates released class groups with upstream source IDs. Counts describe the target collection, not a measured allocation between multiple source IDs.
- Original source partitions were reorganized. A target path such as `train/...` or `test/...` need not match its source archive partition.
- The image examples in README figures can be traced separately through [assets/sample_manifest.json](assets/sample_manifest.json).

## Source references

### S1. Agri-Vision4: A Comprehensive Multi-Crop Leaf Disease Dataset of Tomato, Papaya, Zucchini, and Bottle Gourd from Bangladesh

- Creators: Md Masum Billah; Md. Anisur Rahman; Saifuddin Sagor; Sanzida Parvin; Mohammad Shorif Uddin.
- Year: 2026.
- Repository version cited: 1.
- Original resource: [Agri-Vision4: A Comprehensive Multi-Crop Leaf Disease Dataset of Tomato, Papaya, Zucchini, and Bottle Gourd from Bangladesh](https://data.mendeley.com/datasets/8t6k37ztxc/1).
- DOI: [10.17632/8t6k37ztxc.1](https://doi.org/10.17632/8t6k37ztxc.1).
- Provider license reference: CC BY 4.0.

### S2. Multi-Crop Leaf Disease Dataset: Corn, Potato, Rice, Tomato, and Cashew

- Creators: Md Atef Ashab Sifat; Md Sazzad hosen.
- Year: 2025.
- Repository version cited: 1.
- Original resource: [Multi-Crop Leaf Disease Dataset: Corn, Potato, Rice, Tomato, and Cashew](https://data.mendeley.com/datasets/z6jp232g5j/1).
- DOI: [10.17632/z6jp232g5j.1](https://doi.org/10.17632/z6jp232g5j.1).
- Provider license reference: CC BY 4.0.

### S3. Multiple Plant Diseases

- Creators: samareshkumar (Kaggle account).
- Original resource: [Multiple Plant Diseases](https://www.kaggle.com/datasets/samareshkumar/multipleplantdiseases).
- Provider license reference: Consult the original Kaggle dataset terms; no additional license is asserted here..

### S4. Comprehensive Lemon Leaf Disease Dataset for Advanced Detection and Sustainable Agriculture

- Creators: A K M Fazlul Kobir Siam; Prayma Bishshash; Md Asraful Sharker Nirob; Sajib Bin Mamun; Md Assaduzzaman; Sheak Rashed Haider Noori.
- Year: 2024.
- Repository version cited: 1.
- Original resource: [Comprehensive Lemon Leaf Disease Dataset for Advanced Detection and Sustainable Agriculture](https://data.mendeley.com/datasets/44nrn4593f/1).
- DOI: [10.17632/44nrn4593f.1](https://doi.org/10.17632/44nrn4593f.1).
- Provider license reference: CC BY 4.0.

## Downloaded resources versus identified image sources

The preparation workspace also contained [PlantDoc](https://github.com/pratikkayal/PlantDoc-Dataset), [Saon110/bd-crop-vegetable-plant-disease-dataset](https://huggingface.co/datasets/Saon110/bd-crop-vegetable-plant-disease-dataset), and the YOLO-format [Multi-Crop Disease Dataset](https://data.mendeley.com/datasets/6243z8r6t6/1). Their presence in a download folder does not establish that they supplied the released samples. They are not counted as confirmed sources here. In particular, sample-based groundnut matches identify S6 as an upstream image resource; a direct lineage through the YOLO resource has not been established.

## Attribution and reuse

Please cite this curated collection and the relevant original image providers. The source license descriptions above are references to provider declarations, not a new blanket license for all files in this repository. Preserve original attribution and consult the source pages for reuse terms and any third-party content restrictions. Documentation of a candidate source does not resolve its image-level attribution.
