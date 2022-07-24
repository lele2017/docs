## 版本差异说明

#### 函数接口的重大变化：3.8.0支持，而3.9.0则没有了

**grep -inr *init_primary_helper***

![image-20220723234704784](op-tee官方版本说明.assets/image-20220723234704784.png)

ps：rkbin下提供的bl32.bin启动时有显示“init_primary_helper”的打印：

```
INFO:    BL31: Initializing BL32
INF [0x0] TEE-CORE:init_primary_helper:337: Initializing (1.1.0-266-gee81607c #1 Mon Aug 17 09:23:30 UTC 2020 aarch64)

INF [0x0] TEE-CORE:init_primary_helper:338: Release version: 1.2

INF [0x0] TEE-CORE:init_teecore:83: teecore inits done
INFO:    BL31: Preparing for EL3 exit to normal world
INFO:    Entry point address = 0x200000
INFO:    SPSR = 0x3c9
```

