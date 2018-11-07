---
layout: post
title:  "Tensorflow Installation Tutorial"
date:   2018-11-06 18:34:10 +0700
categories: [Tutorial, Tensorflow, Installation, Guide]
---

---

Last Modified: 2018.05.28

---
### NVIDIA Settings (Only GPU)

1. Graphic Driver: `sudo apt-get install nvidia-381`  
After installation, you can check your own graphic device through `nvidia-smi`

2. CUDA Toolkit 8.0: [https://developer.nvidia.com/cuda-downloads](https://developer.nvidia.com/cuda-downloads) 

3. cuDNN 6.0: [https://developer.nvidia.com/cudnn](https://developer.nvidia.com/cudnn)

After installation of cuDNN 6.0, move them into CUDA directory.  
Windows 10: `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v8.0`  
Linux: `/usr/local/cuda`

**Note that tensorflow 1.4.2 only supports CUDA v8.0 and cuDNN v6.0 (2017.12.27)**  
Now tensorflow 1.8.0 supports CUDA v9.0 and cuDNN v7.0.5 (2018.05.29)  

---
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
