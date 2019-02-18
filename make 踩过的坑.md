１．　python 版本不匹配，要把所有的编译语句　python改为对应的python版本　　

２．　-gencode arch=compute_x,code=sm_x　要根据自己的cuda运行值来设置(在安装cuda路径位置找到deviceQuery，make,执行)，不然会显示　　
  ｀invalid device function｀错误　　
