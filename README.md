# 使用docker-compose部署packetbeat+es数据库审计


## 准备环境

* Docker
* Docker-compose
* CentOS 7 
* images（确定能拉取外网源，如果不行，请自行安装源elasticsearch:7.14.2、kibana:7.14.2、elastic/packetbeat:7.14.2）
---

## 部署指南

**设置宿主机内核参数**

```
echo vm.max_map_count=655350 >> /etc/sysctl.conf
sysctl -p
```

**启动**

```
mkdir -p /data1/esauditdata && chmod -R 777 /data1/esauditdata
cd dbaudit
docker-compose up -d
```

**访问服务**

```
http://docker-compose-ip:5601
```

<font color=#FF0000 >**密码**</font> 

```
# 默认密码
elastic:elasticdocker
```
<font color=#FF0000 >**清理**</font> 

```
docker-compose down -v 
rm -r /data1/esautditdata && rm -r packetbeat-dbaudit-compose
```

---

## 项目说明

* 目前使用的版本为7.14.2
* 登陆kibana后，先创建“索引模式”，在通过Discover查看
* 根据需求，修改 packetbeat/config/packetbeat.yml 相关模块的port，进行监听
