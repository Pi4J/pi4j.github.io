---
title: Install Java and Tools
weight: 18
---

## Add Missing Dependencies

```shell
sudo apt install -y i2c-tools vim git java-common libxi6 libxrender1 libxtst6
```

## Install Java

### For 64-bit Operating System

```shell
mkdir -p ~/Downloads
cd ~/Downloads
wget https://cdn.azul.com/zulu/bin/zulu21.38.21-ca-jdk21.0.5-linux_arm64.deb
sudo dpkg -i zulu21.38.21-ca-jdk21.0.5-linux_arm64.deb
```

### For 32-bit Operating System

To be used when you selected a 32-bit version of the Operating System in the Imager tool

```shell
mkdir -p ~/Downloads
cd ~/Downloads
wget https://cdn.azul.com/zulu-embedded/bin/zulu17.52.17-ca-jdk17.0.12-c2-linux_aarch32hf.tar.gz
TODO
```

### Test Java Installation

Now you should be able to check the Java version with the following command:

```shell
$ java -version

```

## Install JavaFX

## Install SDKMAN and Other Tools

```shell
curl -s "https://get.sdkman.io" | bash
source .bashrc

sdk update

sdk install maven
sdk install jbang
```

