# InvestStudy (Started: 2021-04-07)


Environment 
 - WSL2 based windows 10
 - Ubuntu 18.04
 - Ryzen 5 3600
 - Geforce RTX 3060 (12gb)
 - Nvidia Drvier 470.14
 - Cuda 11.0
 - Cudnn 8.0.5
 - tensorflow 2.6.0


1. Setup


 --------------------------------------------------------------------------  
(0) Etc
- VxXsrv : https://sourceforge.net/projects/vcxsrv/ (GUI기반 프로그램 실행)
- 설치 후  ~/.bashrc 맨 아래 아래 문장 두개를 추가 필요
    
    
```java
export DISPLAY="`grep nameserver /etc/resolv.conf | sed 's/nameserver //'`:0"
export LIBGL_ALWAYS_INDIRECT=1
```
- miniconda : https://docs.conda.io/projects/conda/en/latest/user-guide/install/linux.html 참조
   
 --------------------------------------------------------------------------  
(1) Installing Nvidia Driver for CUDA on WSL
  - 공식 홈페이지 이용 https://developer.nvidia.com/cuda/wsl/download
  - 설치 확인
```java
nvidia-smi.exe
```
    
![image](https://user-images.githubusercontent.com/33775481/115145964-7219e800-a08f-11eb-8160-9827d7b40b57.png)
   
- Drvier Ver : 470.14 
 
 
  --------------------------------------------------------------------------  
(2) Installing CUDA Toolkit (https://docs.nvidia.com/cuda/wsl-user-guide/index.html#running-cuda 참조)
- CUDA repository 설정
```java  
sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub
sudo sh -c 'echo "deb http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64 /" > /etc/apt/sources.list.d/cuda.list'
sudo apt-get update
sudo apt-get install -y cuda-toolkit-11-0
``` 
- Cuda 버전확인 명령어 (경로 확인 필요)
```java    
nvcc --version
```

![image](https://user-images.githubusercontent.com/33775481/116100630-129f8600-a6e8-11eb-9932-fed350009818.png)

- cuda Ver : 11.0 으로 확인


 --------------------------------------------------------------------------  
(3) Installing Cudnn  
- https://developer.nvidia.com/rdp/cudnn-archive
:Download cuDNN v8.0.5 (November 9th, 2020), for CUDA 11.0 (cuDNN Library for Linux (x86_64)) 
(file name : cudnn-11.0-linux-x64-v8.0.5.39.solitairetheme8)
```java      
tar -xzvf cudnn-11.0-linux-x64-v8.0.5.39.solitairetheme8
sudo cp cuda/include/cudnn*.h /usr/local/cuda/include
sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
sudo chmod a+r /usr/local/cuda/include/cudnn*.h /usr/local/cuda/lib64/libcudnn*
``` 
- 아래 명령어 수행시, CUDNN_MAJOR 8이 출력되면 정상 설치 완료 (cudnn Ver : 8.0)
     
	>cat /usr/local/cuda/include/cudnn_version.h | grep CUDNN_MAJOR -A 2
	>

     ![image](https://user-images.githubusercontent.com/33775481/116100178-a7ee4a80-a6e7-11eb-9199-b810d12c3527.png)

     
   - bashrc 파일 맨아래 아래의 경로 추가 필요
     
	>export PATH=/usr/local/cuda-11.1/bin${PATH:+:${PATH}}
	>
	>export LD_LIBRARY_PATH=/usr/local/cuda-11.1/lib64:$LD_LIBRARY_PATH
	>
     
     
 --------------------------------------------------------------------------  
(4) Installing tensorflow      
    
   - 설치 가능한 Tensorflow 버전 확인 (https://www.tensorflow.org/install/source_windows#tested_build_configurations)
   - 현재는 최신 업데이트 버전 tf-nightly-gpu 설치 예정
   
	> pip install tf-nightly
 
   - 현재 설치 버전 : tf-nightly 2.6.0.dev20210426 (tf-nightly 버전 확인 : https://pypi.org/project/tf-nightly/)
  
(4-1) GPU 활용 Tensorflow 사용가능 여부 Test
     
	> import tensorflow as tf 
	> 
	> from tensorflow.python.client import device_lib
	> 
	> device_lib.list_local_devices() 
	> 
   

  - ibcusolver.so.10 에러 발생 (GPU Skip 했기에 아래와 같이 CPU만 인식됨)
  
  ![image](https://user-images.githubusercontent.com/33775481/116102144-66f73580-a6e9-11eb-866b-1b40a6aa9c78.png)

  - 해결 방법
      
      	> sudo ln -s /usr/local/cuda-11.0/lib64/libcusolver.so.10 /usr/local/cuda-11.0/lib64/libcusolver.so.11
  
  ![image](https://user-images.githubusercontent.com/33775481/116102785-f3a1f380-a6e9-11eb-8607-6eec95333b0f.png)

 
  
 --------------------------------------------------------------------------    
(?) Installing Docker & Nvidia Container Toolkint (Docker 활용 GPU 활용 현재 불가능, 추후 업데이트 필요)
     
    > curl https://get.docker.com | sh
    > 
    > distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
    > 
    > curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
    > 
    > curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
    > 
    > curl -s -L https://nvidia.github.io/libnvidia-container/experimental/$distribution/libnvidia-container-experimental.list | sudo tee /etc/apt/sources.list.d/libnvidia-container-experimental.list
    >
    > sudo apt-get update
    > 
	> sudo apt-get install -y nvidia-docker2
	> 
