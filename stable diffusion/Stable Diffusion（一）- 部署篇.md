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

这个是使用 CPU 的配置
``` docker
docker pull siutin/stable-diffusion-webui-docker:latest

docker run -it --name stable-diffusion-webui \
  -v /opt/sdw/models:/app/stable-diffusion-webui/models \
  -v /opt/sdw/outputs:/app/stable-diffusion-webui/outputs \
  --rm siutin/stable-diffusion-webui-docker:latest \
  bash webui.sh --skip-torch-cuda-test --precision full --no-half --use-cpu SD GFPGAN BSRGAN ESRGAN SCUNet --all --share
```

# 2 模型

常用下载地址：
- Hugging Face: https://huggingface.co
- Civitai: https://civitai.com ~~（国内无法访问）~~

# 2.1 模型推荐：mdjrny-v4

来自 `prompthero` 的 `openjourney`，实现类似 `midjourney` 的效果，有比较精致的画面。
- 下载地址：https://huggingface.co/prompthero/openjourney/tree/main
- 使用方式：在 prompt 中加上 `mdjrny-v4 style`
- 示例展示：https://prompthero.com/openjourney-prompts?utm_source=huggingface&utm_medium=referral


![00013-1870768007](https://zoulei-images.oss-cn-chengdu.aliyuncs.com/md-images/00013-1870768007.png)
> mdjrny-v4 style, magic spell book sitting on a table in the catacombs, hypermaximalist, insanely detailed and intricate, octane render, unreal engine, 8k, by greg rutkowski and Peter Mohrbacher and magali villeneuve

![00042-2774243862](https://zoulei-images.oss-cn-chengdu.aliyuncs.com/md-images/00042-2774243862.png)
> mdjrny-v4 style a highly detailed matte painting of a man on a hill watching a rocket launch in the distance by studio ghibli, makoto shinkai, by artgerm, by wlop, by greg rutkowski, volumetric lighting, octane render, 4 k resolution, trending on artstation, masterpiece


# 3 关键词

- 关键词数据库：https://stablediffusionweb.com/prompts
- 词缀超市：https://tags.novelai.dev
- 分享社群：https://www.aigodlike.com