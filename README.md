# n32g031-cmake-template
A simple n32g031 cmake project template.

## Setup project
There are several ways to configure the toolchain:
- Install `arm-none-eabi-gcc` to `/usr/arm-none-eabi-gcc`. Project can automatically find toolchain.
- Pass in parameter `-DCMAKE_C_COMPILER=/path/to/bin/arm-none-eabi-gcc` to cmake.
- Pass in parameter `-DTOOLCHAIN_PATH="/path/to/GNU Arm Embedded Toolchain"` to cmake.
- Set toolchain directory to `TOOLCHAIN_PATH` environment variable.

### For CLion
1. Open [Settings - Build, Execution, Deployment - Toolchains](jetbrains://CLion/settings?name=Build%2C+Execution%2C+Deployment--Toolchains).
2. Add a new toolchain. Set up `C Compiler` and `C++ Compiler`.
3. Open [Settings - Build, Execution, Deployment - CMake](jetbrains://CLion/settings?name=Build%2C+Execution%2C+Deployment--CMake).
4. Add a new profile. Choose the correct toolchain.

## Custom ld or startup.s
Set `TARGET_LD_SCRIPT` and `TARGET_STARTUP_ASM` as your own before `add_subdirectory(sdk)`  
See: [CMakeLists.txt](CMakeLists.txt)

## License
See [LICENSE](LICENSE)
