## 生成构建

```shell
#方式一：
find ./ -name "*.[chSs]"  > cscope.files
# 
find . -type f ! -name "*.o" > cscope.files

cscope -b -q -k
```



