# 1 环境准备

## 1.1 方案一：Windows 本地部署

> 参考 [Stable Diffusion web UI](https://github.com/AUTOMATIC1111/stable-diffusion-webui)

1. 下载 [Python 3.10.6](https://www.python.org/downloads/release/python-3106/)，并配置环境变量
2. 克隆 `stable-diffusion-webui` 仓库到本地
``` git
git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git
```
3. 双击运行 `webui-user.bat` 文件，等待自动下载依赖环境和模型，启动成功后访问 http://localhost:7860

> 1. 如果遇到 `gfpgan`, `clip` 等模块下载时卡住或报错，可以打开 `launch.py` 文件，移动至 232 行左右，在那几个 `https://github.com/xxx` 的地址前面加上 `https://ghproxy.com/` 代理地址，最终效果如下：
![20230405223312](https://zoulei-images.oss-cn-chengdu.aliyuncs.com/md-images/20230405223312.png)

> 2. 如果下载模型时报错或是中断了，可以直接复制那个模型下载地址到浏览器下载，可以断点续传，或者是直接访问 [Hugging Face](https://huggingface.co) 下载模型，然后放到 `models` 对应的目录下。比如我是下载 `v1-5-pruned-emaonly.safetensors` 时中途中断了，手动下载之后放到 `/models/Stable-diffusion` 目录下即可。

## 1.2 方案二：Docker 部署

TODO