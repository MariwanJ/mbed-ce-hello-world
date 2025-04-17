#
# Mbed CE Hello World Project
# To compile this project, please change the target name inside the batch/bash script file, and run the script
#
cmake_minimum_required(VERSION 3.19)
cmake_policy(VERSION 3.19...3.22)

#Define project name : TODO Change the name 
set(PROJECT_NAME  "HelloWorld")
cmake_minimum_required(VERSION 3.19)
cmake_policy(VERSION 3.19)

# Initialize Mbed OS build system. 
# Note: This block must be before the project() call.
#### Initialize Mbed OS build system. ####
######################################################################################################
### Block of including .json5 files. Files of this block must be included before the app.cmake

#[[ Set path of mbed_app.json (necessary at all times) ]]
set(MBED_APP_JSON_PATH mbed_app.json5)

###--------------------------------------------------------------------------------------------------- 
#[[ This part is dedicated for custom targets only! The settings below activate targets from
    custom_targets.json5 and upload method config. If custom targets are not used the lines below should be commented. ]]

#[[ Here set path for custom_targets.json5 (this is our default) ]]
#set(CUSTOM_TARGETS_JSON_PATH custom_targets/custom_targets.json5)

#[[ Here you can set path for custom upload config .cmake (optional example) ]]
#set(CUSTOM_UPLOAD_CFG_PATH ${CMAKE_SOURCE_DIR}/${MBED_TARGET}/${MBED_TARGET}.cmake)

#[[ Note: For custom target you need also an upload method and we have few options how you can do that
    - use the variable CUSTOM_UPLOAD_CFG_PATH above to set the location of your config file
    - use the default expected path for custom targets upload method config file:
      MY_PROJECT/custom_targets/upload_method_cfg
    - of course you can set upload method parameters directly via cmake in this file
   For more visit https://github.com/mbed-ce/mbed-os/wiki/Upload-Methods ]]
   
### End of block
######################################################################################################

### Include Mbed toolchain setup file
include(mbed-os/tools/cmake/mbed_toolchain_setup.cmake)

# If you need any custom upload method configuration for your target, do that here
add_subdirectory(mbed-os) # Load Mbed OS build targets.  Must be added before any other subdirectories

#define libraries you are using here . 
set(LIB1 mbed-os)
# set(LIB2 mbed-netsocket) This is an example .. add your library list here 


# Link Mbed OS core library. This is called mbed-os when using the Mbed RTOS, and mbed-baremetal when using
# the bare metal version. This if statement checks to see which is in use and links it.
# Important: The mbed-os and mbed-baremetal libraries are object libraries, so they should ONLY be
# linked to executables, not to other libraries. Libraries should link to `mbed-core-flags` instead.
if("MBED_CONF_TARGET_APPLICATION_PROFILE=bare-metal" IN_LIST MBED_CONFIG_DEFINITIONS)
    set(LIB1  mbed-baremetal)
else()
    set(LIB1 mbed-os)
endif()

# Combine the libraries into one variable
# set(LIBRARIES_TO_LINK ${LIB1} ${LIB2}) This is an example .. add your library variables here one by one and should be defined before 
set(LIBRARIES_TO_LINK ${LIB1})


#Keep files inside /src directory
file(GLOB_RECURSE SOURCES
     src/*.cpp
     src/*.h
)

#Project name is based on the previous definition
# If you like, you can specify a version here, which CMake will make available in the ${PROJECT_VERSION} variable.
project(${PROJECT_NAME} 
		# VERSION 1.0.0
        LANGUAGES C CXX ASM) 

### Include Mbed project setup file
include(mbed_project_setup)

add_executable(${PROJECT_NAME} ${SOURCES})
######################################################################################################
### Link libraries block
#[[For more about this configuration visit wiki page MbedOS-configuration
https://github.com/mbed-ce/mbed-os/wiki/MbedOS-configuration#configuration-via-cmake-files]]
target_link_libraries(${PROJECT_NAME} ${LIBRARIES_TO_LINK}) # Can also link to mbed-baremetal here
mbed_set_post_build(${PROJECT_NAME}) # Must call this for each target to set up bin file creation, code upload, etc

# OPTIMIZATION OR DEBUG
#To generate debug info. Comment this if you want an optimized - relase version
target_compile_options(${PROJECT_NAME} PRIVATE -O0)
#unComment this if you want optimized version and comment the previos target_compile_options
# target_compile_options(${PROJECT_NAME} PRIVATE -O3)



# This generates build rules to generate bin/hex files, and to flash the code if you have configured an
# upload method.
mbed_set_post_build(${PROJECT_NAME})
#[[ Note: if you wish to use a custom linker script instead of the default Mbed one for
   your target, you can do that with mbed_set_post_build(${PROJECT_NAME} path/to/linker_script.ld) ]]

### End of block
######################################################################################################

