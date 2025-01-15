``` cmd
pip install -r requirements.txt
```

## 3) 下载预训练权重文件

## ![img](./assets/155040763-93c22a27-347c-4e3c-847a-8094621d3f4e.png)

### [Pretrained Checkpoints](https://github.com/ultralytics/yolov5)

| Model                                                        | size (pixels) | mAPval 50-95  | mAPval 50     | Speed CPU b1 (ms) | Speed V100 b1 (ms) | Speed V100 b32 (ms) | params (M) | FLOPs @640 (B) |
| ------------------------------------------------------------ | ------------- | ------------- | ------------- | ----------------- | ------------------ | ------------------- | ---------- | -------------- |
| [YOLOv5n](https://github.com/ultralytics/yolov5/releases/download/v7.0/yolov5n.pt) | 640           | 28.0          | 45.7          | **45**            | **6.3**            | **0.6**             | **1.9**    | **4.5**        |
| [YOLOv5s](https://github.com/ultralytics/yolov5/releases/download/v7.0/yolov5s.pt) | 640           | 37.4          | 56.8          | 98                | 6.4                | 0.9                 | 7.2        | 16.5           |
| [YOLOv5m](https://github.com/ultralytics/yolov5/releases/download/v7.0/yolov5m.pt) | 640           | 45.4          | 64.1          | 224               | 8.2                | 1.7                 | 21.2       | 49.0           |
| [YOLOv5l](https://github.com/ultralytics/yolov5/releases/download/v7.0/yolov5l.pt) | 640           | 49.0          | 67.3          | 430               | 10.1               | 2.7                 | 46.5       | 109.1          |
| [YOLOv5x](https://github.com/ultralytics/yolov5/releases/download/v7.0/yolov5x.pt) | 640           | 50.7          | 68.9          | 766               | 12.1               | 4.8                 | 86.7       | 205.7          |
|                                                              |               |               |               |                   |                    |                     |            |                |
| [YOLOv5n6](https://github.com/ultralytics/yolov5/releases/download/v7.0/yolov5n6.pt) | 1280          | 36.0          | 54.4          | 153               | 8.1                | 2.1                 | 3.2        | 4.6            |
| [YOLOv5s6](https://github.com/ultralytics/yolov5/releases/download/v7.0/yolov5s6.pt) | 1280          | 44.8          | 63.7          | 385               | 8.2                | 3.6                 | 12.6       | 16.8           |
| [YOLOv5m6](https://github.com/ultralytics/yolov5/releases/download/v7.0/yolov5m6.pt) | 1280          | 51.3          | 69.3          | 887               | 11.1               | 6.8                 | 35.7       | 50.0           |
| [YOLOv5l6](https://github.com/ultralytics/yolov5/releases/download/v7.0/yolov5l6.pt) | 1280          | 53.7          | 71.3          | 1784              | 15.8               | 10.5                | 76.8       | 111.4          |
| [YOLOv5x6](https://github.com/ultralytics/yolov5/releases/download/v7.0/yolov5x6.pt) + [TTA](https://docs.ultralytics.com/yolov5/tutorials/test_time_augmentation) | 1280 1536     | 55.0 **55.8** | 72.7 **72.7** | 3136 -            | 26.2 -             | 19.4 -              | 140.7 -    | 209.8 -        |

## 4） 安装测试

测试图片
在yolov5路径下执行

``` cmd
python detect.py --source ./data/images/ --weights weights/yolov5s.pt --conf 0.4
```



## 6训练数据集

#### 1）训练命令

yolov5路径下执行

``` cmd
python train.py --data data/CSGO_Silver.yaml --cfg models/yolov5s-vocBySilver.yaml --weights weights/yolov5s.pt --batch-size 16 --epochs 100
```

#### 2）训练过程可视化

在yolov5路径下执行

``` cmd
tensorboard --logdir=./runs
```

## 7测试训练出的网络模型

#### 1 ）测试图片

在yolov5路径下执行

``` cmd
python detect.py --source $测试图片地址 --weights $训练后的pt权重文件地址 --conf 0.4 
```

#### 2）性能统计

在yolov5路径下执行

``` cmd
python test.py --data $训练使用的yaml文件地址 --weights $ 训练后的pt权重文件地址 --batch-size 16
```

