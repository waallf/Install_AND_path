# 需要的文件  

[roi_文件](./src)  
1. Move everything under `src/` to `YOUR_TENSORFLOW_PATH/lib/python2.7/site-packages/tensorflow/core/user_ops`. You can find out your tensorflow path by running

    `python -c 'import tensorflow as tf; print(tf.__file__)'`

2. `cd YOUR_TENSORFLOW_PATH/lib/python2.7/site-packages/tensorflow/core/user_ops/`
3. Run the following command to compile a GPU-capable RoI-Pooling layer
```
TF_INC=$(python -c 'import tensorflow as tf; print(tf.sysconfig.get_include())')
```
```
TF_LIB=$(python -c 'import tensorflow as tf; print(tf.sysconfig.get_lib())')
```
```
nvcc -std=c++11 -c -o roi_pooling_op_gpu.cu.o roi_pooling_op_gpu.cu.cc -I     $TF_INC -D GOOGLE_CUDA=1 -x cu -Xcompiler -fPIC -I \
~/miniconda3/envs/tensorflow36/lib/python3.6/site-packages -I /usr/local --expt-relaxed-constexpr -DNDEBUG -L$TF_LIB
```
```
g++ -std=c++11 -shared -o roi_pooling_op_gpu.so roi_pooling_op.cc -D_GLIBCXX_USE_CXX11_ABI=0 roi_pooling_op_gpu.cu.o \
-I $TF_INC -L $TF_LIB -ltensorflow_framework -D GOOGLE_CUDA=1 -fPIC -lcudart -L /usr/local/cuda-9.0/lib64/
```
测试是否成功：  
```
 python -c 'import tensorflow as tf; tf.load_op_library("./roi_pooling_op_gpu.so")'  
```
上面为在本机上编译通过的代码  
一般会报找不到***， 就在命令后面加 -I 将路径跟到后面(只需要写道找不到文件的上一级路径)  
要加 $TF_LIB -ltensorflow_framework ，否则会报错  
-D_GLIBCXX_USE_CXX11_ABI =0 否则报错  
## 还需要注意是否在所需要的python环境中  
