# Eclipse IDE

Eclipse is a comprehensive Integrated Development Environment by Eclipse Foundation, Inc. For C/C++ development, we will use the [Eclipse CDT build](http://www.eclipse.org/downloads/packages/eclipse-ide-cc-developers/oxygen3). The current version of the Eclipse platform is Oxygen.

The focus of this guide is to configure Eclispe for C cross-development and debugging using the [ev3dev-c](https://github.com/in4lio/ev3dev-c) libraries for the LEGO Mindstorms EV3 Controller. The steps should be similar for the other Robot Controller platforms except for ARM-architecture specific toolchain settings.

## Docker Cross-Compilation Image Setup

The cross-compilation process will be performed using [Docker](https://www.docker.com/community-edition), to ensure that the build environment libraries for linking with our programs are consistent with the ev3dev distribution libraries. 

Information about the ev3dev cross-compilation docker images are found [here](../toolchains/c-cpp-toolchains.md).

Setup the Docker Environment, and install the appropriate ev3dev docker image based on the version of the ev3dev distribution you're targeting.

To refer to the docker image in Eclipse, we'll tag it as `ev3cross`

```
$ docker tag <docker_cross_compiler_image> ev3cross
```

## Additional Eclipse Plugins

Two additional Eclipse Plugins need to be installed from the Eclipse Marketplace:
* Eclipse Docker Tooling (works with Eclipse Oxygen release and later)
* GNU MCU Eclipse

![Eclipse Plugins](../../images/pics/eclipse-marketplace-installed-tools.png)

## Creating new ev3dev-c project in Eclipse

To get started, we'll create an ARM "Hello World" project in Eclipse.
In Eclipse, select `File->New->C Project`. Choose the `Hello World ARM C Project` from the list.

![ARM Project](../../images/pics/new-c-project-arm.png)

This will automatically configure the build environment to use the ARM Cross GCC Tools. After pressing `Next >`  it will then prompt you for the Cross GCC Toolchain to use. In our case, we will need to use the Custom option since the others are not relevant for our configuration (though we will need to modify the toolchain prefix later).

![Custom Toolchain](../../images/pics/custom-cross-toolchain.png)

When you press `Finish` a new project and main.c will be created.

## Configuring Project Settings

The Build Settings for the newly created project needs to be updated next.
First, select the newly created project folder. If you don't do this Eclipse will not know which project configuration it needs to modify.

Then, select `Project->Properties` and then expand the parameter list for `C/C++ Build->Settings`. This should display the `Tool Settings` tab. 

### Configuring Target Processor

Under `Target processor`, select the appropriate ARM family. For the LEGO Mindstorms EV3, it is `arm926ej-s`. The architecture and instruction set should be set to `Toolchain default`

![Custom Toolchain](../../images/pics/c-project-build-settings-tool-settings.png)

### Configuring Linker Parameters

Then the Linker `Miscelleanous` setting should be configured. The GNU MCU Plugin assumes the use of bare-metal debugging setup and hence includes reference to rdimon. This is not used for ev3dev. References to `rdimon.specs` and `rdimon` should be removed.

![Custom Linker](../../images/pics/c-project-build-settings-tool-settings-linker-misc.png)

After removing references to rdimon, you can verify the updated Linker settings by selecting the Linker overall settings.

![Linker Overall Settings](../../images/pics/c-project-build-settings-tool-settings-linker-overall.png)

### Configuring Cross Toolchain prefix
Configuring the Cross Toolchain prefix is the following step.
As mentioned previously, `arm-none-eabi-` is not the correct cross-compilation toolchain prefix for `ev3dev`. Instead, it should be set to `arm-linux-gnueabi-`. In addition, we should uncheck the `Create Flash Image` option since we're not going to flash it to the robot controller.

![Cross Toolchain](../../images/pics/c-project-build-settings-toolchains.png)

### Configuring Docker Settings

Next the build needs to be setup to target the Docker container. Switch to the `Container Settings` tab. The checkmark `Build inside Docker Image` should be checked. In addition the name of the Docker Image can be selected from the drop down menu (assuming that it was configured and tagged properly for Docker previously).

![Docker Settings](../../images/pics/c-project-build-settings-container-settings.png)


## Building Cross-Compilation Project Using Docker

Once all that is done, the next step is to build the project. 
With the project folder selected in the Project Explorer View, initiate a `Project->Build Project` action. The Eclipse console should display the progress of the build.

![Build Status](../../images/pics/c-project-build-console-status.png)

## Remote Debugging Using Eclipse

TBD
