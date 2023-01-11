---
sort: 2
---

# jz2440 u-boot代码分析



## u-boot移植

### 参考资料

[移植u-boot-2016.11到JZ2440](https://blog.csdn.net/qq_36576792/article/details/86713860)





### 增加run命令

```c
void sysrq_timer_list_show(void)
{
	timer_list_show(NULL, NULL);
}

static int timer_list_open(struct inode *inode, struct file *filp)
{
	return single_open(filp, timer_list_show, NULL);
}

static const struct file_operations timer_list_fops = {
	.open		= timer_list_open,
	.read		= seq_read,
	.llseek		= seq_lseek,
	.release	= single_release,
};
```



## linux
