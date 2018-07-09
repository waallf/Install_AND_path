[copy from ](https://blog.csdn.net/breeze5428/article/details/78256915)  
# 1. download CUDA  
[Download deb file](https://developer.nvidia.com/cuda-downloads)  

# 2. Install deb in Terminal  
```
sudo dpkg -i cuda-repo-ubuntu1604-<Version>.deb  
sudo apt-key add /var/cuda-repo;version;/7fa2af80.pub   
sudo apt-get update
sudo apt-get install cuda
```  
# Change Path  
```sudo gedit ~/.bashrc```  
add this in .bashrc  
```
export CUDA_HOME=/usr/local/cuda-<version>
export LD_LIBRARY_PATH=${CUDA_HOME}/lib64 
export  PATH=${CUDA_HOME}/bin:${PATH} 
```  

# 4. nvidia-smi -lms  view gpu 
