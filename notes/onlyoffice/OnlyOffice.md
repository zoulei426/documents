``` docker
docker run -i -t -d -p 8180:80 -p 8188:443 --restart=always --name onlyoffice-document-server \
    -v /opt/onlyoffice/logs:/var/log/onlyoffice  \
    -v /opt/onlyoffice/data:/var/www/onlyoffice/Data  onlyoffice/documentserver
```