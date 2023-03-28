# 个人网站搭建系列（一）- CentOS 篇
> 本文档介绍了在 CentOS 服务器上快速搭建个人网站的简要流程，主要通过 Docker 这种容器化技术完成。

### 安装 Docker

- 使用 `root` 权限更新 `yum` 包
```
yum -y update
```

- 安装需要的软件包， `yum-util` 提供 `yum-config-manager` 功能，另外两个是 `devicemapper` 驱动依赖的
```
yum install -y yum-utils device-mapper-persistent-data lvm2
```

- 设置 `yum` 源（选择其中一个，国内推荐阿里的）
```
yum-config-manager --add-repo http://download.docker.com/linux/centos/docker-ce.repo（中央仓库）
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo（阿里仓库）
```

- 查看所有仓库中所有 `Docker` 版本，并选择特定版本安装
```
yum list docker-ce --showduplicates | sort -r
```
> 比如我的查询结果如下：
> ```
> docker-ce.x86_64  3:23.0.1-1.el7  docker-ce-stable
> ```

-  使用 `yum install docker-ce-版本号` 安装 `Docker`（期间会有 2 次确认，输入 `y` 回车确认）
```
yum install docker-ce-23.0.1
```

- 启动 `Docker` 并设置开机自启
```
systemctl start docker
systemctl enable docker
```

- 检查是否安装成功
```
docker version
```

- 配置国内镜像源[阿里镜像加速器](https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors)
```
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://zriwtgsj.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

### 安装 Portainer

- 安装 `Portainer`
```
docker run -d -p 9000:9000 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer
```

- 在云服务上配置防火墙策略，开放 `9000` 端口，后续安装的服务请根据需求同样开放对应的端口

### 安装 MySQL 数据库

- 安装 `MySQL`，其中 `my-secret-pw` 是 root 用户的密码，请自行修改
```
docker run --name mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -p 3306:3306 -d mysql
```

### 安装 WordPress

- 安装 `WordPress`
```
docker run --name wordpress --link mysql:mysql -p 8080:80 -d wordpress
```
> 注意：若这里使用了 `link`，则配置 `WordPress` 的数据库主机名时可以直接使用 `mysql`

- 后续如果需要修改数据库连接，可以进入该容器的 `_data` 目录下修改 `wp-config.php` 文件
```
cd /var/lib/docker/volumes/xxx/_data
```