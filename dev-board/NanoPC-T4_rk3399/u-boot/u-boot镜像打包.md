## boot_merger

Z:\sda4\develop\rk3399\src\android-8.1\RKDocs\common\u-boot\Rockchip U-Boot 开发指南 V3.8-20170214.pdf

打包描述如下：

```shell
./tools/boot_merger ./tools/rk_tools/RKBOOT/RK3288.ini out:RK3288Loader_UBOOT.bin fix opt:RK3288Loader_UBOOT_V2.15.bin merge success(RK3288Loader_UBOOT_V2.15.bin)
```

>以 3288 的配置文件为例：
>[CHIP_NAME]
>NAME=RK320A ----芯片名称： ”RK”加上与 maskrom 约定的 4B 芯片型号
>[VERSION]
>MAJOR=2 ----主版本号
>MINOR=15 ----次版本号
>[CODE471_OPTION] ----code471，目前设置为 ddr bin
>NUM=1
>Path1=tools/rk_tools/32_LPDDR2_300MHz_LPDDR3_300MHz_DDR3_300MHz_20
>140404.bin
>[CODE472_OPTION] ----code472，目前设置为 usbplug bin
>NUM=1
>Path1=tools/rk_tools/rk32xxusbplug.bin
>[LOADER_OPTION]
>NUM=2
>LOADER1=FlashData ----flash data，目前设置为 ddr bin
>LOADER2=FlashBoot ----flash boot，目前设置为 UBOOT bin
>FlashData=tools/rk_tools/32_LPDDR2_300MHz_LPDDR3_300MHz_DDR3_300MHz
>_20140404.bin
>FlashBoot=u-boot.bin
>[OUTPUT] ----输出路径，目前文件名会自动添加版本号
>PATH=RK3288Loader_UBOOT.bin 

RK3399MINIALL.ini内容如下：

```
[CHIP_NAME]
NAME=RK330C
[VERSION]
MAJOR=1
MINOR=26
[CODE471_OPTION]
NUM=1
Path1=bin/rk33/rk3399_ddr_800MHz_v1.25.bin
Sleep=1
[CODE472_OPTION]
NUM=1
Path1=bin/rk33/rk3399_usbplug_v1.26.bin
[LOADER_OPTION]
NUM=2
LOADER1=FlashData
LOADER2=FlashBoot
FlashData=bin/rk33/rk3399_ddr_800MHz_v1.25.bin
FlashBoot=bin/rk33/rk3399_miniloader_v1.26.bin
#FlashBoot=/mnt/sda4/develop/rk3399/src/rockchip-linux/u-boot/u-boot.bin
[OUTPUT]
PATH=rk3399_loader_v1.25.126.bin
```

