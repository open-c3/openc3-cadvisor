# Docker 容器监控

## 描述

如果您的docker是在机器上启动的，没有容器管理平台。

可以通过这个插件对docker进行监控。


## 使用方式

### 在安装了OpenC3监控Agent的集群上启动openc3-cadvisor镜像
```bash
    docker run \
    --volume=/:/rootfs:ro \
    --volume=/var/run:/var/run:rw \
    --volume=/sys:/sys:ro \
    --volume=/opt/mydan/var/logs/openc3-cadvisor/:/home/work/uploadCadviosrData/log \
    --volume=/var/lib/docker/:/var/lib/docker:ro \
    --volume=/home/docker/containers:/home/docker/containers:ro \
    --publish=65100:65100 \
    --env Interval=60 \
    --env ClusterName=defaultcluster \
    --detach=true \
    --name=openc3-cadvisor \
    --net=host \
    --restart=always \
    openc3/openc3-cadvisor:latest
```

### 在grafana中导入下面的看版

[点击下载grafana看版](/grafana.dashbord.json)
![grafana看版](/grafana.dashbord.png)

### 标签说明
```
可以从grafana看版中看到监控数据可以进行分组。分组维度为 cluster、namespace、task。

因为所有采集的数据，我们会加上5个标签，分别为 cluster、namespace、task、name、id。


标签来源:

id:        docker容器的id
name:      docker容器的name
namespace: 容器的namespace，如果找不到则默认为“default”，
           一般情况下都会有，如果不指定，docker启动的时候会给一个namspace，如 "docker"

cluster:   从启动命令ClusterName指定
task:      把name用“-”切割，第一个字符串就是task
```
