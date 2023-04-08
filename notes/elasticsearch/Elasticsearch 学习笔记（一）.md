
## 1 环境准备

- [es & jvm 支持矩阵](https://www.elastic.co/cn/support/matrix#matrix_jvm)
- [spring & es 版本对应](https://docs.spring.io/spring-data/elasticsearch/docs/current/reference/html/#preface.requirements)

由于准备基于 `Spring Boot 2.6.11` 开发，所以考虑 `7.15 - 8.0` 之间的版本，目前最新的中文分词器 `7.x` 的版本是 `7.17.9`，所以最终选择了 `7.17.7` 的版本。
> 本来是准备使用最新的 `8.6.2`，但貌似 `Spring-Data-Elasticearch` 对这个版本的响应的解析有问题。

### 1.1 使用 Docker 安装 Elasticsearch

先创建一个名为 `elastic` 的网络，再安装 `Docker` 包。
``` docker
docker network create elastic
docker run -d --name elasticsearch --net elastic -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" -v E:\Docker\elasticsearch\config\elasticsearch.yml:/usr/share/elasticsearch/config/elasticsearch.yml -v E:\Docker\elasticsearch\data:/usr/share/elasticsearch/data -v E:\Docker\elasticsearch\plugins:/usr/share/elasticsearch/plugins elasticsearch:7.17.7
```

> Q: Elasticsearch 8.x 报错：received plaintext http traffic on an https channel, closing connection <br>
> A: 修改 elasticsearch.yml，将 `xpack.security.enabled` 设置为 `false`
> ```yml
> xpack.security.enabled: false
> ```

### 1.2 安装 IK 分词器

分词器版本必须与 `Elasticsearch` 版本保持一致，可以通过两种方式安装：

- 访问 [elasticsearch-analysis-ik](https://github.com/medcl/elasticsearch-analysis-ik)，下载对应版本，然后解压放到 `plugins` 目录下。
- 进入容器使用命令安装
``` docker
docker exec -it es bash
./bin/elasticsearch-plugin install https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v7.17.7/elasticsearch-analysis-ik-7.17.7.zip
```

> 安装好之后需要重启 `Elasticsearch` 容器

### 1.3 安装 es-head

``` docker
docker run -d --name elasticsearch-head -p 9100:9100 mobz/elasticsearch-head:5-alpine
```

> 若存在跨域问题，需要在服务端做 CORS 的配置
``` yml
http.cors.enabled: true 
http.cors.allow-origin: "*"
```

### 1.4 安装 Kibana

``` docker
docker run -d --name kibana --net elastic --link elasticsearch:elasticsearch -p 5601:5601 -v E:\Docker\kibana\config\kibana.yml:/usr/share/kibana/config/kibana.yml kibana:7.17.7
```

打开 `kibana.yml` 写入如下配置：
> 因为使用了 `link` 连接，所以主机名可以填写 `elasticsearch`
``` yml
server:
  name: kibana
  host: "0"

elasticsearch:
  hosts: 
    - http://elasticsearch:9200

monitoring:
  enabled: true
```
最后访问控制台 http://localhost:5601/app/dev_tools#/console
