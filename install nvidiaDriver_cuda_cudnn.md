# 安装这些东西必需要有严格的版本对应关系，否则安装不成功  
## install nvidaiDriver  
1.查看自己电脑应该安装的驱动器版本 [连接](https://www.nvidia.cn/Download/index.aspx?lang=cn)  
2.`sudo apt-get install nvidia-390`   
3.安装完成以后`nvidia-smi`查看是否安装成功  
## install cuda   
* 安装完nvidia驱动器以后，查看版本对照表 [连接](https://www.cnblogs.com/LearnFromNow/p/9417272.html)  

1.下载对应版本的cuda [连接](https://developer.nvidia.com/)  下载.run版本  
2.运行.run文件，， `sudo sh --下载的文件名.run`   
  点回车，一直往下，会提醒是否安装对应的nvidia 驱动器版本（以为前面已经配置好了，所以没有再安装），其他都选择默认   
3.配置环境变量  
  * `sudo gedit /etc/profile`  
  *  打开文件后，在末尾添加路径，  
  *  `export PATH=/usr/local/cuda/bin:$PATH`  
  *  `export LD_LIBRARY_PATH=/usr/local/cuda/lib64&LD_LIBRARY_PATH`  
  
4.然后保存，重启电脑  
5.测试安装是否成功  
  `cd /usr/local/cuda/samples/1_Utilities/deviceQuery`  
  `sudo make`  
  `./deviceQuery`  
  如果显示关于GPU的信息就是成功了   
  
# install cudnn   
* 安装的是cudnn7.0版    
## 此处有坑  
1. 下载对应版本的cudnn[连接](https://developer.nvidia.com/cudnn)  
2. 这里需要下载两个版本（不知道为啥），runtime版和developer版  
3. 将下载的文件格式改为.tgz，然后解压  
4. 一个里版本里面有头文件(在include文件中)，一个里面有动态连接文件（在lib文件中），将头文件（cudnn.h）拷贝到/usr/local/cuda/lib64  
5. 复制动态连接库 `sudo cp lib* /usr/local/cuda/lib64/`  
6. `cd /usr/local/cuda/lib64/`  
7. 对刚考进来的两个动态连接库创建软链接： `sudo ln -s libcudnn.so.7 libcudnn.so`,`sudo ln -s libcudnn.so.7.0.5 libcudnn.so.7`  

  
