# Organization of ev3dev Repositories

The ev3dev Repositories in GitHub consists of the following major components:
* Components related to EV3 Programmer /LMS Bytecode Support (EV3 Programmer Software Compatible)
> EV3 Programmer support cannot be used concurrently with the rest of the ev3dev development environment
* Components related to Linux-based Programming Support (ev3dev Distribution)
* Linux Kernel Sourcecode Repositories (Platform Specific Linux Kernel)
> The relevant kernel repository depends on the EV3 Controller Hardware Platform (choose *ONE* appropriate kernel)

![Image](https://github.com/tcwan/ev3dev/blob/ev3dev-wiki-1/images/ev3dev-related-repositories.dot.svg?sanitize=true)

## Linux-based Programming Components

### Common components

The `lego-linux-drivers` repository hosts the Linux SysFS-based I/O routines for accessing the motors and sensors used by ev3dev. Most I/O will take place using the SysFS interface under the `/sys/class/` virtual filesystem. This allows for user space drivers to be written easily for reading information from the sensors, for example. 

> SysFS is classified as User-space I/O where the actual data transfers with the device take place via pseudo-files found under `/sys/class` using normal file manipulation routines such as `open()`, `read()`, `write()`, and `close()`. This is different from kernel mode I/O where data transfers take place inside a interrupt handler specifically written for a kernel module running within the kernel context.
>
> The disadvantage of using SysFS is that I/O response time would be slower than if a dedicated kernel driver were available. The advantage of SysFS is that interrupt handling routines do not need to be written by the user.

### Language-specific Components

The important repositories listed here are the Language Bindings which provide the Application Programming Interface (API) to `ev3devKit`, which provides a standard set of function modules for application developers. The ev3dev project maintains several standard Language bindings for the GObject/GLib-based `ev3devKit` library, which can be automatically updated for all supported languages easily when new APIs are developed.

Alternatively, third party Language Bindings and support libraries are available for several languages. These  do not use the `ev3devKit` libraries but provide their own API and libraries for writing programs. 

Nonetheless, all of them depend on `lego-linux-drivers` to actually interface with the sensors and motors.

### Higher level Components

Included in this category are the Graphics libraries, based on GRX 3, and the Vision libraries for use with the Pixy and NXTCam4/5 cameras.

In addition, a version of the Python interpreter `micropython` has been ported and is maintained by the ev3dev project to support Python-based development.

## EV3 Programmer Components

### lmsasm

LMS Bytecode Assembler to generate bytecode output for the LMS Virtual Machine

### lms-hacker-tools

LMS Bytecode Disassembler. Given a .rxe file, convert it into a LMS instruction stream

### lms2012-compat

This is the LMS Virtual Machine subsystem that is derived from the official LEGO Firmware.

## Linux Kernel Sourcecode Repositories

There are several Linux kernel repositories maintained by ev3dev.org.
* ev3-kernel: This tracks the Debian mainline kernel, and is meant for use with the LEGO Mindstorms EV3 Controller (EV3 Brick)
* bb-kernel: This kernel is derived from the Beagleboard.org maintained kernel, and is meant for use with the Beaglebone Controller
* rpi-kernel: This kernel is derived from the Raspberry Pi Foundation maintained kernel, and is meant for use with the RPi Controller
* Other kernels may be added in the future given sufficient interest and support by the platform for interfacing with LEGO Mindstorms sensors and motors