# Satellite Image Scene Classification (卫星图像场景分类)

本项目是一个基于深度学习的卫星图像场景分类系统，提供了基于 **TensorFlow (v1)** 和 **Keras** 的两种实现方案，并包含用于图像预处理的 PyQt5 GUI 工具。

## 📋 项目简介

该项目旨在利用卷积神经网络 (CNN) 对遥感卫星图像进行场景分类。项目涵盖了从数据预处理、模型训练到预测的全流程。

主要特点：
- **双框架支持**：
    - `classification/` 目录下提供了基于 TensorFlow (原生 API) 的实现，针对 UC_Merge_LandUse 数据集 (21类)。
    - `keras_train/` 目录下提供了基于 Keras 的实现，针对 NWPU-RESISC45 数据集 (45类)，支持数据增强。
- **图形化预处理工具**：提供基于 PyQt5 的 GUI 界面，方便用户进行图像尺寸统一 (Resize) 和归一化处理。
- **自定义 CNN 模型**：实现了包含卷积层、池化层、Dropout 和全连接层的自定义网络结构。

## 🛠️ 环境依赖

请确保安装以下 Python 库：

- Python 3.x
- TensorFlow (1.x 或 2.x 兼容模式)
- Keras
- OpenCV (`opencv-python`)
- PyQt5
- NumPy
- Matplotlib
- Scikit-learn

安装示例：
```bash
pip install tensorflow keras opencv-python PyQt5 numpy matplotlib scikit-learn
```

## 📂 项目结构

```text
e:\Repository\SatelliteImageSceneClassification/
├── classification/          # TensorFlow 原生实现代码
│   ├── train.py             # 模型训练脚本 (UC_Merge 数据集)
│   ├── dataset.py           # 数据加载与处理
│   ├── predict.py           # 预测脚本
│   └── ...
├── keras_train/             # Keras 训练代码
│   ├── NWPU.py              # NWPU 数据集训练脚本
│   └── ...
├── keras_predict/           # Keras 预测代码
│   ├── NWPU_UI.py           # 带界面的预测脚本
│   └── ...
├── pretreatment/            # 预处理工具
│   ├── resize_main.py       # 图像缩放 GUI
│   ├── uniformization.py    # 图像归一化 GUI
│   └── ...
├── Demo/                    # 演示脚本
├── main.py                  # 预处理工具启动入口
└── README.md                # 项目说明文档
```

## 🚀 使用说明

### 1. 数据预处理
运行根目录下的 `main.py` 启动预处理工具箱：
```bash
python main.py
```
该工具提供两个窗口：
- **Resize Window**: 用于批量修改图片尺寸（如统一调整为 224x224 或 64x64）。
- **Uniformization Window**: 用于图像归一化处理。

### 2. 模型训练

#### 方案 A：TensorFlow 原生实现 (针对 UC_Merge 21类数据)
修改 `classification/train.py` 中的 `train_path` 为你的数据集路径，然后运行：
```bash
python classification/train.py
```
*注意：该脚本使用 TensorFlow v1 语法，TF2 环境下可能需要使用 `tf.compat.v1`。*

#### 方案 B：Keras 实现 (针对 NWPU 45类数据)
修改 `keras_train/NWPU.py` 中的 `train_data_dir` 和 `val_data_dir`，然后运行：
```bash
python keras_train/NWPU.py
```
该脚本利用 `ImageDataGenerator` 进行数据增强（旋转、缩放、翻转），适合大规模数据集训练。

### 3. 模型预测
- Keras 版本预测可参考 `keras_predict/` 目录下的脚本，部分脚本包含 UI 界面支持。

## 📊 数据集说明

项目代码中主要使用了以下两个遥感数据集（需自行下载）：
1.  **UC-Merced Land Use Dataset**: 包含 21 个类别（如农田、飞机、海滩、建筑等）。
2.  **NWPU-RESISC45 Dataset**: 包含 45 个类别，数据量更大，更具挑战性。

## 📝 注意事项
- 代码中的绝对路径（如 `/Users/mac/...`）需要根据你的实际文件存放位置进行修改。
- 图像后缀默认为 `.tif`，如果使用 `.jpg` 或其他格式，请相应修改代码中的文件读取部分。
