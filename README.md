# video-meeting

Flutter、Janus、WebRTC实现多人视频会议

## 环境搭建

Ubuntu 18.04 64位

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

# 安装 libwebsockets.tar.gz

scp /Users/lidemba/Downloads/。。。/libwebsockets.tar.gz root@120.79.179.182:/root/sfu




```

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
