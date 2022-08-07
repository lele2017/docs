

```
sudo apt install debmake

mkdir dpkg
mv gsoap_2.8.28.orig.tar.gz dpkg/
debmake -a gsoap_2.8.28.orig.tar.gz


cd /mnt/sda4/develop/onvif/dpkg/openssl
sudo apt source openssl
mv openssl-1.0.2g/ openssl-1.0.2g-
tar xzf openssl_1.0.2g.orig.tar.gz
tar xf openssl_1.0.2g-1ubuntu4.20.debian.tar.xz
cd debian/


#新旧补丁制作
sudo apt install dpatch
sudo apt install libtool

debuild -us -uc

#openssl重新源码编译

//此处默认下载就已有打patch
rm -rf ./*;apt source openssl
tar xf openssl_1.0.2g-1ubuntu4.20.debian.tar.xz

dpkg-source -x openssl_1.0.2g-1ubuntu4.20.dsc
dpkg-buildpackage -us -uc


vim debian/patches/CVE-2018-0739.patch
\\192.168.1.102\mnt\sda4\develop\onvif\dpkg\openssl\openssl-1.0.2g\crypto\asn1\asn1.h
此patch增加内容为1378 行
# define ASN1_R_NESTED_TOO_DEEP                           219

sudo cp /usr/bin/automake-1.15 /usr/bin/automake-1.14

cd /mnt/sda4/develop/onvif/dpkg/gsoap/gsoap-2.8.28
./configure --prefix=/mnt/sda4/develop/onvif/dpkg/gsoap/gsoap-2.8.28/build/
```

