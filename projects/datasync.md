# 数据同步
> PostgreSQL to Elasticsearch by Flink CDC

### 1 安装 PostgreSQL & PgAdmin4

``` docker
# Linux
docker run -p 15432:80 \
    -e 'PGADMIN_DEFAULT_EMAIL=1815207163@qq.com' \
    -e 'PGADMIN_DEFAULT_PASSWORD=770880po' \
    -e 'PGADMIN_CONFIG_ENHANCED_COOKIE_PROTECTION=True' \
    -e 'PGADMIN_CONFIG_LOGIN_BANNER="Authorised users only!"' \
    -e 'PGADMIN_CONFIG_CONSOLE_LOG_LEVEL=10' \
    -d dpage/pgadmin4:latest

# Windows
docker run --name pgadmin4 -p 15432:80 -e PGADMIN_DEFAULT_EMAIL=1815207163@qq.com -e PGADMIN_DEFAULT_PASSWORD=770880po -d dpage/pgadmin4:latest
```

```
docker pull dpage/pgadmin4:latest
```
