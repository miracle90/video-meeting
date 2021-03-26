# video-meeting

Flutter、Janus、WebRTC实现多人视频会议

## 一、环境搭建

Ubuntu 18.04 64位 

### 1、Janus服务器搭建

```
apt-get update 

sudo apt-get install git -y

sudo apt-get install aptitude

aptitude install libmicrohttpd-dev libjansson-dev libnice-dev

apt install cmake // 编译libwebsocket使用

wget https://github.com/cisco/libsrtp/archive/v2.2.0.tar.gz

tar xfv v2.2.0.tar.gz

cd libsrtp-2.2.0

apt-get install libssl-dev libevent-dev libpq-dev mysql-client libmysqlclient-dev libhiredis-dev make -y

./configure --prefix=/usr --enable-openssl

make shared_library && sudo make install

// 安装 libwebsockets.tar.gz

scp /Users/lidemba/Downloads/。。。/libwebsockets.tar.gz root@120.79.179.182:/root/sfu

tar -zxvf libwebsockets.tar.gz

cd libwebsockets

mkdir build

cd build

cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr -DCMAKE_C_FLAGS="-fpic" ..

make && sudo make install

cd ~/sfu

// 安装 janus-gateway.tar.gz

scp /Users/lidemba/Downloads/。。。/janus-gateway.tar.gz root@120.79.179.182:/root/sfu

tar -zxvf janus-gateway.tar.gz

cd janus-gateway

sh autogen.sh

// ./configure --prefix=/opt/janus --enable-websockets --disable-docs 报错 => No package 'libconfig' found
// 解决方法
sudo apt-get install libconfig-dev -y
sudo apt-get install gengetopt -y

./configure --prefix=/opt/janus --enable-websockets --disable-docs

make

make install

cd /opt/janus

ls => bin  etc  include  lib  share
```

### 2、nginx服务搭建

```
apt-get install build-essential

apt-get install libtool

apt-get install libpcre3 libpcre3-dev

apt-get install zlib1g-dev

apt-get install openssl

wget http://nginx.org/download/nginx-1.16.1.tar.gz

// 给文件夹添加权限 => chmod 777 certs

tar -zxvf nginx-1.16.1.tar.gz

cd nginx-1.16.1

./configure --prefix=/usr/local/nginx --with-http_ssl_module

make

make install

cd /usr/local/nginx => conf  html  logs  sbin
```

### 3、ssl证书配置

### 4、coturn服务搭建

```
wget https://github.com/coturn/coturn/archive/4.5.1.1.tar.gz

tar -zxvf 4.5.1.1.tar.gz

cd coturn-4.5.1.1

./configure --prefix=/usr/local/coturn

make && make install

cd /usr/local/coturn/etc

# 复制一份
cp turnserver.conf.default turnserver.conf

vim turnserver.conf

# 端口
listening-port=3478
# 服务器外网IP
external-ip=49.232.89.57
# 用户名密码
user=codeboy:helloworld
# 域名
realm=stun.l.supercodeboy.com
```

### 5、ICE测试服务

### 6、Janus Demo配置

```
# nginx 配置

支持https，证书，janus demo目录

# netstat -nptl 查看端口占用情况

# 配置Janus

janus.jcfg.sample => 默认配置（https证书路径，coturn服务配置，stun，turn）

janus.transport.http.jcfg.sample => https配置，进行信令交互（开启https、端口、证书）

janus.transport.websockets.jcfg.sample => websocket服务配置（开启wss，端口，证书）

janus.plugin.videoroom.jcfg => 配置插件

# 启动Janus服务器
nohup /opt/janus/bin/janus >> /var/log/janus.log 2>&1 &
```

## 二、Janus信令系统

* create
* attach
* success
* error
* ack
* event
* message
* trickle
* keepalive
* webrtcup
* media
* slowlink
* hangup

## 三、使用Flutter进行客户端开发

### 1、工程目录介绍
### 2、权限采集

* 安卓
* ios

### 3、依赖安装（flutter_webrtc）

* pod install => 需要安装CocoaPods => 依赖Ruby v2.6.3
* xcode配置

### 4、客户端界面搭建

### 5、janus下事务处理对象

## SFU架构

## Janus流媒体服务

### 核心概念

* ICE
* DTLS
* RTP（实时传输协议 Real-time Transport Protocol或简写RTP）
* RTCP
* SRTP
* SCTP
* SDP（会话描述协议 Session Description Protocol）

### 插件

* VideoRoom
* VideoCall
* TextRoom
* Streaming
* SIP
* AudioRoom

### 数据传输

* HTTP
* websocket
* MQTT
* NanoMsg
* RabbitMq
