# XD-OSLC20
XD-OSLC20: A new Optial-SAR high-resolution dataset for land cover classification spanning 20 different locations, produced by the IPIU Lab at Xidian University.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Data Size](https://img.shields.io/badge/Data%20Size-8.99B%20Pixels-blue)]()
[![Classes](https://img.shields.io/badge/Classes-8-green)]()

## 📖 Introduction

>This is a heads-up about the dataset; the official release date will be announced after the paper is accepted.

Welcome to the official repository of **XD-OSLC20**! This is a large-scale, high-resolution (1m) multimodal remote sensing dataset specifically designed for **Optical-SAR Fusion Land Cover Classification**.

This dataset aims to advance research in heterogeneous remote sensing data fusion and interpretation. By pairing Optical and SAR imagery, it helps overcome the limitations of single-modality sensors, such as cloud interference in optical images and the lack of semantic textures in SAR. The dataset covers 20 typical sample regions across East Asia (China, Japan, South Korea, and North Korea), capturing extremely rich geographical and topographical features.

## ✨ Key Features
* **High-Precision Registration**: Provides strictly aligned Optical and SAR image pairs for multimodal feature learning.
* **Massive Scale**: Contains a total of **8.99 billion** pixels and **15,071** finely annotated objects, satisfying the data demands of large-scale deep learning models.
* **Geographic Diversity**: Spans across 4 countries/regions, encompassing diverse terrains including dense coastal urban areas, inland farmlands, and arid zones, providing an ideal benchmark for cross-regional generalization.
* **Rigorous Spatial Splitting**: The dataset supports strict spatially independent train/validation splits to fundamentally prevent spatial data leakage, ensuring objective model evaluation.
* **Fine-Grained Categories**: Defines 8 typical land cover classes, comprehensively covering both urban and natural scenes.

## 📊 Class Definitions
The dataset includes the following 8 typical land cover categories. To facilitate visualization and ensure consistency across different models, we provide the following color mapping (RGB) for the 8 land cover categories:

| **ID** | **Class Name** | **Chinese Name** | **Color** | **RGB Value**    | **Hex Code** |
| ------ | -------------- | ---------------- | --------- | ---------------- | ------------ |
| 1      | **Water**      | 水体               | 🟦        | `(0, 176, 240)`  | `#00B0F0`    |
| 2      | **Farmland**   | 农田               | 🟨        | `(255, 192, 0)`  | `#FFC000`    |
| 3      | **Forest**     | 森林               | 🟩        | `(0, 176, 80)`   | `#00B050`    |
| 4      | **Grassland**  | 草地               | 🍃        | `(146, 208, 80)` | `#92D050`    |
| 5      | **Road**       | 道路               | ⬛         | `(23, 55, 94)`   | `#17375E`    |
| 6      | **Building**   | 建筑               | 🟥        | `(192, 0, 0)`    | `#C00000`    |
| 7      | **Bare Land**  | 裸地               | 🟫        | `(148, 138, 84)` | `#948A54`    |
| 8      | **Others**     | 其他               | 🌑        | `(0, 0, 0)`      | `#000000`    |

color_map.py be like:
```python
import numpy as np

COLOR_MAP = {
    1: [0, 176, 240],   # Water
    2: [255, 192, 0],   # Farmland
    3: [0, 176, 80],    # Forest
    4: [146, 208, 80],  # Grassland
    5: [23, 55, 94],    # Road
    6: [192, 0, 0],     # Building
    7: [148, 138, 84],  # BareLand
    0: [0, 0, 0]        # Others
}

def visualize_label(label_mask):
    h, w = label_mask.shape
    img = np.zeros((h, w, 3), dtype=np.uint8)
    for i, color in COLOR_MAP.items():
        img[label_mask == i] = color
    return img
```
## 📂 Data Structure
The dataset is organized into opt, sar, and lbl directories, with corresponding .txt files in the list folder to define the data splits. This structure is optimized for standard semantic segmentation pipelines.
```
<Dataset_Name>/
├── opt/             # High-resolution Optical images (.tif / .png)
├── sar/             # Co-registered SAR images (.tif / .png)
├── lbl/             # Land cover ground truth masks
└── list/            # Data split files
    ├── train.txt    # List of filenames for training
    ├── val.txt      # List of filenames for validation
    └── test.txt     # List of filenames for testing
```
