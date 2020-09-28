# CResMD

### Interactive Multi-Dimension Modulation with Dynamic Controllable Residual Learning for Image Restoration [Paper](http://www.ecva.net/papers/eccv_2020/papers_ECCV/papers/123650052.pdf)
By Jingwen He*, [Chao Dong*](https://scholar.google.com.hk/citations?user=OSDCB0UAAAAJ&hl=en), and [Yu Qiao](http://mmlab.siat.ac.cn/yuqiao/) (* indicates equal contribution)

<p align="center"> 
  
  <img src="figures/2D_modulation.png">
  two-dimension modulation
  
</p>

<p align="center">

  <img src="figures/3D_modulation.png">
  three-dimension modulation

</p>

<h2 align="center">
Demo video of two-dimension modulation.
</h2>
<p align="center">
<a href="https://www.youtube.com/watch?v=GHkGOkqf1tU" target="_blank">
<img src="figures/cover.png" >
</a></p>


## Dependencies and Installation

- Python 3 (Recommend to use [Anaconda](https://www.anaconda.com/download/#linux))
- [PyTorch >= 1.0](https://pytorch.org/)
- NVIDIA GPU + [CUDA](https://developer.nvidia.com/cuda-downloads)
- Python packages: `pip install numpy opencv-python lmdb pyyaml`
- TensorBoard:
  - PyTorch >= 1.1: `pip install tb-nightly future`
  - PyTorch == 1.0: `pip install tensorboardX`


## How to Test
- **Prepare the test dataset**
	1. Download LIVE1 dataset and CBSD68 dataset from [Google Drive](https://drive.google.com/drive/folders/1-ye2s6og03jHh5A0cjtINpOUickJEra0?usp=sharing)
	1. Generate LQ images with different combinations of degradations using matlab [`codes/data_scripts/generate_2D_val.m`](codes/data_scripts/generate_2D_val.m), [`codes/data_scripts/generate_3D_val.m`](codes/data_scripts/generate_3D_val.m).

- **Modulation Testing**
	1. (optional) Modify the configuration file [`options/test/modulation_CResMD.yml`](codes/options/test/modulation_CResMD.yml). 
	- `dataroot_GT`, `dataroot_LQ`, `pretrain_model_G`.
	- `cond_init`: The starting point of modulation, usually set to [0, 0].
	- `modulation_dim`: The dimension you would like to modulate.
	- `modulation_stride`: The stride for modulation process, usually set to 0.1.
	1. Run command:
	```c++
	cd codes
	python modulation_CResMD.py -opt options/test/modulation_CResMD.yml
	```

- **Test CResMD**
	1. (optional) Modify the configuration file [`options/test/test_CResMD.yml`](codes/options/test/test_CResMD.yml). 
	- `dataroot_GT`, `dataroot_LQ`
	- `cond_norm` (This paper uses [40, 50] for 2D modulation, [40, 50, 92] for 3D modulation).
	- `mode` (LQGT or LQGT_cond. if it is set to LQGT, you should specify `cond`, which is the degradation levels.)
	1. Run command:
	```c++
	python test.py -opt options/test/test_CResMD.yml
	```

- **Test base network**
	1. Modify the configuration file [`options/test/test_Base.yml`](codes/options/test/test_Base.yml).
	1. Run command:
	```c++
	python test.py -opt options/test/test_Base.yml
	```

## How to Train
- **CResMD**
	1. Prepare datasets, usually the DIV2K dataset. More details are in [`codes/data`](codes/data).
	1. Modify the configuration file [`options/train/train_CResMD.yml`](codes/options/train/train_CResMD.yml)
	- `dataroot_GT`, `dataroot_LQ`
	- `cond_norm` (This paper uses [40, 50] for 2D modulation, [40, 50, 92] for 3D modulation).
	1. Run command:
	```c++
	python train_CResMD.py -opt options/train/train_CResMD.yml
	```

- **base network**
	1. Prepare datasets, usually the DIV2K dataset. More details are in [`codes/data`](codes/data). 
	1. Modify the configuration file [`options/train/train_Base.yml`](codes/options/train/train_Base.yml) 
	1. Run command: 
	```c++
	python train.py -opt options/train/train_Base.yml
	```

## Acknowledgement

- This code is based on [mmsr](https://github.com/open-mmlab/mmsr).
