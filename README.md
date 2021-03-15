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
