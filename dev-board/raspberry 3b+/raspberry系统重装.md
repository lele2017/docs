## 更新apt为清华源

```shell
sudo cp /etc/apt/sources.list /etc/apt/sources.list.orig
lsb_release -a     //确定所用版本
sudo vim /etc/apt/sources.list
增加内容如下
#默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye main contrib non-free
deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye main contrib non-free
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye-updates main contrib non-free
deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye-updates main contrib non-free
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye-backports main contrib non-free
deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye-backports main contrib non-free
deb https://mirrors.tuna.tsinghua.edu.cn/debian-security bullseye-security main contrib non-free
deb-src https://mirrors.tuna.tsinghua.edu.cn/debian-security bullseye-security main contrib non-free
sudo apt update
```

清华源镜像地址：

https://mirrors.tuna.tsinghua.edu.cn/raspberrypi/dists/

## 安装samba服务

```shell
sudo apt install samba
sudo vim /etc/samba/smb.conf
新增内容：
[root]
   comment = Users profiles
   path = /
   guest ok = yes
   browseable = yes
   create mask = 0600
   directory mask = 0700
   writable = yes
sudo service smbd start
```

## dev-tool安装

```shell
sudo apt install exuberant-ctags
sudo apt install cscope
```

### 创建新用户pi

sudo useradd -mk /home/pi -s /bin/bash pi







