Dataloader

- use opencv (`cv2`) to read and process images.

- read from **image** files OR from **.lmdb** for fast IO speed.
    - How to create .lmdb file? Please see [`codes/data_scripts/create_lmdb.py`](../data_scripts/create_lmdb.py).

## How To Prepare Data
1. Training: Download DIV2K dataset from [DIV2K offical page](https://data.vision.ee.ethz.ch/cvl/DIV2K/), or from [Baidu Drive](https://pan.baidu.com/s/1LUj90_skqlVw4rjRVeEoiw).
1. Testing: Download LIVE1 dataset and CBSD68 dataset from [Google Drive](https://drive.google.com/drive/folders/1-ye2s6og03jHh5A0cjtINpOUickJEra0?usp=sharing).

1. We use DIV2K dataset for training. 
    1. since DIV2K images are large, we first crop them to sub images using [`codes/data_scripts/extract_subimages.py`](../data_scripts/extract_subimages.py). 
    1. generate LQ images using matlab with [`codes/data_scripts/generate_2groups.m`](../data_scripts/generate_2groups.m) for CResMD, [`codes/data_scripts/generate_deg.m`](../data_scripts/generate_deg.m) for base network. 
    1. (optional) generate .lmdb file if needed using [`codes/data_scripts/create_lmdb.py`](../data_scripts/create_lmdb.py).
    1. modify configurations in `options/train/xxx.yml` when training, e.g., `dataroot_GT`, `dataroot_LQ`.


1. For validation and test folder.
	1. Generate different combinations of degradations using matlab with [`codes/data_scripts/generate_2D_val.m`](codes/data_scripts/generate_2D_val.m).
	1. modify configurations on test dataset in `options/train/xxx.yml` or `options/test/xxx.yml` when training or testing, e.g., `dataroot_GT`, `dataroot_LQ`.

## General Data Process
### data augmentation
We use random crop, random flip/rotation, (random scale) for data augmentation. 
