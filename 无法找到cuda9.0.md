在添加cuda环境变量后，一直无法找到cuda9.0
*1　有可能是在sudo下执行的，需要在sudo下添加环境变量
*2  添加lib
```
sudo vim /etc/ld.so.conf.d/cuda.conf
/usr/local/cuda/lib64 
/lib
/usr/lib
/usr/lib32
```
