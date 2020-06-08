Dataloader

- use opencv (`cv2`) to read and process images.

- read from **image** files OR from **.lmdb** for fast IO speed.
    - How to create .lmdb file? Please see [`codes/data_scripts/create_lmdb.py`](../data_scripts/create_lmdb.py).

## How To Prepare Data
1. Prepare the images. You can download DIV2K dataset can be downloaded from [DIV2K offical page](https://data.vision.ee.ethz.ch/cvl/DIV2K/), or from [Baidu Drive](https://pan.baidu.com/s/1LUj90_skqlVw4rjRVeEoiw).

1. We use DIV2K dataset for training. 
    1. since DIV2K images are large, we first crop them to sub images using [`codes/data_scripts/extract_subimages.py`](../data_scripts/extract_subimages.py). 
    1. generate LQ images using matlab with [`codes/data_scripts/generate_2groups.m`](../data_scripts/generate_2groups.m) for CResMD, [`codes/data_scripts/generate_deg.m`](../data_scripts/generate_deg.m) for base network. If you already have LQ images, you can skip this step. Please make sure the LQ and GT folders have the same number of images.
    1. (optional) generate .lmdb file if needed using [`codes/data_scripts/create_lmdb.py`](../data_scripts/create_lmdb.py).
    1. modify configurations in `options/train/xxx.yml` when training, e.g., `dataroot_GT`, `dataroot_LQ`.



4. The same for validation (you can choose some from the test folder) and test folder.

## General Data Process

### data augmentation

We use random crop, random flip/rotation, (random scale) for data augmentation. 
