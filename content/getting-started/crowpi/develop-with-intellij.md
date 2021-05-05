---
title: Develop with Intellij IDEA
weight: 62
---

In this tutorial, the development is implemented using the IntelliJ IDEA development environment. The articles, 
instructions and pictures are created accordingly. IntelliJ IDEA is from available Jetbrains in different versions. 
The community version already has enough functionality for development with the CrowPi. The development environment 
is available for Windows, MacOS and Linux, but NOT for Raspberry Pi. The download can be found here: Download IntelliJ IDEA. 
The subsequent setup of IntelliJ IDEA is also identical on all platforms.

## Clones des Repositories

As soon as we have installed the development environment, it is time to clone the entry-level project for the CrowPi.
The source code can be found on GitHub . In order to clone the repository, the corresponding link must be copied on GitHub 
and then imported into IntelliJ IDEA. Now step-by-step in pictures a more detailed instruction.

Visit CrowPi on GitHub and copy the link to clone as described in the picture. can. GitHub Clone Project

## Import the project

In the start window of IntelliJ is the option Get from VCSavailable. This must be selected so that the code can be cloned 
directly from GitHub. Then you can simply paste the link that was previously copied from GitHub. By confirming with Clone
the process is started and any necessary authentication of the user is carried out. Simply follow the instructions of the 
tool. Import from VCS Insert import from VCS link

As soon as the project has been completely cloned on the local computer, the project opens automatically in the development
environment. A small dialog pops up at the bottom right. This must be with Importmust be confirmed so that the repository 
can be properly initialized. Maven is a software project management tool. More information can be found in the Apache Maven Project . Basically, however, nothing needs to be changed. The CrowPi project already offers a complete setup and is easy to use. Import Maven Project

Importing the Maven project triggers a security warning at IntelliJ. This can easily be done with Trust project ... 
must be confirmed as long as the code comes from the official FHNW CrowPi repository. Trust Project confirmation

Now the last import step. So that errors can be searched for better later and the functions of the components can also
be analyzed very deeply, it is worthwhile with Maven Documentations and Sourcesto download. It's easy with a few clicks.
The Maven project menu is opened on the far right. Then by clicking on Download Sources and/or Documentation. Then in 
the context menu Download Sources and Documentationchoose. So all used libraries are locally available and visible. 
Now only the start configuration of the project is missing, which is described in the next section. IDownload Dependencies 
and Sources

## Setting the run configuration

The FHNW's CrowPi project uses 3 run configurations. These define which parts of the code are executed and how. 
However, there is no need to worry, because most of it is already predefined and all you have to do is enter the 
IP address of the Raspberry Pi. The following configurations are used:

* crowpi-examples [install]
* crowpi-examples [debug]
* Remote Debug

Copied in the process crowpi-examples [install] the current code on the Raspberry Pi. This works via a combination of 
SSH/SCP. The copied code is then started on the Raspberry Pi. crowpi-examples [debug]does nothing else in principle. 
However, other options are selected during the connection and a connection from a debugger is waited for before the 
application is actually executed. Remote Debugprovides exactly this debugger. This connects to the Raspberry Pi and 
troubleshooting can begin. You can find more information like this here: Starting and debugging on the CrowPi

So that everything works smoothly, the IP address of the Raspberry Pi must first be set as mentioned. To do this, 
click here and Edit Configurationschoose. As explained before, the IP address of the Raspberry Pi is displayed on 
the background image of the CrowPi. Select configuration menu

The dialog for setting the configurations now opens. A little hint: Wherever the IP address of the Raspberry Pi 
belongs there is already a placeholder Add CrowPi IP here. The three configurations

First will crowpi-examples [debug]confiurated. For this, as in the picture, the tab Runner open and then on Add CrowPi
IP heredouble click. The dialog window for typing in the IP address then opens. Briefly with OK confirm and press Apply 
to save. Settings debug

The second follows crowpi-examples [install]Configuration. This works exactly the same as that crowpi-examples 
[debug]Configuration. Exactly the same setting is required. Again with Apply to save. Settings Install

Now the last configuration follows Remote Debug. The menu is a bit different here. However, it is easier to use than 
the previous ones. Briefly in the field Hostenter the IP address of the Raspberry Pi. With OK exit the setting is
terminated. Remote Debug Settings

##  Erster Testlauf

It's done already. Everything is set up to start the CrowPi project for the first time directly from the development 
environment. In addition the run configuration crowpi-examples [install]choose. Then start the application by pressing 
the green play button. Start the application

It immediately opens that Run Fensterby IntelliJ. It takes a moment and some text is displayed on the command line. 
After a few seconds the output stops and it looks like this: Run Output von IntelliJ

A number can now be typed in here according to the instruction and with Enterbeeing confirmed. The corresponding 
sample application is then executed. If there are still error messages in the command line, it is worth checking 
the network connection of the computer and the Raspberry Pi again. There are also some tips and tricks for 
troubleshooting in the troubleshooting section of this tutorial. 