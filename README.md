# Mbed CE Hello World using Batch/bash files with Eclipse tutorial
This project implements a basic hello world using Mbed OS Community Edition.  Use it as an example or a starting place for your own projects!
Use the batch or bash file to compile. You need to change the project name inside the CMakeList.txt file. Under /src you can put your project files.

## How to set up this project:

1. Clone it to your machine.  Don't forget to use `--recursive` to clone the submodules: `git clone --recursive https://github.com/MariwanJ/mbed-ce-hello-world `
2. You may want to update the mbed-os submodule to the latest version, with `cd mbed-os && git pull origin master`
3. Set up the GNU ARM toolchain (and other programs) on your machine using [the toolchain setup guide](https://github.com/mbed-ce/mbed-os/wiki/Toolchain-Setup-Guide).
4. Set up the CMake project for editing.  We have three ways to do this:
    - On the [command line](https://github.com/mbed-ce/mbed-os/wiki/Project-Setup:-Command-Line)
    - Using the [CLion IDE](https://github.com/mbed-ce/mbed-os/wiki/Project-Setup:-CLion)
    - Using the [VS Code IDE](https://github.com/mbed-ce/mbed-os/wiki/Project-Setup:-VS-Code)
5. Build the `flash-HelloWorld` target to upload the code to a connected device.
6. Batch or Bash files uses 20 threads for compiling source code. Increase or decrease that as you wish (-j 20)

## This Version: 
I made some changes in the structure of the files. i.e. your project files should be inside the folder /src. IMHO project files shouldn't be in the root of the project.
I also added a pdf that will let you configure Eclipse to compile, debug your project. Using OpenOCD, your bin will be uploaded automatically when you debug. 
Otherwise, you can just copy the bin file into the virtual Nucleo flash memory that will install the bin inside the Nucleo module. Or you can use stm32 utility to upload the project.
I don't have other boards, or other modules. You might update this readme and contribute with this version to make it more general.

Mbed studio, or Visual studio code, IMHO, is not a proper IDE for debugging mbed projects. Feel free to contribute to this copy or the original. 

## Notes:
- Inside your cpp file under /src do not use #include <balbla.h> , you should write the include with quotation marks .i.e. #include "balbla.h".
- You must include the libraries you use in the cmake file. I updated the cmake file and put place and note how to do so. Look at the documentations also here https://github.com/mbed-ce/mbed-os/wiki/MbedOS-configuration#configuration-via-cmake-files
- The PDF shows you how to configure Eclipse for debugging and for compiling. Please notice that the pictures inside the pdf is for a project based on NUCLEO-F207ZG. Try to change the names, script files..etc. to your HW. OpeOCD scritp could be either written or found on the net if you cannot find it. I made the script for F2X. Board by myself. OpenOCD doesn’t provide that by default.