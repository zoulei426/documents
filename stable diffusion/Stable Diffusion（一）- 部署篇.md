# 简介

[Stable Diffusion web UI](https://github.com/AUTOMATIC1111/stable-diffusion-webui) 是一个基于 `Stable Diffusion` 的 UI 界面。

- 基础的“文生图”，“图生图”
- 提供了默认的 CheckPoint 模型 `v1-5-pruned-emaonly`，但推荐根据自己的需求下载对应的模型
- 支持很多插件，比如强大的 `ControlNet`

# 1 环境准备

## 1.1 方案一：Windows 本地部署

1. 下载 [Python 3.10.6](https://www.python.org/downloads/release/python-3106/)，并配置环境变量
2. 克隆 `stable-diffusion-webui` 仓库到本地
``` git
git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git
```
3. 双击运行 `webui-user.bat` 文件，等待自动下载依赖环境和模型，启动成功后访问 http://localhost:7860

> - 如果遇到 `gfpgan`, `clip` 等模块下载时卡住或报错，可以打开 `launch.py` 文件，移动至 232 行左右，在那几个 `https://github.com/xxx` 的地址前面加上 `https://ghproxy.com/` 代理地址，最终效果如下：
![20230405223312](https://zoulei-images.oss-cn-chengdu.aliyuncs.com/md-images/20230405223312.png)
> - 如果下载模型时报错或是中断了，可以直接复制那个模型下载地址到浏览器下载，可以断点续传，或者是直接访问 [Hugging Face](https://huggingface.co) 下载模型，然后放到 `models` 对应的目录下。比如我是下载 `v1-5-pruned-emaonly.safetensors` 时中途中断了，手动下载之后放到 `/models/Stable-diffusion` 目录下即可。

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

这里的模型特指“大模型”，也就是 `CheckPoint`，大小一般在 2~7 GB，常用文件后缀为 `.ckpt` 或 `.safetensors`，两者几乎一样，区别主要在后者无法执行脚本，更加安全。模型文件下载之后需要放到 `\models\Stable-diffusion` 路径下，然后到 UI 左上角点击刷新按钮，就可以在下拉框中选择下载的模型使用了。

常用模型下载地址：
- Hugging Face: https://huggingface.co
- Civitai: https://civitai.com ~~（国内无法访问）~~

## 2.1 模型推荐：mdjrny-v4

来自 `prompthero` 的 `openjourney`，实现类似 `midjourney` 的效果，有比较精致的画面。
- 下载地址：[openjourney](https://huggingface.co/prompthero/openjourney/tree/main)，自行选择下载 `.ckpt` 或者 `.safetensors` 文件
- 使用方式：在 prompt 中加上 `mdjrny-v4 style`
- 示例展示：[prompthero](https://prompthero.com/openjourney-prompts)


![00013-1870768007](https://zoulei-images.oss-cn-chengdu.aliyuncs.com/md-images/00013-1870768007.png)
> mdjrny-v4 style, magic spell book sitting on a table in the catacombs, hypermaximalist, insanely detailed and intricate, octane render, unreal engine, 8k, by greg rutkowski and Peter Mohrbacher and magali villeneuve

![00042-2774243862](https://zoulei-images.oss-cn-chengdu.aliyuncs.com/md-images/00042-2774243862.png)
> mdjrny-v4 style a highly detailed matte painting of a man on a hill watching a rocket launch in the distance by studio ghibli, makoto shinkai, by artgerm, by wlop, by greg rutkowski, volumetric lighting, octane render, 4 k resolution, trending on artstation, masterpiece

## 2.2 模型推荐：Deliberate

一款写实向的模型
- 下载地址：[deliberate](https://huggingface.co/XpucT/Deliberate/tree/main)

## 2.3 模型推荐：tmndMix

一款适合于优美风景的模型
- 下载地址：[tmnd-mix](https://huggingface.co/ckpt/tmnd-mix/tree/main)

![00137-1451192500](https://zoulei-images.oss-cn-chengdu.aliyuncs.com/md-images/00137-1451192500.png)
> masterpiece, best quality, sun, sky,  mountain, forest, grassland, river, overlooking, bridge, wheat field, birds, colored clouds, buildings, paddy field

## 2.4 模型推荐：dreamlike-photoreal

来自 `dreamlike-art` 的超现实风格的模型
- 下载地址：[dreamlike-photoreal-2.0 ](https://huggingface.co/dreamlike-art/dreamlike-photoreal-2.0/tree/main)

![00113-2516665644](https://zoulei-images.oss-cn-chengdu.aliyuncs.com/md-images/00113-2516665644.png)
> 1pikachu, from Monsters inc, cute, pixar, unreal engine, tron, hyper detailed, volumetric lighting, ultra-detailed, light leaks, trending on artstation, sharp focus, intricat

## 2.5 模型推荐 revAnimated

额外搭配一个微缩景观模型 `Miniatureworldstyle` 可以实现比较精致的微缩世界
> `Miniatureworldstyle` 是一种 `LyCORIS` 模型，与 `LoRA` 模型类似，但 `sdWebUI` 没有内置这个类型的模型，需要先下载 `a1111-sd-webui-lycoris` 插件，然后重启应用生效。
>
> 有关 `LoRA`、`LyCORIS` 等模型在下一篇文章详解。

- 下载地址：[revAnimated](https://huggingface.co/hanafuusen2001/ReVAnimated/tree/main)，[Miniatureworldstyle](https://huggingface.co/ygdm123/Miniatureworldstyle/tree/main)

使用方式：
- 在 prompt 中加上 `<lyco:miniatureWorldStyle_v10:0.8>`，建议权重在 0.6-0.9 之间
- 使用 `mini(ttp)` 触发整体效果
- 使用 `miniature`, `lanpscape` 触发模型效果
- 使用容器的名字放在最后，比如 `plate`, `cup`, `bowl` 等可以把微缩城市装进去
- 使用 `isometric` 来触发方块
- 使用类似 `statue of Liberty` 的单词来触发主建筑物，使用 `one man in the bathroom` 这样的词来触发人物场景

![00188-2532553446](https://zoulei-images.oss-cn-chengdu.aliyuncs.com/md-images/00188-2532553446.png)
> mini(ttp), (8k, RAW photo, best quality, ultra-detailed, masterpiece:1.2), (realistic:1.37), Snow-capped mountains with snow, miniature, landscape, in bowl, \<lyco:miniminiatureWorldStyle_v10ature_V1:0.8\>

# 3 提示词

# 3.1 常用提示词参考

常用提高质量的正向提示词：

| 正向提示词 | 描述 |
| :-------- | :--- |
| HDR, UHD, 8K (HDR、UHD、4K、8K和64K) | 提升照片的质量 |
| best quality | 最佳质量 |
| Highly detailed, ultra-detailed | 更多细节 |
| masterpiece | 杰作 |
| realistic, photo-realistic | 真实的 |
| ... | ... |

常用提高质量的反向提示词：

| 反向提示词 | 描述 |
| :-------- | :--- |
| worst quality, low quality, normal quality | 低质量 |
| watermark, signature, text, extra digit | 水印、签名、额外的数字等 |
| deformed, bad anatomy, badly drawn face, extra limb, mutated hands and fingers, malformed limbs, deformed hands | 人物变形 |
| ... | ... |

参考网址：
- [提示词数据库](https://stablediffusionweb.com/prompts)
- [词缀超市](https://tags.novelai.dev)
- [分享社群](https://www.aigodlike.com)
- [词图 Prompt Tool](https://prompttool.com)
- [无界 AI](https://www.wujieai.com/tag-generator)

## 3.2 提示词权重

基本逻辑
- 若是想明确某主体，应当使其生成步骤向前，生成步骤数加大，词缀排序向前，权重提高
> 画面质量 → 主要元素 → 细节
- 若是想明确风格，则风格词缀应当优于内容词缀
> 画面质量 → 风格 → 元素 → 细节

分割符
- 逗号 `,` 用于分割词缀，有一定权重排序功能，逗号前权重高，逗号后权重低，因而建议排序：
> 综述（图像质量+画风+镜头效果+光照效果+主题+构图）<br>
> 主体（人物&对象+姿势+服装+道具）<br>
> 细节（场景+环境+饰品+特征）

组合符
- 冒号 `:` 用于自定义权重数值格式：左圆括号 + 词缀 + 冒号 + 数字 + 右圆括号
- 圆括号 `()` 用于增加 0.1 权重
- 花括号 `{}` 用于增加 0.5 权重
- 方括号 `[]` 用于减少 0.1 权重
- 上诉括号叠加使用可以叠加权重