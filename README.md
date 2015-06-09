# STM32 ARM Eclipse OS X Tooling Support

## Install the Tooling We're Going To Use

###Install Xcode & install commandline tools

[https://itunes.apple.com/us/app/xcode/id497799835?mt=12](https://itunes.apple.com/us/app/xcode/id497799835?mt=12)

    $ xcode-select --install
    $ xcode-select -p

###Install homebrew

    $ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

###Modify BASH PATH to include any Homebrew installed binaries

    $ nano ~/.bashc

    export PATH=/usr/local/bin:/usr/local/sbin:$PATH

    $ source ~/.bashrc

###Install ST Link command line tools

    brew install stlink

###Install Oracle JVM 8

[http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

###Install GNU Tools for ARM Embedded Processors

[https://launchpad.net/gcc-arm-embedded/+download](https://launchpad.net/gcc-arm-embedded/+download)

    $ cd ~/Downloads
    $ mkdir ~/arm_tools
    $ tar -xjvf gcc-arm-none-eabi-*-mac.tar.bz2 -C ~/arm_tools/
    $ ls -la ~/arm_tools/

###Install Eclipse Luna (4.4) with CDT
[https://www.eclipse.org/downloads/](https://www.eclipse.org/downloads/)

###Install GNU ARM Eclipse Tools
[http://gnuarmeclipse.sourceforge.net/updates](http://gnuarmeclipse.sourceforge.net/updates)

###Install EmbSysRegView Eclipse Plugin
[http://embsysregview.sourceforge.net/update](http://embsysregview.sourceforge.net/update)

###Modify BASH PATH variable to find ARM tools & openocd

    $ nano ~/.bashrc

    export PATH=$PATH:"$HOME/arm_tools/gcc-arm-none-eabi-*/bin"
    export PATH=$PATH:"/Applications/GNU ARM Eclipse/OpenOCD/0.9.0-201505191004/bin"

    $ source ~/.bashrc


##Create Example Blinky Project To Verify Tooling Install 

-    Open Eclipse
-    Create New Project


####Post Build Commands
    ${cross_prefix}objcopy -O srec ${ProjName}.${BuildArtifactFileExt} ${ProjName}.s19 ; ${cross_prefix}objcopy -O binary ${ProjName}.${BuildArtifactFileExt} ${ProjName}.bin


##Debug via Command Line
    $ STLINK_DEVICE="0x0483:0x374b" st-util

    $ arm-none-eabi-gdb Debug/blinky.elf
    $(gdb) target extended-remote :4242
    $(gdb) load
    $(gdb) continue


##Flash Release Build via Command Line
    st-flash write Release/blinky.bin 0x8000000
