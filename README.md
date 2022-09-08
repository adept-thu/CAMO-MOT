# CAMO-MOT

This is the official code release of the paper [CAMO-MOT: Combined Appearance-Motion Optimization for 3D Multi-Object Tracking with Camera-LiDAR Fusion](https://arxiv.org/abs/2209.02540).

## News

- 2022-09-08.  CAMO-MOT is released on [arXiv](https://arxiv.org/abs/2209.02540):slightly_smiling_face:.
- 2022-08-04.  We rank **first** among all methods on **nuScenes** Dataset for [Tracking](https://www.nuscenes.org/tracking?externalData=all&mapData=all&modalities=Any):blush:. 
- 2022-08-03.  We rank **4th** among all methods on **KITTI** Dataset for [MOT](http://www.cvlibs.net/datasets/kitti/eval_tracking.php):grinning:.

We are still working on writing the documentations and cleaning up the code. And we will release our model on **nuScenes/KITTI** and paper as soon as possible:smiley:.

## Results

### Multi-object tracking(on nuScenes test set)

 Method         | AMOTA    | AMOTP   
--------------- |:--------:|:--------:
 CAMO-MOT       | 0.753    | 0.472
 
 
You can find detailed results on nuScenes **test** set on this [website](https://eval.ai/web/challenges/challenge-page/476/leaderboard/1321).
Or you can view the accuracy trend of MOT algorithms on this [website](https://paperswithcode.com/sota/3d-multi-object-tracking-on-nuscenes)

### Multi-object tracking(on nuScenes val set)

 Tracker        | AMOTA    | AMOTP   
--------------- |:--------:|:--------:
 CAMO-MOT       | 0.763    | 0.527
 
On nuScenes, we use [BEVFusion](https://github.com/mit-han-lab/bevfusion) and [FocalConv](https://github.com/dvlab-research/FocalsConv) as our detectors.

### Multi-object tracking(on KITTI test)

 Category       | HOTA (%) | MOTA (%) | MOTP (%)| MT (%) | ML (%) | IDS | FRAG |  FP  |   FN  
--------------- |:--------:|:--------:|:-------:|:------:|:------:|:---:|:----:|:----:|:-----:
 *Car*          | 79.99    | 90.38    |  85.00  | 84.46  | 7.54   | 30  | 156  | 2337 | 942   
 *Pedestrian*   | 44.77    | 52.48    |  64.50  | 35.40  | 25.77  | 152 | 1133 | 8325 | 2525  
 
You can find detailed results on KITTI **test** set on this [website](http://www.cvlibs.net/datasets/kitti/eval_tracking_detail.php?result=b3be646ab7ac4935ad15cb81cc1e12a6d8db4983). 

### Multi-object tracking(on KITTI val)

 Category       | HOTA (%) | MOTA (%) | IDS |  FP  |   FN  
--------------- |:--------:|:--------:|:---:|:----:|:-----:
 *Car*          | 82.91    | 91.96    | 1   | 302  | 371   
 *Pedestrian*   | 50.99    | 64.75    | 70  | 2240 | 1140  
 
On KITTI, we use [PointGNN](https://github.com/WeijingShi/Point-GNN) as our detector.

## License

`CAMO-MOT` is released under the `MIT` license.

## Acknowledgement

In the detection part, many thanks to the following open-source projects:
- [CenterPoint](https://github.com/tianweiy/CenterPoint)
- [FocalConv](https://github.com/dvlab-research/FocalsConv)
- [BEVFusion](https://github.com/mit-han-lab/bevfusion)
- We especially thank Yukang@yukang2017([FocalConv](https://github.com/dvlab-research/FocalsConv)) for his help.

In the tracking part, many thanks to the following open-source projects:
- [DEFT](https://github.com/MedChaabane/DEFT)
- [EagerMOT](https://github.com/aleksandrkim61/EagerMOT)
- [PC3T](https://github.com/TRI-ML/permatrack)

## Citation
If you find our paper or code useful for you, please consider cite us by:grin::
```
@misc{https://doi.org/10.48550/arxiv.2209.02540,
  doi = {10.48550/ARXIV.2209.02540},
  url = {https://arxiv.org/abs/2209.02540},
  author = {Wang, Li and Zhang, Xinyu and Qin, Wenyuan and Li, Xiaoyu and Yang, Lei and Li, Zhiwei and Zhu, Lei and Wang, Hong and Li, Jun and Liu, Huaping},
  keywords = {Computer Vision and Pattern Recognition (cs.CV), FOS: Computer and information sciences, FOS: Computer and information sciences},
  title = {CAMO-MOT: Combined Appearance-Motion Optimization for 3D Multi-Object Tracking with Camera-LiDAR Fusion},
  publisher = {arXiv},
  year = {2022},
  copyright = {arXiv.org perpetual, non-exclusive license}
}
```

