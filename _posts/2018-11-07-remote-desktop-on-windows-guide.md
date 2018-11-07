---
layout: post
title:  "Remote Desktop on Windows10 Tutorial"
date:   2018-11-07 11:13:10 +0700
categories: [Tensorflow, Remote Desktop, Windows10, Guide]
---

---

Last Modified: 2018.07.11

This tutorial refers to <http://www.snoopybox.co.kr/1545>.

---
### Port Setting

TCP port 21 (by default) connects FTP servers to the internet. Since FTP servers carry numerous vulnerabilities such as anonymous authentication capabilities, directory traversals, remote-desktop service, and cross-site scripting, **TCP port 21 is fundamentally unsafe from the start**.

#### 1. View/Edit the Registry

We need to change this port number.

- Type `regedit` in Run dialog box to directly open the Registry Editor.
- You can change the default TCP port number in the following registry subkey: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp`.
- Change the base setting (default=3389) as a decimal number such as 2022.

<br/>

#### 2. Open a Specific Port in Firewall

Now **you should allow this port number in the firewall setting** with advanced security. Type `wf.msc` in Run dialog box, and click `Advanced settings` on the left-side panel. Then open `Inbound Rules - New Rule` and take the following steps.

- Rule Type: Select the rule type **Port**.
- Protocol and Ports: In the New Inbound Rule Wizard dialog, leave **TCP** selected, and enter port number that you have set in the Registry Editor (see step1) such as 2022.
- Action: Select the option **Allow the connection** to accept incoming traffic on these ports.
- Profile: Depending on the network you are connected to, select the connection types where the particular rule should be applied. You can select all three **Domain**, **Private**, and **Public** if you’re not sure which one to select.
- Name: Provide a name for the rule you created, for example "**Remote**". This name will appear under Incoming Rules in your firewall settings. 

<br/>

#### Restart Remote Desktop Service

Type `services.msc` in Run dialog box and right-click `Remote Desktop Services - Restart`.  

------



### Remote Desktop Service

Now all you have to do is to open `Start - Remote Desktop Connection` and type the IP address of your remote server **with its own FTP port number**, for example "123.456.78.90:2022".



[Go to the Home Page]({{ site.url }}{{ site.baseurl }})

