# 个人网站搭建系列（三）- Markdown 篇

> 本文档介绍了快速搭建编写 `Markdown` 的环境，主要实现图床功能，优点在于带图片的 `Markdown` 文档分享，避免找不到本地图片的情况。

## 方案一：OSS + PicGo + Typora

> 此方案比较简单易操作，但 `OSS` 和 `Typora` 都需要收费，`Typora` 大概 90 元买断，阿里的 `OSS` 大概 9 元 /  40GB / 年，如果是白嫖党，可以直接看方案二。

### 购买云存储

- 推荐购买阿里云的 `OSS` 服务，你也可以使用 `Github`等作为图床服务。进入阿里云控制台，搜索`对象存储`，购买之后进入 `Bucket` 列表，新建一个 `Bucket`，需要注意读写权限设置为`公共读`。新建后复制 `KeyId` 和 `KeySecret` 后续需要使用。

  ![image-20230327134340627](https://zoulei-images.oss-cn-chengdu.aliyuncs.com/md_img/image-20230327134340627.png)

### 安装图床工具 PicGo

- 这是官方文档 [PicGo is Here | PicGo](https://picgo.github.io/PicGo-Doc/zh/guide/#picgo-is-here)，可以进入下载，国内推荐使用山东大学的镜像源 [Molunerfinn_PicGo](https://mirrors.sdu.edu.cn/github-release/Molunerfinn_PicGo/)。

- 安装后进入图床设置，选择 `阿里云OSS`，使用刚才复制的 `KeyId` 和 `KeySecret` 。

  ![image-20230327135424816](https://zoulei-images.oss-cn-chengdu.aliyuncs.com/md_img/image-20230327135424816.png)

### 安装 Markdown 编辑器 Typora

- 进入官网下载安装 [Typora 官方中文站 (typoraio.cn)](https://typoraio.cn/)。

- 安装后进入`偏好设置`，配置图片服务器，选择刚才安装的 `PicGo` 路径。

  ![image-20230327135810980](https://zoulei-images.oss-cn-chengdu.aliyuncs.com/md_img/image-20230327135810980.png)

### 结合 WordPress

- 打开 `WordPress`，写文章时直接将 `Typora` 中写好的文档全选复制到文章中即可，图片可以直接预览。

## 方案二：Github + VS Code + PicGo（VS Code 插件）

> 此方案适合白嫖党，无任何花费，只是性能和体验相比较方案一略差一点，但不影响日常使用。

TODO