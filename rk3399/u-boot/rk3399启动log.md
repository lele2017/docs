## rk3399正常启动时log

```
Bus Width=32 Col=10 Bank=8 Row=15/15 CS=2 Die Bus-Width=32 Size=2048MB
256B stride
ch 0 ddrconfig = 0x101, ddrsize = 0x2020
ch 1 ddrconfig = 0x101, ddrsize = 0x2020
pmugrf_os_reg[2] = 0x3AA0DAA0, stride = 0xD
OUT
Boot1: 2017-06-09, version: 1.09
CPUId = 0x0
ChipType = 0x10, 1893
SdmmcInit=2 0
BootCapSize=100000
UserCapSize=14910MB
FwPartOffset=2000 , 100000
SdmmcInit=0 20
StorageInit ok = 67290
LoadTrustBL
No find bl30.bin
Load uboot, ReadLba = 2000
Load OK, addr=0x200000, size=0x731ac
RunBL31 0x40000
NOTICE:  BL31: v1.3(release):845ee93
NOTICE:  BL31: Built : 15:51:11, Jul 22 2020
NOTICE:  BL31: Rockchip release version: v1.1
INFO:    GICv3 with legacy support detected. ARM GICV3 driver initialized in EL3
INFO:    Using opteed sec cpu_context!
INFO:    boot cpu mask: 0
INFO:    plat_rockchip_pmu_init(1196): pd status 3e
INFO:    BL31: Initializing runtime services
INFO:    BL31: Initializing BL32
INF [0x0] TEE-CORE:init_primary_helper:337: Initializing (1.1.0-266-gee81607c #1 Mon Aug 17 09:23:30 UTC 2020 aarch64)

INF [0x0] TEE-CORE:init_primary_helper:338: Release version: 1.2

INF [0x0] TEE-CORE:init_teecore:83: teecore inits done
INFO:    BL31: Preparing for EL3 exit to normal world
INFO:    Entry point address = 0x200000
INFO:    SPSR = 0x3c9


U-Boot 2014.10-RK3399-06-g650317a (Feb 27 2022 - 15:11:27)

CPU: rk3399
cpu version = 0
CPU's clock information:
    aplll = 816000000HZ
    apllb = 24000000HZ
    gpll = 800000000HZ
               aclk_periph_h = 133333333HZ, hclk_periph_h = 66666666HZ, pclk_periph_h = 33333333HZ
               aclk_periph_l0 = 100000000HZ, hclk_periph_l0 = 100000000HZ, pclk_periph_l0 = 50000000HZ
               hclk_periph_l1 = 100000000HZ, pclk_periph_l1 = 50000000HZ
    cpll = 800000000HZ
    dpll = 800000000HZ
    vpll = 24000000HZ
    npll = 24000000HZ
    ppll = 676000000HZ
Board:  Rockchip platform Board
Uboot as second level loader
DRAM:  Found dram banks: 1
Adding bank:0000000000200000(00000000ffe00000)
Reserve memory for trust os.
dram reserve bank: base = 0x08400000, size = 0x01e00000
128 MiB
SdmmcInit = 0 20
storage init OK!
Using default environment
```

