# Getting Started Developing on ev3dev

## Introduction

The LEGO Mindstorms EV3 Controller (better known as the EV3 Brick) is a Linux-based computing platform for interfacing with the various motors and sensors for the Mindstorms environment.

LEGO provides the EV3 Programmer software which uses graphical programming to develop programs to run on the EV3 Brick. However, these executables stored in `*.rxe` files are actually virtual machine bytecode files (conceptually similar to Java Bytecodes) that run on top of the LMS Virtual Machine.

Alternatively, others are interested in writing programs that execute directly on the EV3 Brick, bypassing the LMS Virtual Machine. Commercial solutions include [`RobotC`](http://www.robotc.net/) which supports C programming for the EV3 Brick.

Nonetheless, since the EV3 Brick Operating System is based on Linux, we have various alternatives to commercially available tools. ev3dev provides a Debian-based Linux distribution to support people interested in writing code directly for the Linux environment using open source tools. This also opens up the possibility of using other Controllers such as the Raspberry Pi, Beaglebone boards, and others which have higher processing capabilities compared to the EV3 Brick Controller to run the software written for the ev3dev distribution.

The basic process to start developing on ev3dev is as follows:
1. [Choose a Language](@choosing-a-language)
2. [Choose a Workflow and Toolchain](#choosing-a-workflow-and-toolchain)
3. [Build the Libraries](#building-the-libraries)
4. Write your programs
5. Download program to Target and debug/run the program

# Choosing a Language

While it is a bit daunting to start by choosing a [Programming Language](http://www.ev3dev.org/docs/programming-languages) if you're new to programming, the list of languages are more or less sorted from easiest for beginners such as Python and Javascript, to more advanced options such as C++ and C.

# Choosing a Workflow and Toolchain

>This mostly applies to more advanced language options. 

For Python and Javascript, almost everything is built-in to the ev3dev distribution already, and all you need is an Editor or Integrated Development Environment (IDE) to write your programs in, and then execute it on the EV3 Controller (after downloading if necessary).

> The pre-built ev3dev image has everything you need, unless you're interested in installing non-standard library packages into the ev3dev image (this is an advanced topic which is not covered in this guide). 

For the other languages, there is a need to compile the source files into executable files that will be run on the EV3 Controller. Technically, it is possible to write and compile programs on the EV3 Controller platform, but that would be an exercise in frustration except for compiling trivial programs such as `Hello World!`. 

Typically we would want to use our Host PC to write, compile and debug the program, since it is much more powerful than the EV3 Controller platform. However, the EV3 Controller uses a different CPU or Instruction Set compared with the ones typically used on your PC. 

>More specifically, the EV3 Controller are (almost) all based on the ARM CPU Architecture, while the PC are (almost) all based on the x86 or x64 (Intel-compatible) CPU Architecture.

Bytecode based languages such as the LEGO Programmer and Java will have Compilers that compile the source programs into Virtual Machine bytecodes, which is able to run on any platform having the appropriate Virtual Machine software. However, the default C and C++ compilers for the PC platform targets the x86 or x64 CPU Architecture, and cannot be run on the EV3 Controller. 

Consequently, when compiling C and C++ programs on the PC to run on the EV3 Controller, we need to perform [Cross Compilation](https://en.wikipedia.org/wiki/Cross_compiler). The C and C++ cross compilers used by ev3dev are based on the GNU Compiler Collection ([`GCC`](https://gcc.gnu.org/)).

> It is important to select the correct Target environment for the cross compiler; otherwise the generated programs will not be able to run on the targeted EV3 controller platform. There are two [Target Architectures](https://www.debian.org/ports/arm/) for ARM-based Debian distributions used by ev3dev depending on the Controller board. The appropriate GCC Cross-Toolchain *MUST* be used to generate the binary executables to avoid unexpected problems:
> * armel (for XXX)
> * armhf (for YYY)

You can use the following selection process for your chosen programming languages as a guide:
* [Python](http://www.ev3dev.org/docs/tutorials/setting-up-python-pycharm/)
* C/C++
![C-CPP-Workflow](https://github.com/tcwan/ev3dev/blob/tcwan-wiki-swarch-1/images/workflow-c-cpp.flowchart.svg)
* ???
* TBD

# Building the Libraries

## Clone the Language-specific Repository

Based on the chosen [Programming Language](http://www.ev3dev.org/docs/programming-languages) and toolchain, the specific repository should be cloned to your Host (PC) platform

## Software Pacakges for Host and Target Platforms

![Software Packages](https://github.com/tcwan/ev3dev/blob/ev3dev-wiki-1/images/ev3dev-software-packages.dot.svg?sanitize=true)

# Building the Libraries
