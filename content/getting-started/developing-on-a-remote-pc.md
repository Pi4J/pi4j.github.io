---
title: Developing on a remote PC
weight: 45
---

{{% notice note %}}
GITHUB PROJECT: [https://github.com/Pi4J/pi4j-maven-archetype](https://github.com/Pi4J/pi4j-maven-archetype)
{{% /notice %}}

## Developing Java programs using a remote PC workstation

Writing your Java program, compiling and running it directly on the Raspberry Pi board
as shown in the previous chapter is perfectly fine, of course,
but there is an alternative way to arrange your developing laboratory, using a normal 
desktop computer as Remote Developing Workstation (RDW).

This [Maven Archetype](https://github.com/Pi4J/pi4j-maven-archetype "raspimaven-archetype") will give you
a tool to generate Pi4J-V2 skeleton Java projects. You can use it for your next Pi4j project and you will be able 
to develop your program on the remote workstation (RDW), compile them, transmit the executable 
code on the target Pi board and run it. You can also start a remote debugging session.

There are some pros. and cons. in such a developing arrangement:

- Pros:
    - Your RDW has much more resources like memory, disk capacity and CPU power
than a Raspberry Pi, and this is true for a P4 model too. You can store all your programs in the
desktop computer.
    - You do not have to install on the Raspberry Pi the Visual Studio Code (or your preferred IDE program),
the Java JDK (JRE it is enough), Maven and the other development tools.
    You do not need to connect the screen, the keyboard and the mouse to the Raspberry Pi
    - You can use smaller PI models
- Cons:
    - You can't run Web applications (using a web container like Tomcat or similar)

## Setting up
### Configure the RPi for Headless mode
The _Headless Mode_ configuration enables the RPi board to communicate with the RDW over SSH protocol.
These are the needed steps:
- Check if the RDW is equipped with a SSH Client. If the RDW OS is Linux you already have it 
- For Windows you can use _putty_, _MobaXterm_ or you can enable the (new) OpenSsh Client porting on Windows 10
- Connect both the RPi and RDW to your local network
- Follow [this guide](https://www.raspberrypi.org/documentation/configuration/wireless/headless.md "Setting up a Raspberry Pi headless") 
to configure your RPi 
- Install the Maven tool on the RDW

You should now be able to open a SSH Terminal window on RDW and to remotely login on the RPi board.
### Install the _raspimaven-archetype_
- Goto the [Github Pi4J Project](https://github.com/Pi4J/pi4j-maven-archetype "raspimaven-archetype") and download the project
clicking on the green _Code_ button and selecting _Download ZIP_
- Unzip the archetype file in an empty folder, let say _my-folder_
- `cd my-folder/raspimaven-archetype`
- `mvn install`

_Congratulation ! - Now you are ready to generate your first **Project Template**_

### Generate a new Project Template
Let suppose you want to begin the new wonderful PI4J-V2 project _my-project_, to do this follow these steps:
- `mkdir my-project`
- `cd my-project`
- `mvn archetype:generate -DarchetypeCatalog=local`
- answer to the questions the archetype asks you (see below for details)
### Configuring your new project
Before starting the new project generation, the archetype asks some configuration data. The list of question
and the replies are shown here below:
1. _Choose archetype:_ **select the _raspimaven-archetype_ from the list proposed**
1. _Define value for property 'groupId':_ **choose the Maven groupId for your project.** (If don't know what is a groupId, don't worry, just type _"com.example"_ for now)
1. _Define value for property 'artifactId':_ **choose a name for the program executable your project will produce**
1. _Define value for property 'version':  1.0-SNAPSHOT:_ **type Enter to accept the default value shown, or type the initial program version, something like _1.0.0_**
1. _Define value for property 'package':  com.example:_ **type Enter to accept the default value shown**

The archetype now shows you a summary of the configuration parameters you have just typed in, plus the values proposed for the _main-class_ and _package_ parameters.
If the list is ok for you, reply _Y_ to accept, otherwise reply _N_ to change one or more values (you will have to re-type all parameter values ...)

After the list confirmation, the archetype generates a new maven project template for you. 

**Congratulations** 

You should be able to open the new project with your preferred java IDE. The IDE should be able
to recognize the project as a valid Maven project.
### Explore the new project template
Feel free to explore the new project familiarizing with the folder structure. These are the most important features:
- The file README.md contains the intruction to configure the connection(s) to your RPi board(s) and the decription of the Maven
commands to build your project, transfer the executable code to the target RPi, run it and also open a debugger session.
- The _pom.xml_ file already includes the dependencies needed to compile your program with the JPi4J-V2 libraries.
- The _platform_ folder contains an example configuration file for connecting to you RPi board. Read the README.md explanation,
open the _platform/raspberry.properties_ file (or copy it to a new file) and edit it to describe how to connect to your RPi

