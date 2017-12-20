# Getting Started Developing on ev3dev

## Introduction

The LEGO Mindstorms EV3 Controller (better known as the EV3 Brick) is a Linux-based computing platform for interfacing with the various motors and sensors for the Mindstorms environment.

LEGO provides the EV3 Programmer software which uses graphical programming to develop programs to run on the EV3 Brick. However, these executables stored in `*.rxe` files are actually virtual machine bytecode files (conceptually similar to Java Bytecodes) that run on top of the LMS Virtual Machine.

Alternatively, others are interested in writing programs that execute directly on the Linux Operating System. Commercial solutions include `RobotC` which supports C programming for the EV3 Brick.

Nonetheless, since the EV3 Brick is based on Linux, we have various alternatives to commercially available tools.
This guide is meant primarily for people interested in writing code directly for the ev3dev Linux environment using open source tools.

# Choosing a Workflow and Toolchain

* C/C++
![C-CPP-Workflow](https://github.com/tcwan/ev3dev/blob/tcwan-wiki-swarch-1/images/workflow-c-cpp.flowchart.svg)
* ???
* TBD


# Software Pacakges for Host and Target Platforms

![Software Packages](https://github.com/tcwan/ev3dev/blob/ev3dev-wiki-1/images/ev3dev-software-packages.dot.svg?sanitize=true)
