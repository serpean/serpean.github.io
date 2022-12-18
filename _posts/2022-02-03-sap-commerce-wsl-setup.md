---
layout:     post
title:      "SAP Commerce WSL Setup"
subtitle:   "Run Linux to compile and windows for everything else."
date:       2022-07-05 12:00:00
author:     "Sergio Pérez"
catalog: false
header-style: text
tags:
  - Linux
  - Sap Commerce
  - WSL
  - Window
---


This tutorial explains how to set up a Windows Subsystem for Linux 2 (WSL2) environment to work with SAP COMMERCE (also known as Hybris). WSL2 allows you to run a Linux environment directly on your Windows machine, which can be useful for development purposes. In this tutorial, we will cover how to install WSL2, set up a Java development environment with SDKMAN, install and configure Maven, configure the .bashrc file, set up an XServer for GUI applications, and install IntelliJ IDEA. By following these steps, you will be able to set up a fully functional development environment for working with SAP COMMERCE on your Windows machine.

## Install WSL2

Windows Subsystem for Linux (WSL) allows you to run a Linux environment directly on your Windows machine. WSL2 is the latest version of WSL, which offers improved performance and support for running Linux GUI applications.

Follow official Microsoft Manual Installation Steps documentation:

* [Install WSL on Windows 10 - Microsoft Docs](https://docs.microsoft.com/en-us/windows/wsl/install-win10#manual-installation-steps)

## Install JAVA with SDKMAN

Java is a popular programming language used in many projects, including SAP COMMERCE. In order to develop and run Java applications on your WSL2 environment, you will need to install a Java Development Kit (JDK).

SDKMAN is a tool that makes it easy to install and manage multiple versions of Java and other development tools on your system. In this tutorial, we will cover how to use SDKMAN to install and set up a Java development environment on your WSL2 environment. We will also explain how to switch between different Java versions and set the JAVA_HOME environment variable. By following these steps, you will be able to set up a Java development environment that is ready for use in your SAP COMMERCE projects.

1. Follow the official documentation [Installation - SDKMAN! the Software Development Kit Manager](https://sdkman.io/install)
2. Install SAPMachine JAVA 11 or above: `sdk install java 11.0.11-sapmchn`
3. Make it default java version.
4. Restart your terminal or execute `source ~/.bashrc`
5. Execute `echo $JAVA_HOME`. The result should be something similar to `/home/{user}/.sdkman/candidates/java/current`

> You can install other version of Java. You can list all your version (`sdk list java`) or switch between them using: `sdk use java <version>`

## Install Maven

Maven is a build automation tool commonly used in Java-based projects, including SAP COMMERCE. It helps manage dependencies, build, test, and deploy projects.

To install Maven on your WSL2 environment, follow the instructions on the Apache Maven website: [Maven – Installing Apache Maven](https://maven.apache.org/install.html).

You can verify that Maven has been successfully installed by running mvn -v in your terminal. This should display the version of Maven installed on your system.

## Configure .bashrc

The .bashrc file is a script that is executed whenever a new terminal session is started in a Linux or Unix-based system. It is used to set environment variables, define aliases, and execute other commands that you want to run every time you start a new terminal session.

In this tutorial, we will cover how to configure the .bashrc file in your WSL2 environment. Specifically, we will add several environment variables that are necessary for running GUI applications and other tools in your WSL2 environment. By following these steps, you will be able to customize your terminal environment to meet your specific needs and preferences.

1. Add the following variable above SDKMAN configuration (`~/.bashrc`)

```bash
export LIBGL_ALWAYS_INDIRECT=1
export LC_ALL=C
# xServer Configuration
export DISPLAY=$(cat /etc/resolv.conf | grep nameserver | awk '{print $2; exit;}'):0.0
```

2. Reload your terminal session:

```bash
source ~/.bashrc
```

## Install & Configure XServer

XServer is a software package that allows you to run graphical user interface (GUI) applications on a Linux or Unix-based system, such as WSL2. In this tutorial, we will cover how to install and configure XServer on your Windows machine, so that you can run GUI applications in your WSL2 environment.

Setting up XServer involves downloading and installing the software, and configuring the necessary environment variables and permissions. We will provide detailed instructions on how to do this in this tutorial. Once you have XServer set up, you will be able to run GUI applications in your WSL2 environment by forwarding the display to your Windows machine.

1. Download and install XServer (VcXsrv Windows X Server download)
2. Open XLaunch
![Open XLauch](/img/in-post/post-sap-commerce-wsl-setup/open-xlaunch.png)
3. XServer Configuration:
![Configuration 1](/img/in-post/post-sap-commerce-wsl-setup/configuration-1.png)
![Configuration 2](/img/in-post/post-sap-commerce-wsl-setup/configuration-2.png)
![Configuration 3](/img/in-post/post-sap-commerce-wsl-setup/configuration-3.png)
![Configuration 4](/img/in-post/post-sap-commerce-wsl-setup/configuration-4.png)
4. Click Finish.

> The created direct access must be executed after each PC restart.

Permitir la configuraicón de firewall de windows para esta aplicación
Allow Windows Firewall configuration allows this application:
![Windows Firewall Config](/img/in-post/post-sap-commerce-wsl-setup/windows-firewall-config.png)

## Install IntelliJ

IntelliJ IDEA is a popular integrated development environment (IDE) for Java and other programming languages. It offers a wide range of features for code editing, debugging, testing, and more. In this tutorial, we will cover how to install IntelliJ IDEA on your WSL2 environment and set it up for use in your SAP COMMERCE projects.

There are two options for installing IntelliJ IDEA on your WSL2 environment: using JetBrains Toolbox or directly installing the software. We will cover both options in this tutorial.

> Execute `idea` after installation in your terminal to open IntellIJ.

### Toolbox

1. [JetBrains Toolbox App: Manage Your Tools with Ease](https://www.jetbrains.com/toolbox-app/)
2. Allow toolbox to generate scripts

### Direct Install

1. Download IntelliJ IDEA: The Capable & Ergonomic Java IDE by JetBrains
2. `unzip ideaUI<version>.ZIP ideaUI`
3. `sudo mv ideaUI /opt`
4. Execute  `alias idea='/opt/ideaUI/bin/idea.sh > /dev/null 2> /dev/null'`
5. Execute `source ~/.bashrc`

In conclusion, setting up a WSL2 environment for development with SAP COMMERCE can be a useful way to work on projects on a Windows machine. By following the steps outlined in this tutorial, you can install WSL2, set up a Java development environment with SDKMAN, install and configure Maven, configure the .bashrc file, set up an XServer for GUI applications, and install IntelliJ IDEA. With these tools in place, you will have a fully functional development environment for working on SAP COMMERCE projects on your Windows machine. This setup can save you the hassle of setting up a separate Linux machine or using a virtual machine, and allows you to use the tools and applications you are most comfortable with.
