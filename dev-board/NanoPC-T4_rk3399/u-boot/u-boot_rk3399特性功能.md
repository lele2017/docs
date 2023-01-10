## T4单板u-boot下按键设置

#### 入口函数

void key_init(void)

#### 进入maskrom

开机时按住boot键

__maybe_unused static void RockusbKeyInit(void)

#### 进入loader模式

开机时按住RecoveryKey

RecoveryKeyInit();

#### 电源按键

__maybe_unused static void PowerKeyInit(void)

#### 熄屏按键

PowerHoldGpioInit();



### T4单板启动后停留在loader下，不继续进入到系统（非按住recovery键）



