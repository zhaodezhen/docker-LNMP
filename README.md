1. 安装docker
2. 安装docker-compose

## docker加速
* vi /etc/docker/daemon.json
```
{
  "registry-mirrors": ["https://registry.docker-cn.com"]
}
```
* 重启docker服务 service docker restart

## 部署php
* 安装composer镜像
* 使用composer镜像
```
vi ~/.bashrc

composer () {
    tty=
    tty -s && tty=--tty
    docker run \
        $tty \
        --interactive \
        --rm \
        --volume /etc/passwd:/etc/passwd:ro \
        --volume /etc/group:/etc/group:ro \
        --volume $(pwd):/app \
        composer "$@"
}
```

## 运行用户设置 docker容器和物理uid,gid一致 
php www-data:www-data 33:33
mysql mysql:mysql 999:999

ps 安装环境ubantu
开发中遇到的问题

1.up 时端口被占用问题，导致fpm连接mysql失败，up前检查端口 netstat -antup
2.container_linux.go:348、container_linux.go:393  这个错误就比较坑了,让我重装好几次服务,相应的错误有docker不能关闭、nginx不能重启、守护进程丢失、找不到等，google了一大堆，一个正确的都没有，被逼无奈只能找docker对于这个的描述，最后找到问题，内存太小(使用'free -mh'查看内存， 我使用的是google共享服务器)，然后增加内存，大于2G就好，然后重启，OK