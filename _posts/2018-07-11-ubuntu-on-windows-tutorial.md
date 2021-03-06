---
layout: post
title:  "Ubuntu on Windows10 Tutorial"
date:   2018-07-11 14:11:10 +0700
categories: [Tutorial, Ubuntu, WSL, Windows10]
---

---

Last Modified: 2018.07.11  

**NOTE THAT CUDA SUPPORT IS NOT AVAILABLE ON WSL**

---
### Installation

Now Ubuntu 16.04 is freely available for Windows10. The ubuntu terminal for Windows (<u>Windows Subsystem for Linux</u>, WSL) has many of the same features as follows:

- Shell environments including Bash, **without virtual machines or dual-booting**.
- Run **native tools such as SSH**, git, apt and dpkg directly from your Windows10.

Ubuntu can be installed from the **Microsoft Store**: 

- Use the Start menu to launch the Microsoft Store application.
- Search and install *Ubuntu 16.04* published by Canonical Group Limited.

<br/>

#### 1. Edit the Registry

You should activate "Windows Subsystem for Linux" in *Windows Features On or Off*.  To do this, press `Windows + R` to open Run dialog box and type `OptionalFeatures.exe` to directly do this. Then reboot the system.

<br/>

#### 2. Configuration

The above steps only enable to use Ubuntu 16.04 on Windows10. To use SSH just like openssh-server in local ubuntu machine, you need to configure some features that Windows does not support. If you do not have openssh-server toolkit, type `sudo apt-get install openssh-server`  

- Run `sudo vim /etc/ssh/sshd_config` to edit the SSH configuration file.
- Change the port number (default=22) such as 1234.
- Make sure that **UsePrivilegeSeparation** is set to **no**,  because this option is not supported yet in WSL. 
- If you want to connect ther server with your own password, make sure that **PasswordAuthentication** is set to **yes**. It will also ask for a key file in SSH connection.
- When the error with key files occurs, you should generate these key files manually. For example `sudo ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key`

<br/>

#### 3. Open a Specific Port in Firewall for SSH

Allow the port number that you have set for SSH above (e.g. 1234). See the [last post]({% post_url 2018-06-17-ftp-server-on-windows-tutorial %})

<br/>

#### 4. Restart OpenSSH-Server

Type `sudo service ssh --full-restart` on your ubuntu shell to restart the server. 

<br/>

#### 5. SSH into Ubuntu 16.04 on Windows 10

Open `Start - Remote Desktop Connection` and type the IP address of your remote server with **your own FTP port number**, for example "123.456.78.90:1234".

<br/>

[Go to the Home Page]({{ site.url }}{{ site.baseurl }})

Further Information: <dongyul.oh@snu.ac.kr>

<br/>

