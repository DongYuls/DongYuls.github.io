---
layout: post
title:  "Tensorflow Installation Tutorial"
date:   2018-11-06 18:34:10 +0700
categories: [Tutorial, Tensorflow, Installation]
---

---

Last Modified: 2018.11.07
This tutorial refers to https://www.tensorflow.org/install/gpu.

---
### NVIDIA Settings (Only GPU)

TensorFlow GPU support requires an assortment of drivers and libraries. To avoid library conflicts, your are recommended using a virtual environment with pyenv (Linux only) after installation of Tensorflow GPU. 

#### Hardware Requirements

- NVIDIA® GPU card with CUDA® Compute Capability >= 3.5. See the list of [CUDA-enabled GPU cards](https://developer.nvidia.com/cuda-gpus).

#### Software Requirements

- NVIDIA® GPU drivers: CUDA 9.0 requires 384.x or higher.  
- CUDA® Toolkit: TensorFlow supports CUDA 9.0.  
- cuDNN SDK (>= 7.2)

#### 1. Install CUDA

##### (Option. 1) APT with Command Line
For Ubuntu 16.04 and possibly other Debian-based Linux distros add the NVIDIA package repository and use `apt` to install CUDA.

```
sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/7fa2af80.pub
wget http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_9.1.85-1_amd64.deb
sudo apt install ./cuda-repo-ubuntu1604_9.1.85-1_amd64.deb

wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64/nvidia-machine-learning-repo-ubuntu1604_1.0.0-1_amd64.deb
sudo apt install ./nvidia-machine-learning-repo-ubuntu1604_1.0.0-1_amd64.deb

sudo apt update

sudo apt install cuda9.0 cuda-cublas-9-0 cuda-cufft-9-0 cuda-curand-9-0 \
    cuda-cusolver-9-0 cuda-cusparse-9-0 libcudnn7=7.2.1.38-1+cuda9.0 \
    libnccl2=2.2.13-1+cuda9.0 cuda-command-line-tools-9-0
```

##### (Option. 2) Manually Download

Go to [https://developer.nvidia.com/cuda-downloads](https://developer.nvidia.com/cuda-downloads) and see the **legacy releases**.

- Install CUDA Toolkit 9.0 clicking the green button that describe your computer platform.

- You must download the base installer, and the other pathces are optional.

- After installation, type the following instruction with Command Line:

  ```
  sudo dpkg -i cuda-repo-ubuntu1604-9-0-local_9.0.176-1_amd64.deb
  sudo apt-key add /var/cuda-repo-<version>/7fa2af80.pub
  sudo apt-get update
  sudo apt-get install cuda
  ```

<br/>

#### 2. Install cuDNN 6.0

Go to [https://developer.nvidia.com/cudnn](https://developer.nvidia.com/cudnn) and download cuDNN 7.3.1 **Library for Linux** (matching CUDA 9.0 which you have just downloaded in step1).
- After installation of cuDNN, unzip it with `tar -xzvf [cuDNN filename]` 

- Copy them (header files) into CUDA directory (the directory path may differ according to CUDA version):

  ```
  sudo cp cuda/include/cudnn.h /usr/local/cuda-9.0/include/ 
  sudo cp cuda/lib64/* /usr/local/cuda-9.0/lib64/ 
  ```

  Note:  "C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0" (Windows10)

---
<br/>

### Build Python Environment

If you are using Window 10, you should install Microsoft Visual C++ 2015 Redistributable Package.  
Download: [https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/en-us/download/details.aspx?id=52685)  
Naive Python: [https://www.python.org/](https://www.python.org/)

In Linux, you must do following steps:

1. Install packages and dependencies (.pyenv)  
`sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm`

2. Install pyenv from git  
`sudo apt-get install git`  
`curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash`

3. After installation, you should add several script (shown below) into ".profile", which is located in your home directory.  
`sudo apt install vim`  
`vim .profile`  
...  
```html
export PATH="$HOME/.pyenv/bin:$PATH"  
eval "$(pyenv init -)"  
eval "$(pyenv virtualenv-init -)"  
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64/  
```

4. Reboot or logout  
`sudo reboot` or `logout`

5. Install python 3.n  
`pyenv install 3.5.2`  
`pyenv versions`  
`pyenv global 3.5.2`  

---
### Install Tensorflow

`pip install tensorflow-gpu` or `pip install tensorflow`

---

### Build Matlab Environment

Dependencies
- CUDA v8.0 with cuDNN 6.0
- Microsoft Visual Studio 2015 (Visual C++)

1. First of all, you need C/C\++ compiler such as Visual C\++ or MinGW. However, matconvnet which is a library for building convolution neural network, currently only supports Visual C\++.  
    Download: [https://www.visualstudio.com/ko/vs/older-downloads/](https://www.visualstudio.com/ko/vs/older-downloads/)  
2. After installation, make sure that Visual C++ and Windows10 SDK have been installed.  
    Run Visual Studio 2015 installer again and check the following items.   
    `Programming Language - Visual C++`  
    `Universal Tools for Windows Apps (Check All)`

3. Reboot the system  
4. Make new user environment variable path so that matlab can locate the complier.
```
C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\bin
C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE
C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\Tools
```

5. Make new system environment variable path named *include* and *LIB*, respectively, to link basic header files for C++ compiler.
```
C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\include
C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\atlmfc\include
C:\Program Files (x86)\Windows Kits\10\Include\10.0.10150.0\ucrt
```
```
C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\lib
C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\atlmfc\lib
C:\Program Files (x86)\Windows Kits\10\Include\10.0.10150.0\ucrt\x86
C:\Program Files (x86)\Windows Kits\8.1\Lib\winv6.3\um\x86
```

6. Now install Matlab R2017a from https://kr.mathworks.com/downloads/web_downloads/. **Note that this tutorial has been verified only with "Visual Studio 2015 + Matlab R2017a + CUDA v8.0 + cuDNN 6.0"**

<br/>

[Go to the Home Page]({{ site.url }}{{ site.baseurl }})

<br/>

