---
title: Install Java and Tools
weight: 18
---


```shell
sudo apt install -y i2c-tools vim git java-common libxi6 libxrender1 libxtst6
curl -s "https://get.sdkman.io" | bash
source .bashrc
sdk install maven

mkdir -p ~/Downloads
cd ~/Downloads
wget https://cdn.azul.com/zulu/bin/zulu21.34.19-ca-jdk21.0.3-linux_arm64.deb
sudo dpkg -i zulu21.34.19-ca-jdk21.0.3-linux_arm64.deb
```

As we have put the Full edition on the SD card, Java is already available. Open a terminal window and type in `java -version`.
Java will be started to show you the installed version.

```shell
$ java -version
openjdk version "11.0.9" 2020-10-20
OpenJDK Runtime Environment (build 11.0.9+11-post-Raspbian-1deb10u1)
OpenJDK Server VM (build 11.0.9+11-post-Raspbian-1deb10u1, mixed mode)
```
