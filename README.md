## RTEMS 5 CMake C++11 Starter
This repository contains a simple RTEMS application. 

The CMakeLists.txt targets a SPARC ERC32 BSP, as the one installed by following the official [Quick Start Guide](https://docs.rtems.org/branches/master/user/start/index.html) using the RSB method. 

:warning: **You need to manually adjust AT LEAST the second line of the CMakeFile to reflect your RTEMS_ROOT_PATH.**\
I suggest to also check all *_INSTALL_DIR, *_LIB_DIR, and *_INCLUDE_DIR to match your configuration.
