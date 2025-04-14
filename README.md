# 文档篡改智能检测系统（基于YOLO优化）

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![PyTorch](https://img.shields.io/badge/PyTorch-1.12%2B-orange)
![YOLOv8](https://img.shields.io/badge/YOLO-v8-ff69b4)
![License](https://img.shields.io/badge/License-MIT-green)

## 项目概述
本项目基于Ultralytics YOLO框架，针对文档篡改检测场景进行深度优化，通过改进模型结构、训练策略和数据处理流程，实现高精度的文档篡改区域检测。

## 核心技术
1. **模型架构**
   - 改进YOLOv8的Backbone网络，增加局部注意力模块
   - 优化检测头结构，提升小目标检测能力
   - 采用轻量化设计，模型体积减少47%

2. **训练优化**
   - 使用Focal-EIoU Loss解决样本不平衡问题
   - 实现动态学习率调度（CosineAnnealing+Warmup）
   - 迁移学习+领域自适应训练策略

3. **数据处理**
   - 文档专用数据增强：
     - 局部区域擦除
     - 文本仿射变换
     - 色彩空间扰动
   - 智能标注清洗工具

## 项目结构
├── configs/            # 训练配置文件
├── data/               # 数据预处理脚本
├── models/             # 自定义模型实现
├── tools/              # 实用工具
│   ├── export_onnx.py  
│   └── visualize.py    
├── train.py            # 主训练入口
└── requirements.txt    # 依赖列表

## 快速开始
1. 安装依赖：
pip install -r requirements.txt

2. 准备数据：
python data/prepare_dataset.py --input_dir your_data

3. 开始训练：
python train.py --config configs/custom_yolo.yaml

4. 模型导出：
python tools/export_onnx.py --weights best.pt

## 性能表现
| 指标          | 优化前 | 优化后 |
|---------------|--------|--------|
| mAP@0.5       | 0.68   | 0.83   |
| 推理速度(FPS) | 38     | 55     |
| 模型大小(MB)  | 182    | 96     |

## 贡献指南
欢迎通过Issue或PR提交改进方案，需包含：
1. 问题描述
2. 修改方案
3. 验证结果

## 许可证
MIT License © 2023 [YourName]
