# jmeter数据可视化展示

https://hub.docker.com/ 可以从官网查询需要下载的镜像

## 1、influxdb镜像启动

docker pull influxdb  
docker run -d --name influxdb -p 8088:8086 influxdb

### 命令详解：

\-d ：后台运行此容器  
\--name ：启运容器分配名字influxdb  
\-p ：映射端口，8088端口为宿主机infuxdb管理端口，8086是infuxdb容器的内部端口  
influxdb：通过这个容器来运行的，本地不存在的话，默认会从docker官方仓库pull下来

### influxdb成功检查

容器部署成功即可现在可以通过浏览器去访问influxdb的管理端了 浏览器输入：http://180.76.115.65:8088/，看到下图即成功

### 创建用户&组织

点击【get start】 输入用户名、密码、确认密码、org、bucket 点击【load your data】 点击API Tokens，点击Generate API Token（生成Token令牌），点击Read/Write Token（读/写Token） 填写Description（描述）：jmeterTocken，选择Read和Write的桶influxdb，点击Save（保存）

## jmeter

注意：必须使用5.2以上版本 添加后端监听器（ Backend Listener） 在后端监听器实现中选择InfluxdbBackendListenerClient，在influxdbURL中把http://ip:8086/api/v2/write?org=influxdb&bucket=jmeter复制进去并修改为自己的influxdb的ip地址，在application 中输入InfluxDB2，点击添加，在左侧输入influxdbToken，右侧输入的内容为 在InfluxDB中配置的外部读写Token：jmeterToken的值 添加一个http请求，直接get一下https://www.baidu.com就可以从influxdb上面看到数据

## grafana

### 下载grafana镜像

docker pull grafana/grafana

### 启动grafana

docker run --name grafana -p 3000:3000 -d grafana/grafana

### 打开Grafana

地址：http://ip地址:3000/ 例如：http://192.168.0.1:3000/ 账号：admin，默认密码：admin，点击Log in

### 新建jmeter-influxDB

点击首页的data source新建一个jmeter-influxdb的数据源 ![image-20220105220220038](../images/image-20220105220220038.png) 选中influxdb，进行双击 ![image-20220105220417911](../images/image-20220105220417911.png) 配置influxdb的地址，端口默认是8086，grafana和influxdb在同一个服务器，可以用localhost或者具体ip 在Custom HTTP Headers（自定义HTTP头）栏，点击+Add header，Header输入：Authorization， Value：Token 5Cd3xuxJ4tnoH\_weYtO88wBGI36EflLonCgko5i1waz8a6BmxLueTVlI83HJEDcOBoyRMbBs\_LZlI\_Tv1ZNZww Value的值为：Token +空格+InfluxDB 的Data-API Tokens中配置的外部访问jmeterToken的值 输入数据库、用户名和密码

点击Save & Test（保存和测试）按钮，提示Data source is working（数据源正在工作），表示配置已经好了，点击Back（返回）

### 新建jmeter-dashboard

进入 https://grafana.com/grafana/dashboards 该页面进行搜索jmeter可以找到很多jmeter的dashboard模板，选择一个支持influxdb数据源的，进行复制 回到grafana页面，点击+到点击import,进行导入模板 粘贴模板id（5496模板内容比较齐全），点击load进行加载 命名和选择数据源，其他参数保持不变，点击import按钮进行导入

## 映射jmeter的buckets到database

InfluxDB2.0升级，使用新方式查询数据，不直接支持2.0之前的版本查询，而dashboard模板使用的还是旧方式查询，如果不进行新旧版本映射，则dashboard无法显示数据。 在postman或者接口请求工具中，请求http://your\_ip:8086/api/v2/dbrps 这个接口,请求办法为post 请求头为： Authorization: Token YourAuthToken Content-type: application/json body内容： { "bucketID": "dfec69ab18f8ac9c", "database": "jmeter", "default": true, "orgID": "7ad6a0648eaed150", "retention\_policy": "example-rp" } bucketID：桶的ID。位置在InfluxDB --> Data --> Buckets database：数据库名称，也就是桶的名称,也就是bucket的名称jmeter orgID：组织的ID，在InfluxDB的地址栏查看 请求成功 配置成功后，刷新grafana的仪表盘页面，可以正常显示数据
