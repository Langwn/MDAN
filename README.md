# MDAN: Multimodal Rumor Detection via Multi-perspective Cross-domain Hierarchical Fusion

## Description
This repository contains the implementation of MDAN for multimodal rumor detection on the Weibo and Weibo-21 datasets.

## Dataset Information
This study uses two third-party public datasets: Weibo and Weibo-21. The datasets were not created by the authors of this repository. Please download them from their original public sources and organize them according to the directory structure described below.

### Weibo
- Files used in this project: `train_origin.csv`, `val_origin.csv`, `test_origin.csv`
- Image folders: `data/rumor_images/`, `data/nonrumor_images/`

### Weibo-21
- Files used in this project: `train_datasets.xlsx`, `val_datasets.xlsx`, `test_datasets.xlsx`
- Image folders: `Weibo_21/rumor_images/`, `Weibo_21/nonrumor_images/`

## Directory Structure
An example directory layout is shown below:

```text
MDAN-master/
|-- main_weibo.py
|-- main_weibo21.py
|-- run.py
|-- data_pre.py
|-- weibo21_data_pre.py
|-- clip_data_pre.py
|-- weibo21_clip_data_pre.py
|-- pretrained_model/
|   |-- chinese_roberta_wwm_base_ext_pytorch/
|   `-- w2v/
|-- data/
|   |-- train_origin.csv
|   |-- val_origin.csv
|   |-- test_origin.csv
|   |-- rumor_images/
|   `-- nonrumor_images/
`-- Weibo_21/
    |-- train_datasets.xlsx
    |-- val_datasets.xlsx
    |-- test_datasets.xlsx
    |-- rumor_images/
    `-- nonrumor_images/
```

## Code Information
- `main_weibo.py`: training and evaluation on the Weibo dataset
- `main_weibo21.py`: training and evaluation on the Weibo-21 dataset
- `run.py`: experiment pipeline and dataloader construction
- `data_pre.py`: image preprocessing and cache generation for Weibo
- `weibo21_data_pre.py`: image preprocessing and cache generation for Weibo-21
- `clip_data_pre.py`: CLIP-based cache generation for Weibo
- `weibo21_clip_data_pre.py`: CLIP-based cache generation for Weibo-21
- `MDAN.py`: model training and evaluation logic
- `layers.py`: network components used by the model
- `models_mae.py`: MAE-related modules

## Requirements
The codebase depends on the following software environment and third-party libraries:

- Python 3.8+
- PyTorch >= 1.8
- torchvision >= 0.8
- transformers >= 3.0
- timm 0.3.x
- pandas >= 1.0
- numpy >= 1.19
- Pillow >= 8.0
- scikit-learn >= 0.24
- tqdm >= 4.0
- cn_clip
- positional_encodings
- openpyxl

Notes:
- The exact versions of some third-party libraries used in the original experiments were not fully preserved.
- Based on the codebase, the implementation is most consistent with a PyTorch environment of version 1.8 or later and timm 0.3.x.
- The `openpyxl` package is required for loading the Weibo-21 Excel files.
- The `tqdm` package is required for progress bars during training and evaluation.

## Pretrained Models
The implementation expects local pretrained resources for:
- Chinese RoBERTa
- CLIP
- MAE
- Optional word2vec embeddings

Please place these files under the paths referenced in `main_weibo.py` and `main_weibo21.py`, or modify those paths according to your environment.

## Usage Instructions
1. Download the Weibo and Weibo-21 datasets from their original public sources.
2. Organize the dataset files and image folders according to the directory structure above.
3. Download the pretrained models required for BERT, CLIP, and MAE.
4. Install the required Python dependencies.
5. Run the preprocessing scripts to generate cached `.pkl` files if needed.
6. Run `python main_weibo.py` for Weibo experiments.
7. Run `python main_weibo21.py` for Weibo-21 experiments.

## Methodology
- Text is tokenized with a BERT tokenizer and padded or truncated to the maximum sequence length.
- Images are resized to 256 pixels, center-cropped to 224 x 224, converted to tensors, and normalized.
- For posts with multiple associated images, the first valid readable image is used.
- Preprocessed image tensors are cached into `.pkl` files for faster loading.
- The training configuration includes Adam optimization, early stopping, and dataset-specific loaders.

## Reproducibility Notes
- The implementation contains separate entry points for Weibo and Weibo-21 experiments.
- Random seeds are fixed in the main scripts to improve reproducibility.
- Additional experiment settings such as batch size, learning rate, expert number, and attention heads are specified in the paper and the main scripts.

## Citation
If you use this code, please cite the corresponding paper:

`Wenning Lang, Huanda Wang, Wei Zhou, and Junhao Wen. Multimodal rumor detection via multi-perspective cross-domain hierarchical fusion.`

## License
This code is provided for academic reproducibility only. Please contact the authors for reuse permissions.

## Notes
- The datasets are provided by third-party sources. Users should follow the original dataset licenses and terms of use.
- The authors of this repository do not redistribute the third-party datasets.
