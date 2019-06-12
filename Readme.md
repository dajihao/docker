# docker

## 部署

```
cd /mnt/hgfs/docker/compose
docker-compose up -d --build

修改nginx
docker restart nginx
```

## docker安装

```
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
                  
sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
  
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
    
    
sudo yum install docker-ce docker-ce-cli containerd.io

sudo yum install docker-ce

sudo systemctl start docker

sudo docker run hello-world
```

## docker卸载

```
sudo yum remove docker-ce

sudo rm -rf /var/lib/docker
```

## docker-compose安装

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose
```

## docker-compose卸载

```
sudo rm /usr/local/bin/docker-compose
```

## docker国内镜像

```
修改 daemon 配置文件/etc/docker/daemon.json来使用加速器

(1)创建/etc/docker目录(如果不存在的话)

sudo mkdir -p /etc/docker

(2)修改配置文件/etc/docker/daemon.json

[阿里云]：

// 文件位置: /etc/docker/daemon.json
{
  "registry-mirrors": ["https://y0qd3iq.mirror.aliyuncs.com"]
}
[docker 中文站]：

// 文件位置: /etc/docker/daemon.json
{
  "registry-mirrors": ["https://registry.docker-cn.com"]
}
3.重载守护进程文件，重启 docker

sudo systemctl daemon-reload
sudo systemctl restart docker
4.查看加速器是否生效

[root@txyun ~]# docker info
...
Registry Mirrors:
 https://y0qd36iq.mirror.aliyuncs.com
...

```

## 开机启动

```
开机启动docker
systemctl enable docker

开机启动容器
docker update --restart=always myphp
```