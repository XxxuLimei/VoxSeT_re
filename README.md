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
4. 
