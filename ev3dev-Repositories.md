# Organization of ev3dev Repositories

The ev3dev Repositories in GitHub consists of the following major components:
* Components related to Linux-based Programming
* Components related to EV3 Programmer (LMS Bytecode)
> EV3 Programmer support cannot be used concurrently with the rest of the ev3dev development environment
* Linux Kernel Sourcecode Repositories

![Image](https://github.com/tcwan/ev3dev/blob/ev3dev-wiki-1/images/ev3dev-related-repositories.dot.svg?sanitize=true)

## Linux-based Programming Components

TBD

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