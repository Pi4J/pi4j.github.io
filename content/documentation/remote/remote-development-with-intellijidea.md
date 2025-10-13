---
title: Using IntelliJ IDEA
weight: 171
tags: ["IntelliJ IDEA"]
---

IntelliJ IDEA is the most-used IDE for Java development. You can use it to develop on a remote machine with code on the Raspberry Pi. Make sure you have the Remote Development Gateway plugin enabled as described on [Connect to a remote server from IntelliJ IDEA](https://www.jetbrains.com/help/idea/remote-development-starting-page.html) and [Install JetBrains Gateway﻿](https://www.jetbrains.com/help/idea/jetbrains-gateway.html).

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