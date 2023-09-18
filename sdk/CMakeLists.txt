cmake_minimum_required(VERSION 3.10)

set(N32G031_CMSIS_PATH ${CMAKE_CURRENT_LIST_DIR}/N32G031_CodeLib/firmware/CMSIS)
set(N32G031_PERIPHERAL_PATH ${CMAKE_CURRENT_LIST_DIR}/N32G031_CodeLib/firmware/n32g031_std_periph_driver)

# Peripheral Driver
file(GLOB N32G031_PERIPHERAL_SRCS ${N32G031_PERIPHERAL_PATH}/src/*.c)

# CMSIS
set(TARGET_C_SOURCES
        ${N32G031_CMSIS_PATH}/device/system_n32g031.c
        ${N32G031_PERIPHERAL_SRCS}
        )

set(TARGET_C_INCLUDES
        ${N32G031_CMSIS_PATH}/core
        ${N32G031_CMSIS_PATH}/device
        ${N32G031_PERIPHERAL_PATH}/inc
        )

# Shared library and linker script search paths
set(TARGET_LIB_DIRECTORIES
        ${N32G031_PERIPHERAL_PATH}/inc
        )

if (NOT TARGET_STARTUP_ASM)
    message(FATAL_ERROR "Must set TARGET_STARTUP_ASM to locate startup asm")
endif ()
message(STATUS "Use startup asm: " ${TARGET_STARTUP_ASM})

if (NOT TARGET_LD_SCRIPT)
    message(FATAL_ERROR "Must set TARGET_LD_SCRIPT to locate ld script")
endif ()
message(STATUS "Use LD script: " ${TARGET_LD_SCRIPT})

add_library(N32G031_SDK STATIC ${TARGET_C_SOURCES} ${TARGET_STARTUP_ASM})

# Shared sources, includes and definitions
target_compile_definitions(N32G031_SDK PUBLIC ${TARGET_C_DEFINES})
target_include_directories(N32G031_SDK
        PUBLIC ${TARGET_C_INCLUDES}
        INTERFACE ${TARGET_C_INCLUDES}
        )

target_link_directories(N32G031_SDK PUBLIC ${TARGET_LIB_DIRECTORIES})
target_link_libraries(N32G031_SDK PUBLIC "c" "m" "nosys")
target_link_options(N32G031_SDK
        PUBLIC "-T${TARGET_LD_SCRIPT}"
        PUBLIC "-Wl,-Map=${CMAKE_CURRENT_BINARY_DIR}/${CMAKE_PROJECT_NAME}.map,--cref"
        )