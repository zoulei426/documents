# 个人网站搭建系列（二）- WordPress 篇
> 本文档介绍了 WordPress 的简要配置，以及一些推荐的插件。

### 1 插件推荐

- Akismet 反垃圾评论
> 由千百万人使用，Akismet可能是保护您的站点免受垃圾评论的世界上最好的方式。

- WP Githuber MD
> 一个为 WordPress 网站提供全功能 Markdown 语法的插件。

- Simple Link Directory - Lite
> 管理你的外部链接。

### 2 配置

- ~~开启链接管理，进入主题文件夹下的 `functions.php`，添加以下代码~~
```
add_filter( 'pre_option_link_manager_enabled', '__return_true' );
```