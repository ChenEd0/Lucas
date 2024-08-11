---
title: 性能监控（五）
description: docker容器化部署grafana+prometheus
sidebar_position: 6
last_update:
  author: 郑学贤
---

# jmeter数据可视化展示

https://hub.docker.com/  可以从官网查询需要下载的镜像

## prometheus镜像启动

  docker pull prometheus  
  docker run -d --name prometheus --restart=always -p 9091:9090 -e "TZ=Asia/Shanghai" prom/prometheus

### 命令详解：
-d ：后台运行此容器  
--name ：启运容器分配名字prometheus  
--restart=always 服务宕机后，会自动重启  
-e "TZ=Asia/Shanghai" 设置时间为上海时间  
-p ：映射端口，9091端口为宿主机prometheus管理端口，9090是prometheus容器的内部端口  
prom/prometheus：通过这个容器来运行的，本地不存在的话，默认会从docker官方仓库pull下来

### prometheus成功检查

容器部署成功即可现在可以通过浏览器去访问prometheus的管理端了  
浏览器输入：http://180.76.115.65:9091/，看到下图即成功

![](@site/static/img/test_img/2022-08-09-11-07-03.png)


### 添加jmeter监控地址

prometheus.yml配置文件中添加jmeter监控地址

  docker exec -it prometheus sh  
  cd  /etc/prometheus/  
  vi  prometheus.yml

使用vi编辑器修改prometheus.yml的配置文件，添加jmeter的配置监控，此处使用的ip地址是我们jmeter所在服务器的IP地址，端口为固定的9270端口，然后重启容器，我们的prometheus数据库服务器就搭建好了，后续可以通过配置的监控地址，通过jmeter写入测试数据。

![](@site/static/img/test_img/2022-08-09-11-12-12.png)

prometheus.yml 文件添加下面内容

```
  - job_name: "jmeter1"                                                                       
    static_configs:             
      - targets: ["180.76.182.90:9270"]
```
![](@site/static/img/test_img/2022-08-10-11-44-11.png)


## jmeter

注意：必须使用5.2以上版本

jmeter.properties添加prometheus.ip

  prometheus.ip =0.0.0.0

![](@site/static/img/test_img/2022-08-10-11-48-53.png)

下载prometheus的jar包，https://github.com/johrstrom/jmeter-prometheus-plugin/releases

![](@site/static/img/test_img/2022-08-10-20-02-53.png)


添加prometheus监听器

![](@site/static/img/test_img/2022-08-10-20-05-10.png)

![](@site/static/img/test_img/2022-08-10-20-05-44.png)



## grafana

### 下载grafana镜像

  docker pull grafana/grafana

### 启动grafana

  docker run --name grafana -p 3000:3000 -d grafana/grafana


### 打开Grafana

地址：http://ip地址:3000/
例如：http://192.168.0.1:3000/

账号：admin，默认密码：admin，点击Log in



### 新建jmeter-prometheus

点击首页的data  source新建一个jmeter-prometheus的数据源

![image-20220105220220038](@site/static/img/test_img/image-20220105220220038.png)


选中prometheus，进行双击

![](@site/static/img/test_img/2022-08-10-13-40-46.png)


输入name的名称，名称不能重复，否则会报错
配置prometheus的地址，端口默认是8086，grafana和prometheus在同一个服务器，可以用localhost或者具体ip(建议直接用公网ip)

![](@site/static/img/test_img/2022-08-10-13-45-49.png)


其他值保持默认，点击Save & Test（保存和测试）按钮，提示Data source is working（数据源正在工作），表示配置已经好了，点击Back（返回）

![](@site/static/img/test_img/2022-08-10-13-48-02.png)

### 新建jmeter-dashboard

进入 https://grafana.com/grafana/dashboards/?search=jmeter&dataSource=prometheus 该页面选择一个支持prometheus数据源的，进行复制

![](@site/static/img/test_img/2022-08-10-13-58-11.png)

![](@site/static/img/test_img/2022-08-10-13-58-52.png)


回到grafana页面，点击+到点击import,进行导入模板

![image-20220105222403163](@site/static/img/test_img/image-20220105222403163.png)


粘贴模板id（5496模板内容比较齐全），点击load进行加载

![](@site/static/img/test_img/2022-08-10-14-00-24.png)


命名和选择数据源，其他参数保持不变，点击import按钮进行导入

![](@site/static/img/test_img/2022-08-10-14-03-02.png)



配置成功后，刷新grafana的仪表盘页面，可以正常显示数据

![](@site/static/img/test_img/2022-08-10-19-42-49.png)

