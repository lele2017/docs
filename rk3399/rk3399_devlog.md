---
sort: 0
---

# rk3399 QT代码分析



## u-boot



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
