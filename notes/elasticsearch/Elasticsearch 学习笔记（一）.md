
## 1 环境准备

- [es & jvm 支持矩阵](https://www.elastic.co/cn/support/matrix#matrix_jvm)
- [spring & es 版本对应](https://docs.spring.io/spring-data/elasticsearch/docs/current/reference/html/#preface.requirements)

### 1.1 使用 Docker 安装 Elasticsearch

``` docker
docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" -v E:\Docker\elasticsearch\config\elasticsearch.yml:/usr/share/elasticsearch/config/elasticsearch.yml -v E:\Docker\elasticsearch\data:/usr/share/elasticsearch/data -v E:\Docker\elasticsearch\plugins:/usr/share/elasticsearch/plugins elasticsearch:7.17.7
```

> Q: Elasticsearch 8.0 报错：received plaintext http traffic on an https channel, closing connection <br>
> A: 修改 elasticsearch.yml，将 `xpack.security.enabled` 设置为 `false`
> ```yml
> xpack.security.enabled: false
> ```

### 1.2 安装 IK 分词器

访问 [elasticsearch-analysis-ik](https://github.com/medcl/elasticsearch-analysis-ik)

``` docker
docker exec -it es bash
./bin/elasticsearch-plugin install https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v7.17.7/elasticsearch-analysis-ik-7.17.7.zip
```

重启 Docker

### 1.3 安装 es-head

``` docker
docker run -d --name elasticsearch-head -p 9100:9100 mobz/elasticsearch-head:5-alpine
```

> 若存在跨域问题，需要在服务端做 CORS 的配置
``` yml
http.cors.enabled: true 
http.cors.allow-origin: "*"
```