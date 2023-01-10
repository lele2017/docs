## 参考资料

[OP-TEE 编译流程](https://blog.csdn.net/lidan113lidan/article/details/119879565)

## 编译步骤

```shell
update-alternatives --config python                           //选择2.7版本
git checkout 3.8.0
git checkout 3.9.0 core/arch/arm/kernel/link.mk
make PLATFORM=rockchip CFG_TEE_CORE_LOG_LEVEL=4 DEBUG=0



```



## 链接分析

core/arch/arm/kernel/kern.ld.S