cmake_minimum_required(VERSION 3.10)
include(cmake/toolchain.cmake)

project(n32g031_template)

enable_language(C)
enable_language(CXX)
enable_language(ASM)

# Custom linker script
set(TARGET_LD_SCRIPT ${CMAKE_SOURCE_DIR}/ld/n32g031_flash.ld)
# Custom startup
set(TARGET_STARTUP_ASM ${CMAKE_SOURCE_DIR}/startup/startup_n32g031_gcc.s)

# Add N32G031 SDK
add_subdirectory(sdk)

# Add project sources
add_executable(n32g031_template src/main.c src/n32g031_it.c)
target_include_directories(n32g031_template PUBLIC src)

target_link_libraries(n32g031_template N32G031_SDK)

# Generate .bin and .hex
generate_binary_file(n32g031_template)
generate_hex_file(n32g031_template)
