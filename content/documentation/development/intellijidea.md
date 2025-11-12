---
title: Using IntelliJ IDEA
weight: 172
tags: ["IntelliJ IDEA"]
---

IntelliJ IDEA is the most-used IDE for Java development. It's also available for ARM devices but has [high minimum requirements](https://www.jetbrains.com/help/idea/prerequisites.html#min_requirements), so it's not a good fit to use on a Raspberry Pi:

* 4 vCPUs, either x86_64 or arm64 architecture. Also, higher clock frequency is preferred to higher core count.
* 8 GB RAM.
* Not supported: _Single-board computers such as Raspberry Pi. To run your code on a Raspberry Pi, check out remote interpreters or remote debugging, and similar features._

## Remote Development with IntelliJ IDEA

You can use IntelliJ IDEA to develop on a remote machine (Windows, Linux, or macOS) with code on the Raspberry Pi. Make sure you have the Remote Development Gateway plugin enabled as described on [Connect to a remote server from IntelliJ IDEA](https://www.jetbrains.com/help/idea/remote-development-starting-page.html) and [Install JetBrains Gateway﻿](https://www.jetbrains.com/help/idea/jetbrains-gateway.html).

1. Go to "File" > "Remote Development".
![01-toolbar.png](/assets/documentation/intellij/01-toolbar.png)
2. Click "SSH Connection" > "New Connection".
![02-ssh.png](/assets/documentation/intellij/02-ssh.png)
3. Fill in the username and hostname of your Raspberry Pi and click "Check Connection and Continue".
![03-connect.png](/assets/documentation/intellij/03-connect.png)
4. Select the directory with the sources you want to edit.
![04-directory.png](/assets/documentation/intellij/04-directory.png)
5. Check the IDE version and directory and click "Download IDE and Connect"
![05-directory.png](/assets/documentation/intellij/05-confirm.png)
6. Wait till the IDE Gateway is downloaded and installed.
![06-downloading.png](/assets/documentation/intellij/06-downloading.png)
7. You can now from your PC work with the code located on the Raspberry Pi and run commands in the terminal.
![07-ide.png](/assets/documentation/intellij/07-ide.png)