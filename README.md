# VoxSeT_re  
### 希望通过这个模型尝试一下Waymo数据集  
## 0413:  
1. 配置了环境：  
```
pip install -r requirements.txt
python setup.py build_ext --inplace 
```  
2. 安装了`torch_scatter`;  
3. 使用pcdet的方法准备kitti数据集：  
- 使用命令`python -m pcdet.datasets.kitti.kitti_dataset create_kitti_infos tools/cfgs/dataset_configs/kitti_dataset.yaml`生成数据集的info本质上就是运行`pcdet.datasets.kitti.kitti_dataset.py`脚本，因此kitti数据集的路径不止需要在`ools/cfgs/dataset_configs/kitti_dataset.yaml`该文件的第二行修改，还应该在`pcdet.datasets.kitti.kitti_dataset.py`脚本的main函数中修改；
```
ROOT_DIR = (Path(__file__).resolve().parent / '../../../').resolve()
        create_kitti_infos(
            dataset_cfg=dataset_cfg,
            class_names=['Car', 'Pedestrian', 'Cyclist'],
            data_path=ROOT_DIR / 'data' / 'kitti',
            save_path=ROOT_DIR / 'data' / 'kitti'
        )
```  
4. 数据集准备就绪：  
```
Database Pedestrian: 2207
Database Car: 14357
Database Cyclist: 734
Database Van: 1297
Database Truck: 488
Database Tram: 224
Database Misc: 337
Database Person_sitting: 56
---------------Data preparation Done---------------
```  
5. 测试官方提供的预训练模型`python test.py --cfg_file ./cfgs/kitti_models/voxset.yaml --ckpt /home/xilm/fuxian/VoxSeT/VoxSeT-master/ckpt/checkpoint_epoch_100.pth`  
```
2023-04-13 17:23:49,099   INFO  Car AP@0.70, 0.70, 0.70:
bbox AP:94.9003, 89.9381, 89.2051
bev  AP:90.1572, 88.0972, 86.8397
3d   AP:88.8694, 78.7660, 77.5758
aos  AP:94.87, 89.84, 88.99
Car AP_R40@0.70, 0.70, 0.70:
bbox AP:97.2767, 94.4693, 91.9666
bev  AP:94.0420, 90.2430, 87.8950
3d   AP:91.0222, 82.0140, 79.0486
aos  AP:97.25, 94.34, 91.73
Car AP@0.70, 0.50, 0.50:
bbox AP:94.9003, 89.9381, 89.2051
bev  AP:95.0099, 94.0536, 89.5490
3d   AP:94.9769, 90.0833, 89.4566
aos  AP:94.87, 89.84, 88.99
Car AP_R40@0.70, 0.50, 0.50:
bbox AP:97.2767, 94.4693, 91.9666
bev  AP:97.6013, 96.3001, 94.3429
3d   AP:97.5804, 94.8489, 94.1315
aos  AP:97.25, 94.34, 91.73
Pedestrian AP@0.50, 0.50, 0.50:
bbox AP:73.7829, 70.4956, 68.0514
bev  AP:63.1125, 58.5591, 55.1318
3d   AP:60.2515, 55.5535, 50.1888
aos  AP:67.51, 63.60, 60.86
Pedestrian AP_R40@0.50, 0.50, 0.50:
bbox AP:74.8630, 71.6399, 68.3216
bev  AP:63.4051, 58.2776, 53.9557
3d   AP:59.8142, 54.2357, 49.1996
aos  AP:67.95, 63.99, 60.35
Pedestrian AP@0.50, 0.25, 0.25:
bbox AP:73.7829, 70.4956, 68.0514
bev  AP:80.1824, 76.5899, 73.1859
3d   AP:80.1261, 76.4103, 72.8890
aos  AP:67.51, 63.60, 60.86
Pedestrian AP_R40@0.50, 0.25, 0.25:
bbox AP:74.8630, 71.6399, 68.3216
bev  AP:81.3282, 77.8717, 74.4539
3d   AP:81.2723, 77.6285, 74.2510
aos  AP:67.95, 63.99, 60.35
Cyclist AP@0.50, 0.50, 0.50:
bbox AP:94.0427, 78.9481, 74.5767
bev  AP:85.6768, 71.9008, 67.1551
3d   AP:85.4238, 70.2774, 64.9804
aos  AP:93.69, 78.05, 73.76
Cyclist AP_R40@0.50, 0.50, 0.50:
bbox AP:95.3813, 80.2433, 75.9120
bev  AP:90.0341, 72.0699, 67.6753
3d   AP:89.6957, 70.3786, 65.8911
aos  AP:95.06, 79.31, 74.99
Cyclist AP@0.50, 0.25, 0.25:
bbox AP:94.0427, 78.9481, 74.5767
bev  AP:92.3370, 75.7610, 71.3869
3d   AP:92.3370, 75.7610, 71.3869
aos  AP:93.69, 78.05, 73.76
Cyclist AP_R40@0.50, 0.25, 0.25:
bbox AP:95.3813, 80.2433, 75.9120
bev  AP:93.6741, 76.7814, 72.4608
3d   AP:93.6741, 76.7814, 72.4608
aos  AP:95.06, 79.31, 74.99

2023-04-13 17:23:49,104   INFO  Result is save to /home/xilm/fuxian/VoxSeT/VoxSeT-master/output/cfgs/kitti_models/voxset/default/eval/epoch_100/val/default
2023-04-13 17:23:49,104   INFO  ****************Evaluation done.*****************
```  
