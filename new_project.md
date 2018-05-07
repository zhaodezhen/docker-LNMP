* nginx/etc/conf.d/default.conf
```
server {
    listen  86;
    root   /var/www/html/jscomment/public;
    include php.conf;
}
```
* 重启nginx
docker-compose restart nginx