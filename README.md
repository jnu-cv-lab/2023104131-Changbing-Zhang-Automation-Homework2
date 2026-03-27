# OpenCV 图像处理作业

## 项目简介

本项目使用 OpenCV 库实现了一个简单的 C++ 图像处理程序，完成了以下任务：

1. 读取一张测试图片  
2. 在终端输出图像基本信息（宽度、高度、通道数、数据类型）  
3. 显示原图  
4. 将彩色图转换为灰度图并显示  
5. 保存灰度图为新文件  
6. 访问中心像素值，并裁剪图像左上角区域保存  

## 环境要求

- **操作系统**：Ubuntu 20.04 及以上（或 WSL）  
- **编译器**：g++ 支持 C++11 及以上  
- **依赖库**：OpenCV 4.x 开发包、pkg-config

### 安装依赖

```bash
sudo apt update
sudo apt install build-essential pkg-config libopencv-dev
```

验证安装：

```bash
pkg-config --modversion opencv4   # 应显示版本号，如 4.5.5
g++ --version                     # 应显示 g++ 版本
```

## 文件结构

```
Homework2/
├── exp2.cpp          # 源代码
├── picture.jpg       # 测试图片（可替换）
├── gray_picture.jpg  # 运行后生成的灰度图
├── cropped_picture.jpg # 运行后生成的裁剪区域
└── README.md         # 本文件

运行后：

- 终端会输出图像尺寸、通道数、数据类型、中心像素值等信息。
- 弹出三个窗口分别显示原图、灰度图和裁剪区域。
- 按任意键关闭窗口。
- 当前目录下生成 `gray_picture.jpg` 和 `cropped_picture.jpg`。

## 代码功能详解

### 任务 1：读取图片
使用 `cv::imread()` 读取命令行参数指定的图片，若失败则退出。

### 任务 2：输出基本信息
- `image.cols` / `image.rows`：宽度、高度  
- `image.channels()`：通道数  
- `image.depth()`：数据类型，通过 `switch` 映射为可读字符串

### 任务 3：显示原图
`cv::imshow()` 显示图像窗口，`cv::waitKey(0)` 等待按键。

### 任务 4：灰度转换
`cv::cvtColor(image, grayImage, cv::COLOR_BGR2GRAY)` 将 BGR 彩色图转为灰度图。

### 任务 5：保存灰度图
`cv::imwrite("gray_" + filename, grayImage)` 保存。

### 任务 6：简单操作
- **访问中心像素**：`image.at<cv::Vec3b>(center)` 获取 BGR 值并输出。
- **裁剪左上角区域**：定义矩形区域 `cv::Rect(0, 0, 100, 100)`，用 `image(roi).clone()` 裁剪并保存。
