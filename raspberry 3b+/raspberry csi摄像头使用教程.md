## 参考资料

[树莓派使用CSI摄像头 和 利用mjpg-streamer通过网络使用摄像头](https://blog.csdn.net/lcx1837/article/details/114179304)

## 启用csi摄像头配置

```
sudo raspi-config 
```



## csi摄像头驱动

```
rmmod bcm2835_v4l2
```



## 检测csi摄像头连接是否ok

```
vcgencmd get_camera
```

> supported=1 detected=1, libcamera interfaces=0
>
> [如果detected=0，说明摄像头模块没接好，重新排查下硬件。detected=1则说明CSI摄像头接入正常。supported=1说明摄像头已经使能，摄像头已经可以使用。supported=1则说明CSI摄像头没有使能，需要使能下摄像头模块](https://blog.csdn.net/lcx1837/article/details/114179304)

## 安装mjpg

```shell
sudo apt-get install subversion
sudo apt-get install libjpeg62-turbo-dev
sudo apt-get install imagemagick
sudo apt-get install -y libv4l-dev cmake git

#git clone https://github.com/jacksonliam/mjpg-streamer.git
git clone https://gitee.com/bozen021/mjpg-streamer.git
cd mjpg-streamer/mjpg-streamer-experimental/

vim plugins/input_raspicam/input_raspicam.c
	修改内容：见下面修改点①

make all
sudo make install
```

修改点①：实际不修改也是可以正常访问

```c
diff --git a/mjpg-streamer-experimental/start.sh b/mjpg-streamer-experimental/start.sh
index 65d118c..0cbe1ec 100755
--- a/mjpg-streamer-experimental/start.sh
+++ b/mjpg-streamer-experimental/start.sh
@@ -27,6 +27,7 @@
 export LD_LIBRARY_PATH="$(pwd)"
 #./mjpg_streamer -i "input_uvc.so --help"

+#./mjpg_streamer -i "input_raspicam.so" -o "./output_http.so -w ./www"     //实际不用修改此处
 ./mjpg_streamer -i "./input_uvc.so" -o "./output_http.so -w ./www"
 #./mjpg_streamer -i "./input_uvc.so -n -f 30 -r 1280x960"  -o "./output_http.so -w ./www"
 #./mjpg_streamer -i "./input_uvc.so -n -f 30 -r 640x480 -d /dev/video0"  -o "./output_http.so -w ./www" &
```

## pc端访问

http://192.168.1.100:8080/stream.html

## 多路访问

参考：https://segmentfault.com/a/1190000040009665



## onvif协议IPC开发

### 参考资料：

[ONVIF协议网络摄像机（IPC）客户端程序开发（1）：专栏开篇](https://blog.csdn.net/benkaoya/article/details/72424335)

### ONVIF Device Test Tool工具

下载链接：http://download.csdn.net/detail/benkaoya/9813327

### gsoap2工具

使用迅雷下载：https://sourceforge.net/projects/gsoap2/postdownload

#### 基于raspberry单板进行编译

```shell
#安装依赖包
sudo apt-get install -y openssl flex bison autoconf libssl-dev

#下载gsoap并编译
wget https://udomain.dl.sourceforge.net/project/gsoap2/gsoap_2.8.122.zip
sudo unzip gsoap_2.8.122.zip -d ./
cd gsoap-2.8/
./configure --prefix=/usr/local/gSOAP
make
sudo make install
```

ps：编译时会卡死

#### 使用x86主机进行交叉编译

```shell
cd /mnt/sda4/develop/raspberry/sdk/open_source/gsoap-2.8/deb
scp pi@192.168.1.100:/home/pi/open_source/deb/libssl-dev_1.1.1n-0+deb11u3+rpt1_arm64.deb ./
scp pi@192.168.1.100:/home/pi/open_source/deb/zlib1g-dev_1%3a1.2.11.dfsg-2+deb11u1_arm64.deb ./

dpkg-deb -R libssl-dev_1.1.1n-0+deb11u3+rpt1_arm64.deb libssl-dev_1.1.1n-0+deb11u3+rpt1_arm64
dpkg-deb -R zlib1g-dev_1%3a1.2.11.dfsg-2+deb11u1_arm64.deb zlib1g-dev_1%3a1.2.11.dfsg-2+deb11u1_arm64

cd /mnt/sda4/develop/raspberry/sdk/open_source/gsoap-2.8/
unzip gsoap_2.8.122.zip -d ./
./configure --prefix=/usr/local/gSOAP CC=aarch64-linux-gnu-gcc CFLAGS="-I/mnt/sda4/develop/raspberry/sdk/open_source/gsoap-2.8/deb/libssl-dev_1.1.1n-0+deb11u3+rpt1_arm64/usr/include/ -I/mnt/sda4/develop/raspberry/sdk/open_source/gsoap-2.8/deb/libssl-dev_1.1.1n-0+deb11u3+rpt1_arm64/usr/include/aarch64-linux-gnu/ -I/mnt/sda4/develop/raspberry/sdk/open_source/gsoap-2.8/deb/zlib1g-dev_1%3a1.2.11.dfsg-2+deb11u1_arm64/usr/include/"
make -j8
scp gsoap/src/soapcpp2 pi@192.168.1.100:/home/pi/open_source/gsoap-2.8/deb/
```

说明：gsoap在编译时需要依赖libssl库，为了减少编译依赖库，通过在raspberry环境下载 libssl-dev_1.1.1n-0+deb11u3+rpt1_arm64.deb，而后解压得到相关头文件(*.h)及库(*.so),再在./configure操作时，指定路径即可，操作步骤如下

（在raspberry环境执行）

```shell
cd /home/pi/open_source/gsoap-2.8/deb
apt-get download $(apt-cache depends --recurse --no-recommends --no-suggests --no-conflicts --no-breaks --no-replaces --no-enhances --no-pre-depends libssl-dev | grep -v arm64 | grep "^\w")

apt-get download $(apt-cache depends --recurse --no-recommends --no-suggests --no-conflicts --no-breaks --no-replaces --no-enhances --no-pre-depends zlib1g-dev | grep -v arm64 | grep "^\w")

```

##### 查看gsoap的安装文件

```
sudo dpkg-query -L  gsoap
```



### raspberry下安装v4l2onvif

```shell
#安装依赖包
cd ~/
apt install -y liblivemedia-dev gsoap

sudo apt source gsoap

cp gsoap-2.8.104/gsoap/VisualStudio2005/wsdl2h/wsdl2h/stdsoap2.h /usr/share/gsoap/plugin/stdsoap2.h

cp /usr/include/BasicUsageEnvironment/BasicUsageEnvironment.hh v4l2rtspserver/inc/
cp /usr/include/BasicUsageEnvironment/*.hh v4l2rtspserver/inc/
cp /usr/include/UsageEnvironment/*.hh v4l2rtspserver/inc/
cp /usr/include/liveMedia/*.hh v4l2rtspserver/inc/ -f


apt install -y liblog4cpp5-dev libasound2-dev

cp /usr/include/groupsock/NetCommon.h v4l2rtspserver/inc/ -f
cp /usr/include/groupsock/GroupsockHelper.hh v4l2rtspserver/inc/ -f
cp /usr/include/groupsock/*.hh v4l2rtspserver/inc/ -f

#下载v4l2onvif编译环境
git clone https://github.com/mpromonet/v4l2onvif
cd v4l2onvif
make

#涉及到的仓库
https://gitee.com/fe-mirror/hls.js
```

### ubuntu下安装v4l2onvif

```shell
apt install -y liblivemedia-dev gsoap
apt install -y liblog4cpp5-dev libasound2-dev

#案例一：v4l2onvif编译环境,回退版本，可正常生成目录文件onvif-server.exe和onvif-client.exe
cd /mnt/sda4/develop/onvif/
git clone https://github.com/mpromonet/v4l2onvif
cd v4l2onvif
git reset --hard 6c260c267d3b39e3a81c8fb7fae1cf5c26351142
make onvif-server.exe  -j5
make
./onvif-server.e

#案例二：基于最新版本进行编译 v4l2onvif.latest
cd /mnt/sda4/develop/onvif
git clone https://github.com/mpromonet/v4l2onvif v4l2onvif.latest
cd v4l2onvif.latest

#案例三：拷贝raspberry已下载好的代码
scp -r pi@192.168.1.100:/home/pi/v4l2onvif v4l2onvif.cp_from_raspberry

#使用gitee.com的
cd /mnt/sda4/develop/onvif/v4l2onvif.gitee/
git clone git@gitee.com:yk_rk3399/v4l2onvif.git

scp pi@192.168.1.100:/home/pi/gsoap_2.8.104.orig.tar.gz ./
cd /mnt/sda4/develop/onvif/v4l2onvif.gitee/gsoap/gsoap-2.8.104

```

