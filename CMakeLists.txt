cmake_minimum_required(VERSION 3.10)
set(RTEMS_ROOT_PATH             "/mnt/sdb/rtems")
set(RTEMS_TOOLS_INSTALL_DIR     "${RTEMS_ROOT_PATH}/5")
set(RTEMS_TOOLS_BSP_LIB_DIR     "${RTEMS_ROOT_PATH}/5/arm-rtems5/lib")
set(RTEMS_KERNEL_INSTALL_DIR    "${RTEMS_ROOT_PATH}/5/arm-rtems5/beagleboneblack")
set(RTEMS_KERNEL_BSP_LIB_DIR    "${RTEMS_ROOT_PATH}/5/arm-rtems5/beagleboneblack/lib")

set(ENV{PATH} "${RTEMS_TOOLS_INSTALL_DIR}/bin:$ENV{PATH}")
set(RTEMS_TOOLS_BSP_INCLUDE_DIR       "${RTEMS_ROOT_PATH}/5/arm-rtems5/include")
set(RTEMS_KERNEL_BSP_INCLUDE_DIR      "${RTEMS_KERNEL_BSP_LIB_DIR}/include")
set(RTEMS_COMPILE_OPTIONS             "-B${RTEMS_KERNEL_BSP_LIB_DIR} -B${RTEMS_TOOLS_BSP_LIB_DIR} -specs bsp_specs -qrtems -mcpu=cortex-a8")

set(CMAKE_SYSTEM_NAME         Generic)
set(CMAKE_SYSTEM_PROCESSOR    arm)


set(CMAKE_C_COMPILER "arm-rtems5-gcc")
set(CMAKE_CXX_COMPILER "arm-rtems5-g++")

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE          "RelWithDebInfo"     CACHE STRING "")
endif()
set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS Debug RelWithDebInfo Release)

set(CMAKE_CXX_FLAGS_DEBUG             "${RTEMS_COMPILE_OPTIONS} -g"              CACHE STRING "")
set(CMAKE_CXX_FLAGS_RELWITHDEBINFO    "${RTEMS_COMPILE_OPTIONS} -g -O2"          CACHE STRING "")
set(CMAKE_CXX_FLAGS_RELEASE           "${RTEMS_COMPILE_OPTIONS} -O2 -DNDEBUG"    CACHE STRING "")

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(hello)

add_executable(HELLO example.cpp)
                           
target_include_directories(HELLO BEFORE PRIVATE
                           ${RTEMS_TOOLS_BSP_INCLUDE_DIR}                         
                           ${RTEMS_KERNEL_BSP_INCLUDE_DIR})
