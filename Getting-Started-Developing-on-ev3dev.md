# Getting Started Developing on ev3dev

## Introduction

The standard LEGO Mindstorms EV3 Controller (better known as the EV3 Brick) is a Linux-based computing platform for interfacing with the various motors and sensors for the Mindstorms environment.

LEGO provides the EV3 Programmer software which uses a graphical programming paradigm, originating from National Instruments' LabView platform, to develop programs to run on the EV3 Brick. However, these executables stored in `*.rxe` files are actually virtual machine bytecode files (conceptually similar to Java Bytecodes) that run on top of the LMS Virtual Machine.

Alternatively, others are interested in writing programs that execute directly on the EV3 Brick, bypassing the LMS Virtual Machine. Commercial solutions include [`RobotC`](http://www.robotc.net/) which supports C programming for the EV3 Brick (Q: Does the Robot-C custom firmware support `*.rxe` execution?).

Nonetheless, since the EV3 Brick Operating System is based on Linux, we have various alternatives to commercially available tools. ev3dev provides a Debian-based Linux distribution to support people interested in writing code directly for the Linux environment using open source tools. This also opens up the possibility of using other EV3 Controllers such as the Raspberry Pi, Beaglebone boards (with appropriate motor and sensor expansion capes)`, and others which have higher processing capabilities compared to the EV3 Brick to run software written for the ev3dev distribution.

The basic process to start developing on ev3dev is as follows:
1. [Choose a Language](@choosing-a-language)
2. [Choose a Workflow and Toolchain](#choosing-a-workflow-and-toolchain)
3. [Build the Libraries](#building-the-libraries)
4. [Write your Programs](#writing-your-programs)
5. [Download Program to Target and Debug/Run the Program](#downloading-and-debugging-programs)

# Choosing a Language

While it is a bit daunting to start by choosing a [Programming Language](http://www.ev3dev.org/docs/programming-languages) if you're new to programming, the list of languages are more or less sorted from easiest for beginners such as Python and Javascript, to more advanced options such as C++ and C.

# Choosing a Workflow and Toolchain

## Workflow Introduction

>This mostly applies to more advanced language options. 

For Python and Javascript, almost everything is already built-in to the ev3dev distribution; all you need is an Editor or Integrated Development Environment (IDE) to write your programs in, and then execute it on the EV3 Controller (after downloading if necessary).

> The pre-built ev3dev image has everything you need, unless you're interested in installing non-standard library packages into the ev3dev image (this is an advanced topic which is not covered in this guide). 

For the other languages, there is a need to compile the source files into executable files that will be run on the EV3 Controller. Technically, it is possible to write and compile programs on the EV3 Controller platform, but that would be an exercise in frustration except for compiling trivial programs such as `Hello World!`. 

Typically we would want to use our Host PC to write, compile and debug the program, since it is much more powerful than the EV3 Controller platform. However, the EV3 Controller uses a different CPU or Instruction Set compared with the ones typically used on your PC. 

>More specifically, the available EV3 Controllers are ~~almost~~ all based on the ARM CPU Architecture, while the PC are (almost) all based on the x86 or x64 (Intel-Architecture compatible) CPU Architecture.

Bytecode based languages such as the LEGO Programmer and Java will have Compilers that compile the source programs into Virtual Machine bytecodes, which is able to run on any platform having the appropriate Virtual Machine software. However, the default C and C++ compilers for the PC platform targets the x86 or x64 CPU Architecture, and cannot be run on the EV3 Controller. 

Consequently, when compiling C and C++ programs on the PC to run on the EV3 Controller, we need to perform [Cross Compilation](https://en.wikipedia.org/wiki/Cross_compiler). The C and C++ cross compilers used by ev3dev are based on the GNU Compiler Collection ([`GCC`](https://gcc.gnu.org/)).

> It is important to select the correct Target environment for the cross compiler; otherwise the generated programs will not be able to run on the targeted EV3 controller platform. Generally we should use a generic Cross-Compiler which can generate executables for multiple target architectures. 
>
>However, if you're building on the Target platform natively, or else intend to run the architecture specific cross-compiler under emulation on the Host to build with custom libraries which are only available for the given target architecture, GCC provides architecture specific compiler and cross-compiler toolchains that takes less disk space compared with the multi-target cross-compilers.

When cross-compiling using a GCC Cross-Toolchain, the selected target architecture *MUST* be compliant with the chosen EV3 Controller platform distribution (EV3 Brick, RPi, etc.), otherwise unexpected problems may occur. There are two [Target Architectures](https://www.debian.org/ports/arm/) for ARM-based Debian distributions used by ev3dev depending on the Controller hardware platform:
> * armel (for XXX)
> * armhf (for YYY)

## Toolchain Selection

You can use the following Toolchain Selection Guide for your chosen programming languages as a reference:
* [Python](http://www.ev3dev.org/docs/tutorials/setting-up-python-pycharm/)
* C/C++
![C-CPP-Workflow](https://github.com/tcwan/ev3dev/blob/tcwan-wiki-swarch-1/images/workflow-c-cpp.flowchart.svg)
* ???
* TBD

## Software Packages for Host and Target Platforms

It is important to keep in mind that you're dealing with two separate Operating Systems environments when developing software for the EV3, the **Host** (PC) environment and the **Target** (EV3) environment. The **Host** environment typically would be based on Windows, macOS, or Linux Operating Systems, while the **Target** will be based on the Debian Linux-derived ev3dev Distribution. Nonetheless, the following discussion assumes the use of a [POSIX compliant](https://en.wikipedia.org/wiki/POSIX) environment for the **Host**. 

![Software Packages](https://github.com/tcwan/ev3dev/blob/ev3dev-wiki-1/images/ev3dev-software-packages.dot.svg?sanitize=true)

### Host Packages

The essential components for developing on the Host are:
* [Integrated Development Environment](https://en.wikipedia.org/wiki/Integrated_development_environment) (IDE) or Editor
* Cross-compiler Toolchain
>ev3dev has packaged the relevant GCC Cross-compiler Toolchain in [Docker](https://www.docker.com/what-docker) containers to simplify the installation of a POSIX-compliant development environment for the Host.
* Project Build Tools (we assume the use of [Makefiles](https://en.wikipedia.org/wiki/Makefile) for managing compilation)
* Remote Access program (we assume use of [OpenSSH client](https://en.wikipedia.org/wiki/OpenSSH) to login to the EV3 Platform remotely)
* Executable Program Downloader from PC to Target (e.g., OpenSSH provides `scp` (Secure Copy) for transferring files)
* Cross-Debugger (usually comes with the Cross-compiler Toolchain, but can also be provided as part of the IDE)

In addition, several build tools are provided for building ev3dev Distribution Boot images or GCC Cross-compiler toolchains for Docker. 
>These build tools are not needed unless you plan to create custom toolchains or custom ev3dev Distribution images.

### Target Packages
* Platform specific Kernel
* 

>Take a look at [Organization of ev3dev Repositories](ev3dev-Repositories) for more information regarding the packages maintained by the ev3dev project.

# Building the Libraries

## Clone the Language-specific Repository

Based on the chosen [Programming Language](http://www.ev3dev.org/docs/programming-languages) and toolchain, the specific repository should be cloned to your Host (PC) platform


# Writing Your Programs

TBD

# Downloading and Debugging Programs

TBD