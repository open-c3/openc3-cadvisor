Docker 容器监控
------------------------------------
描述
------------------

如果您的docker是在机器上启动的，没有容器管理平台。

可以通过这个插件对docker进行监控。


使用方式：

-----------------

## 在安装了OpenC3监控Agent的集群上启动openc3-cadvisor镜像
```bash
    docker run \
    --volume=/:/rootfs:ro \
    --volume=/var/run:/var/run:rw \
    --volume=/sys:/sys:ro \
    --volume=/home/work/log/cadvisor/:/home/work/uploadCadviosrData/log \
    --volume=/var/lib/docker/:/var/lib/docker:ro \
    --volume=/home/docker/containers:/home/docker/containers:ro \
    --publish=18080:18080 \
    --env Interval=60 \
    --detach=true \
    --name=micadvisor \
    --net=host \
    --restart=always \
    micadvisor:latest
```

## 在grafana中导入下面的看版

[点击下载grafana看版](/grafana.dashbord.json)
