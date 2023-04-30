# 简介

项目地址：https://github.com/Mikubill/sd-webui-controlnet

# 1 安装 ControlNet 扩展

进入 `Extensions` 选项卡，点击 `Load From`，在搜索框中输入 `sd-webui-controlnet`，点击 `Install` 等待安装完成。
> 如果点击 `Load From` 时出现异常，应该是无法访问 `Github` 导致，推荐安装 `Steam++` 代理加速。

![20230426195846](https://zoulei-images.oss-cn-chengdu.aliyuncs.com/md-images/20230426195846.png)

安装完成后在 `Installed` 选项卡点击 `Apply and restart UI` 重启。

# 2 安装预处理器模型

## 2.1 下载模型

- 原版：https://huggingface.co/lllyasviel/ControlNet/tree/main/models
- 精简版：https://huggingface.co/lllyasviel/ControlNet-v1-1/tree/main

下载完成后放到 `extensions\sd-webui-controlnet\models` 目录下

## 2.2 预处理器与模型对应表

| 预处理名称 | 对应模型 | 模型描述 |
| :-------- | :-------- | :-------- |
| canny | control_canny | 边缘检测，适合原画设计师 |
| depth | control_depth | 深度检测 |
| hed | control_hed | 边缘检测但保留更多细节，适合重新着色和风格化。 |
| mlsd | control_mlsd | 线段识别，识别人物功能极差，非常适合建筑。 |
| normal_map | control_normal | 根据图片生成法线贴图，非常适合CG建模师。 |
| openpose | control_openpose | 提取人物骨骼姿势 |
| openpose_hand | control_openpose | 提取人物+手部骨骼姿势 |
| scribble | control_openpose | 提取黑白稿 |
| fake_scribble | control_scribble | 涂鸦风格提取（很强大的模型） |
| segmentation | control_seg | 语义分割 |

# 3 预处理器使用

## 3.1 Canny

`Canny` 模型的主要功能是提取并生成线稿，通过线稿进行二次绘制。

TODO

## 3.x resample