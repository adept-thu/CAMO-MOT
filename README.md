# CAMO-MOT
This is the official code release of the paper [CAMO-MOT: Combined Appearance-Motion Optimization for 3D Multi-Object Tracking with Camera-LiDAR Fusion](填充网址).

## Overview

TODO

## Model Zoo

The results are evaluated on the validation set of the
KITTI [object tracking dataset](http://www.cvlibs.net/datasets/kitti/eval_tracking.php). 
## Requirement

The code has been tested in the following environment:

- Ubuntu 18.04 
- Python 3.6
- PyTorch 1.7.0
- CUDA Toolkit 11.1

## Installation

1. Install [PyTorch](https://pytorch.org/get-started/locally/) and [CUDA](https://developer.nvidia.com/cuda-toolkit).

2. Install other required Python packages:

```shell
pip install -r requirements.txt
```

3. Build and install the required CUDA modules via PyTorch and the CUDA toolkit:
4. Install COCOAPI:
pip install -U 'git+https://github.com/cocodataset/cocoapi.git#subdirectory=PythonAPI'
5. Compile DCNv2
cd src/lib/model/networks/
git clone https://github.com/CharlesShang/DCNv2
cd DCNv2
./make.sh

## Getting Started

### Dataset preparation

Please download the official KITTI [object tracking dataset](http://www.cvlibs.net/datasets/kitti/eval_tracking.php).

To generate the detection results, please use the following command to reformat the ground truth to
KITTI's [object detection](http://www.cvlibs.net/datasets/kitti/eval_object.php?obj_benchmark=3d) format. You can create
your own data splits by modifying `config/opts.py` file.
You can download the Kitti tracking pose data from [here](https://drive.google.com/drive/folders/1Vw_Mlfy_fJY6u0JiCD-RMb6_m37QAXPQ?usp=sharing), and
you can download the point-rcnn, second-iou and pv-rcnn detections from [here](https://drive.google.com/file/d/1zVWFGwRqF_CBP4DFJJa4nBcu-z6kpF1R/view?usp=sharing).~~~~
```shell
python tools/kitti_converter.py --data_root ${DATA_ROOT}
```

The final dataset organization should be like this (you can have your custom data root):

To run this code, you should organize Kitti tracking dataset as below:
```
# Kitti Tracking Dataset       
└── kitti_tracking
       ├── testing 
       |      ├──calib
       |      |    ├──0000.txt
       |      |    ├──....txt
       |      |    └──0028.txt
       |      ├──image_02
       |      |    ├──0000
       |      |    ├──....
       |      |    └──0028
       |      ├──pose
       |      |    ├──0000
       |      |    |    └──pose.txt
       |      |    ├──....
       |      |    └──0028
       |      |         └──pose.txt
       |      ├──label_02
       |      |    ├──0000.txt
       |      |    ├──....txt
       |      |    └──0028.txt
       |      └──velodyne
       |           ├──0000
       |           ├──....
       |           └──0028      
       └── training # the structure is same as testing set
              ├──calib
              ├──image_02
              ├──pose
              ├──label_02
              └──velodyne 
```
Detections
```
└── point-rcnn
       ├── training
       |      ├──0000
       |      |    ├──000001.txt
       |      |    ├──....txt
       |      |    └──000153.txt
       |      ├──...
       |      └──0020
       └──testing 
```

## Training & Testing

### Training

Finetune the additional link/start-end branches based on a pretrained detection model:

```shell
CUDA_VISIBLE_DEVICES=2,3,5 python train.py tracking --exp_id kitti_train --same_aug --hm_disturb 0.05 --lost_disturb 0.2 --fp_disturb 0.1 --gpus 0,1,2,3  --batch_size 36 --num_workers 16 
--load_model ./weights/model_last.pth
```
### Testing

Evaluate the tracking performance on the validation set:

```shell
python test.py tracking --dataset kitti_tracking  --exp_id kitti_train --dataset_version test --pre_hm --track_thresh 0.4  --batch_size 1 --num_workers 16 --load_model ./weights/model_best_all.pth --max_age 16  --max_prediction_num_for_new_object 5 --init_score 0 --post_score 9 --latency 0 --apperance_thresh 0.01 --motion_thresh 10.5
```
The results should be similar to our entry shown below on the KITTI 2D MOT leaderboard. Note that we only have results for Car and Pedestrian because KITTI 2D MOT benchmark only supports to evaluate these two categories, not including the Cyclist. 

 Category       | HOTA (%) | MOTA (%) | MOTP (%)| MT (%) | ML (%) | IDS | FRAG |  FP  |   FN  
--------------- |:--------:|:--------:|:-------:|:------:|:------:|:---:|:----:|:----:|:-----:
 *Car*          | 79.99    | 90.38    |  85.00  | 84.46  | 7.54   | 30  | 156  | 2337 | 942   
 *Pedestrian*   | 44.77    | 52.48    |  64.50  | 35.40  | 25.77  | 152 | 1133 | 8325 | 2525  
 
## Visualization

Please try the code under `tools/visualization` directory to visualize your 3D object tracking results and make an
impressive video!

## License

`CAMO-MOT` is released under the MIT license.

## Acknowledgement

TODO

## Citation

TODO

