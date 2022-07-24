# blog文章：

[TEE: OP-TEE](https://blog.csdn.net/mengkevin/article/details/72771190)

[聊聊SOC启动（四） ATF BL31启动流程](https://zhuanlan.zhihu.com/p/520052961)

[ARM Trusted Firmware分析——启动、PSCI、OP-TEE接口](https://www.cnblogs.com/arnoldlu/p/14175126.html)

[TEE安全攻防之内存隔离](http://www.hackdig.com/02/hack-271973.htm)

### 编译步骤

```
#rm -rf out/
make PLATFORM=rockchip CFG_TEE_CORE_LOG_LEVEL=4 DEBUG=1 CFG_TEE_BENCHMARK=n
sudo cp out/arm-plat-rockchip/core/tee-pager_v2.bin /mnt/sda4/develop/rk3399/src/rockchip-linux/rkbin/bin/rk33/rk3399_bl32_v3.01.bin
cd /mnt/sda4/develop/rk3399/src/rockchip-linux/u-boot
sudo ./make.sh
cd -
```

CFG_TEE_CORE_LOG_LEVEL说明：

```

# Log levels for the TEE core. Defines which core messages are displayed
# on the secure console. Disabling core log (level set to 0) also disables
# logs from the TAs.
# 0: none
# 1: error
# 2: error + warning
# 3: error + warning + debug
# 4: error + warning + debug + flow
CFG_TEE_CORE_LOG_LEVEL ?= 1
```



### 编译op-tee支持rk3399

