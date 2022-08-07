## apt

```shell
#下载deb包对应s
sudo apt source libssl-dev

#强制重装
sudo apt install --reinstall automake
```

### dpkg

参考教程：

[Debian编包-将编译好的.so库文件和.h头文件编译成deb包](https://blog.csdn.net/Emma_YeNT/article/details/119102561)

```shell
#列出所有安装的包：
dpkg-query -l

#查看软件包安装时安装到系统的文件列表
dpkg-query -L gimp

#实例：查看libssl安装到系统的文件列表
sudo dpkg -l|grep libssl
sudo dpkg-query -L libssl-dev

#step 1)、下载deb包
apt-get download $(apt-cache depends --recurse --no-recommends --no-suggests --no-conflicts --no-breaks --no-replaces --no-enhances --no-pre-depends openssl | grep -v i386 | grep "^\w")

apt-get download $(apt-cache depends --recurse --no-recommends --no-suggests --no-conflicts --no-breaks --no-replaces --no-enhances --no-pre-depends openssl | grep -v arm64 | grep "^\w")

apt-get download $(apt-cache depends --recurse --no-recommends --no-suggests --no-conflicts --no-breaks --no-replaces --no-enhances --no-pre-depends libssl-dev | grep -v arm64 | grep "^\w")

#step 2)、解压deb包
dpkg-deb -R libssl1.0.0_1.0.2g-1ubuntu4.20_amd64.deb libssl1.0.0_1.0.2g-1ubuntu4.20_amd64


sudo apt install debhelper
su
sudo rm gsoap-2.8.28 gsoap_2.8.28-1.debian.tar.xz gsoap_2.8.28-1.dsc gsoap_2.8.28.orig.tar.gz debian -rf
sudo apt source gsoap


```

