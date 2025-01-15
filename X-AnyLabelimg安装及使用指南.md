# X-AnyLabeling

`X-AnyLabeling` 是一款全新的交互式自动标注工具，其基于`AnyLabeling`进行构建和二次开发，在此基础上扩展并支持了许多的模型和功能，并借助`Segment Anything`和`YOLO`等主流模型提供强大的 AI 支持。无须任何复杂配置，下载即用，支持自定义模型，极大提升用户标注效率！

> **AnyLabeling = LabelImg + Labelme + Improved UI + Auto-labeling**

## 特性功能

目前[v2.3.0]([Release X-AnyLabeling v2.3.0 · CVHub520/X-AnyLabeling (github.com)](https://github.com/CVHub520/X-AnyLabeling/releases/tag/v2.3.0))提供以下功能，后期计划加入多模态大模型，满足更广泛的需求：

- 支持多边形、矩形、圆形、直线和点的图像标注。
- 支持文本检测、识别和`KIE`（关键信息提取）标注。
- 支持检测-分类级联模型进行细粒度分类。
- 支持一键人脸和关键点检测功能。
- 支持转换成标准的`COCO-JSON`、`VOC-XML`以及`YOLOv5-TXT`文件格式。
- 支持PaddlePaddle、OpenMMLab、Pytorch-TIMM等主流深度学习框架。
- 提供先进的检测器，包括`YOLOv5`、`YOLOv6`、`YOLOv7`、`YOLOv8`、`YOLOX`以及`DETR`系列模型。

完整的支持models：

Supported models

| Task                              | Model                                                        |
| --------------------------------- | ------------------------------------------------------------ |
| **Image Classification**          | ResNet50, InternImage, YOLOv5-cls, YOLOv8-cls, PULC Person/Vehicle Attribute |
| **Object Detection**              | YOLOv5, YOLOv6, YOLOv7, YOLOv8, YOLOX, YOLO-NAS, DAMO_YOLO, GOLD_YOLO, RT-DETR, RTMDet |
| **Instance Segmentation**         | YOLOv5-seg, YOLOv8-seg                                       |
| **Keypoint Detection**            | RTMPose, DWPose, YOLOv6-face, YOLOv8-pose                    |
| **Oriented Object Detection**     | YOLOv5_obb, YOLOv8_obb                                       |
| **Multi-Object Tracking**         | OC-Sort, ByteTrack                                           |
| **Segment Anything**              | SAM, SAM-HQ, EdgeSAM, MobileSAM, EfficientViT-SAM, Med-SAM2D |
| **Optical Character Recognition** | PPOCRv4                                                      |
| **Land Detection**                | CLRNet                                                       |
| **Image Captioning**              | RAM                                                          |
| **Visual Language Model**         | Grounding-DINO                                               |



## 安装

### 方法一、使用在Windows系统上编译的可执行文件

直接在[release](https://github.com/CVHub520/X-AnyLabeling/releases>)页面下载即可
![image-20240116114310875](assets/image-20240116114310875.png)

![image-20240116114323505](assets/image-20240116114323505.png)

v2.3.0支持Win和Linux的直接可执行文件下载，有CPU和GPU版本。其中GPU版本需要有CUDA 11.6及以上CUDA环境。

### 方法二、使用源码进行编译（暂略）

## 使用

