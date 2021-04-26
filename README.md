# InvestStudy
2021-04-07

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

(0) Etc
   - VxXsrv : https://sourceforge.net/projects/vcxsrv/ (GUI기반 프로그램 실행)
   
    - 설치 후  ~/.bashrc 맨 아래 아래 문장 두개를 추가 필요
    > export DISPLAY="`grep nameserver /etc/resolv.conf | sed 's/nameserver //'`:0"
    > 
    > export LIBGL_ALWAYS_INDIRECT=1
   
   - miniconda : https://docs.conda.io/projects/conda/en/latest/user-guide/install/linux.html 

   - tensorflow : 현재 Cuda 11.0 Cudnn 8.0.5 기준으로 활용하기 때문에 developer 버전 
   
(1) Installing Nvidia Driver for CUDA on WSL
  - 공식 홈페이지 이용 https://developer.nvidia.com/cuda/wsl/download
  - 설치 확인
    > nvidia-smi.exe
    

![image](https://user-images.githubusercontent.com/33775481/115145964-7219e800-a08f-11eb-8160-9827d7b40b57.png)
  
  
 드라이버 버전 : 470.14 
 
(2) Installing CUDA Toolkit (https://docs.nvidia.com/cuda/wsl-user-guide/index.html#running-cuda 참조)
  - CUDA repository 설정
    > sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub
    > 
    > sudo sh -c 'echo "deb http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64 /" > /etc/apt/sources.list.d/cuda.list'
    >     
    > sudo apt-get update
    >     
    > sudo apt-get install -y cuda-toolkit-11-0
    > 

(3) Installing Cudnn 
   
   - https://developer.nvidia.com/rdp/cudnn-archive
     
     o  Download cuDNN v8.0.5 (November 9th, 2020), for CUDA 11.0 (cuDNN Library for Linux (x86_64)) 
     (file name : cudnn-11.0-linux-x64-v8.0.5.39.solitairetheme8)
     
     > tar -xzvf cudnn-11.0-linux-x64-v8.0.5.39.solitairetheme8
     > 
     > sudo cp cuda/include/cudnn*.h /usr/local/cuda/include
     > 
     > sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
     > 
     > sudo chmod a+r /usr/local/cuda/include/cudnn*.h /usr/local/cuda/lib64/libcudnn*

     
     
   
(4) Installing Docker & Nvidia Container Toolkint (Docker 활용 GPU 활용 현재 불가능, 추후 업데이트 필요)
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


