# 参考资料

[OPTEE学习笔记 - 启动流程（一）](https://blog.csdn.net/orlando19860122/article/details/111880726)

[OPTEE学习笔记 - 启动流程（二）](https://blog.csdn.net/orlando19860122/article/details/113806163)

[OP-TEE笔记之TEECORE的启动过程](https://blog.csdn.net/u010071291/article/details/50836547?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_title~default-1-50836547-blog-113806163.pc_relevant_vip_default&spm=1001.2101.3001.4242.1&utm_relevant_index=4)

[optee专栏连载文章——作者: 代码改变世界ctw](https://blog.csdn.net/weixin_42135087/category_9726561.html)

# 源码走读分析

### 入口函数（_start）

​	/mnt/sda4/develop/rk3399/src/rockchip-linux/open-tee/optee_os/core/arch/arm/kernel/generic_entry_a64.S

```c
FUNC _start , :
	mov	x19, x0		/* Save pagable part address */
#if defined(CFG_DT_ADDR)
	ldr     x20, =CFG_DT_ADDR
#else
	mov	x20, x2		/* Save DT address */
#endif
	......
	b	.	/* SMC should not return */
END_FUNC _start
```

## 主Init函数：init_primary_helper



```c
_start
  ==》bl generic_boot_init_primary					//optee_os/core/arch/arm/kernel/generic_entry_a64.S
​	==》generic_boot_init_primary 
​	   ==》init_primary_helper
```





