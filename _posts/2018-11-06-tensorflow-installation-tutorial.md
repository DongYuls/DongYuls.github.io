---
layout: post
title:  "Tensorflow Installation Tutorial"
date:   2018-11-06 18:34:10 +0700
categories: [Tutorial, Tensorflow, Installation]
---

---

Last Modified: 2018.11.07  
This tutorial refers to <https://www.tensorflow.org/install>.

---
### NVIDIA Settings (Only GPU)

TensorFlow GPU support requires an assortment of drivers and libraries. To avoid library conflicts, your are recommended using a **virtual environment with pyenv** (Linux only) after installation of Tensorflow GPU.  
<br/>

#### Hardware Requirements

- NVIDIA® GPU card with CUDA® Compute Capability >= 3.5. See the list of [CUDA-enabled GPU cards](https://developer.nvidia.com/cuda-gpus).

#### Software Requirements

- NVIDIA® GPU drivers: CUDA 9.0 requires 384.x or higher.  
- CUDA® Toolkit: TensorFlow supports CUDA 9.0.  
- cuDNN SDK (>= 7.2)  

<br/>

#### 1. Install CUDA

##### Option 1. APT with Command Line
For Ubuntu 16.04 and possibly other Debian-based Linux add the NVIDIA package repository and use `apt` to install CUDA. Installation instructions can be found in <https://www.tensorflow.org/install/gpu>.  

##### Option 2. Manually Download (Recommended)

Go to [https://developer.nvidia.com/cuda-downloads](https://developer.nvidia.com/cuda-downloads) and see the **legacy releases**.

- Install CUDA Toolkit 9.0 by clicking the green button that describe your computer platform.

- You must download the base installer, and the other pathces are optional.

- After installation, type the following instruction with Command Line:
  `sudo dpkg -i cuda-repo-ubuntu1604-9-0-local_9.0.176-1_amd64.deb`  
  `sudo apt-key add /var/cuda-repo-<version>/7fa2af80.pub`  
  `sudo apt-get update`  
  `sudo apt-get install cuda`  
  
  Note: CUDA Toolkit for Windows10 will automatically install CUDA driver and tools needed to create, build and run its application as well as libraries, header files, CUDA samples source code, and other resources.

<br/>

#### 2. Install cuDNN

Go to [https://developer.nvidia.com/cudnn](https://developer.nvidia.com/cudnn) and download cuDNN 7.3.1 **Library for Linux** (matching CUDA 9.0 which you have already downloaded in the previous step).
- After installation of cuDNN archive, unzip it with `tar -xzvf [cuDNN filename]` 

- Copy them into CUDA directory (the directory path may differ according to CUDA version):  

  `sudo cp cuda/include/cudnn.h /usr/local/cuda-9.0/include/`  
  `sudo cp cuda/lib64/* /usr/local/cuda-9.0/lib64/`  


  Note: CUDA path and the environmental variable settings for Windows10 are different. See [Windows Setup](https://www.tensorflow.org/install/gpu).

---
<br/>

### Build Python Environment

If you are using Window 10, you should install Microsoft Visual C++ 2015 Redistributable Package.  
Download: [https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/en-us/download/details.aspx?id=52685)  
Naive Python: [https://www.python.org/](https://www.python.org/)  
<br/>

In Linux, you must take the following steps:

#### 1. Install Packages and Dependencies (.pyenv)   
`sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev` `sudo apt-get install libreadline-dev libsqlite3-dev wget curl llvm ` 

<br/>

#### 2. Install Pyenv from Git  
Pyenv is a very simple python **version management tool** that lets you easily switch between multiple versions of python. It works like a virtualenv, using UNIX tradition of single-purpose tools that do one thing well.
`sudo apt-get install git`  
`curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash`
Further information can be found in <https://github.com/pyenv/pyenv>.

<br/>

#### 3. View/Edit Bash Profile
Pyenv intercepts python commands using shim executables injected into your environmental path, determines which python version has been specified by your application.
Therefore you need to add several script shown below into "**.profile**", which is located in your home directory. Here the editor (e.g. nano, vi, vim) does not matter.  

```
export PATH="$HOME/.pyenv/bin:$PATH"  
eval "$(pyenv init -)"  
eval "$(pyenv virtualenv-init -)"  
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64/
```
After editing .profile, reboot the system or logout.  
<br/>

#### 4. Install python 3.n  
`pyenv install 3.6.6` (to undo: `pyenv uninstall 3.6.6`)   
`pyenv versions` to list python versions that you have.  
`pyenv global 3.6.6`   

Some useful python packages: `pip install pydicom scipy scikit-image sklearn pandas`

---
<br/>

### Install Tensorflow
Current release: `pip install tensorflow-gpu`  
Legacy release: `pip install tensorflow-gpu==<version>`

---

<br/>

### Build Matlab Environment

This tutorial is only validated with the following dependencies.
- CUDA v8.0 with cuDNN 6.0
- Microsoft Visual Studio 2015 (Visual C++)
- Matlab R2017a from <https://kr.mathworks.com/downloads/web_downloads/>

<br/>

#### 1. Install Visual Studio 2015

First of all, you need C/C\++ compiler such as Visual C\++ or MinGW. However, matconvnet which is a library for building convolution neural network, currently only supports Visual C\++.  
Download: [https://www.visualstudio.com/ko/vs/older-downloads/](https://www.visualstudio.com/ko/vs/older-downloads/). The download will be activated only if you agree to use the Visual Studio Dev Essentials benefit on the MyAccount page.

<br/>

#### 2. Install Visual C++ and Windows10 SDK

Make sure that Visual C++ and Windows10 SDK have been installed.  

- **Run Visual Studio 2015 installer again** and check the following items.   
  `Programming Language - Visual C++`  
  `Universal Tools for Windows Apps (Check All)`  

- After installation, reboot the system.  

<br/>

#### 3. Environment Variable Setting

Make new user environment variable path so that matlab can locate the complier.

```
C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\bin
C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE
C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\Tools
```

Make new system environment variable path named **INCLUDE** and **LIB**, respectively, in order to link the basic header files for C++ compiler.

```
C:\Program Files (x86)\Windows Kits\10\Include\10.0.10240.0\ucrt
```

```
C:\Program Files (x86)\Windows Kits\10\Lib\10.0.10240.0\um\x64
C:\Program Files (x86)\Windows Kits\10\Lib\10.0.10240.0\ucrt\x64
```



<br/>

[Go to the Home Page]({{ site.url }}{{ site.baseurl }})

Further Information: <dongyul.oh@snu.ac.kr>

<br/>

