---
layout: post
title:  "FTP Server on Windows10 Tutorial"
date:   2018-11-26 16:53:10 +0700
categories: [Tutorial]
---

---

Last Modified: 2018.07.11  
This tutorial refers to http://frog-hindleg.tistory.com/118.

---
### Bulid FTP Server 

You'll find many third-party software on the internet to build a file transfer server, but Windows includes an FTP server feature that you can set up without the need to resource to other solutions. Since FTP server can only write/read files and not control the whole system like remote desktop, using the default port 21 is OK.

#### 1. Activate FTP Services

Press `Windows + R` on your keyboard to open Run dialog box and type `OptionalFeatures.exe` to directly access *Windows Features On or Off*.  Check the following features marked in bold:

- **Internet Information Services**
    - **FTP Server**
        - **FTP Services**
        - FTP Extensibility
- **Web Management Tools**
    - IIS 6 Management Compatibility
    - IIS Management Scripts and Tools
    - IIS Management Service
    - **IIS Management Console**



#### 2. Configure FTP with IIS Manager  

Type `inetmgr.exe` in Run dialog box to open *IIS Management Tools*, or you can manually open it by goint to `Start - IIS Manager`.  Then right-click the `Sites - Add FTP Site` in the left *Connections* pane. When the wizard appears, take the following steps:

- Site Information: Enter new name in the FTP site name box, for example "My FTP". Then navigate to the folder that you created in the Prerequisites section.
- Binding and SSL Settings: Do not choose a specific IP address for you FTP sites, and just leave it as **All Unassigned**. Enter the TCP/IP **port number 21** for FTP service in Port box. Select the option **Allow SSL** with **Not Selected** for SSL Certificate drop-down. 
- Here **do not use same port number as remote desktop**, which you have already configured in the [last post]({% post_url 2018-06-01-remote_windows_tutorial %}).
- Authentication and Authorization Information: select **Basic** and **Specified users** from the Allow access to drop-down. Type the user name of your FTP server in the box, for example "administrator", and select both **Read** and **Write** in Permissions options.


<br/>

[Go to the Home Page]({{ site.url }}{{ site.baseurl }})

Further Information: <dongyul.oh@snu.ac.kr>

<br/>
