# InvestStudy
2021-04-07

Environment 
 - WSL2 based windows 10
 - Ubuntu 18.04
 - Ryzen 5 3600
 - Geforce RTX 3060 (12gb)


// Ubuntu Terminal -> U.T. 약어로 이용

1. Setup
(1) Installing Nvidia Driver for CUDA on WSL
  - 공식 홈페이지 이용 https://developer.nvidia.com/cuda/wsl/download
  - 설치 확인
    > (U.T.) nvidia-smi.exe
    

![image](https://user-images.githubusercontent.com/33775481/115145964-7219e800-a08f-11eb-8160-9827d7b40b57.png)
  
  
 드라이버 버전 : 470.14  CUDA ver : 11.3
 
(2) Installing CUDA Toolkit (https://docs.nvidia.com/cuda/wsl-user-guide/index.html#running-cuda 참조)
  - CUDA repository 설정
(U.T.) > sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub
    > sudo sh -c 'echo "deb http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64 /" > /etc/apt/sources.list.d/cuda.list'
    > sudo apt-get update
    > sudo apt-get install -y cuda-toolkit-11-3
   
(3) Installing Docker 
(U.T.) > curl https://get.docker.com | sh
  >
