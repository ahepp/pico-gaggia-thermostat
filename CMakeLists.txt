cmake_minimum_required(VERSION 3.12)

include(pico_sdk_import.cmake)

project(pico_examples C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

if (PICO_SDK_VERSION_STRING VERSION_LESS "1.3.0")
    message(FATAL_ERROR "Raspberry Pi Pico SDK version 1.3.0 (or later) required. Your version is ${PICO_SDK_VERSION_STRING}")
endif()

set(PICO_EXAMPLES_PATH ${PROJECT_SOURCE_DIR})

# Initialize the SDK
pico_sdk_init()

add_compile_options(-Wall
        -Wno-format
        )

add_executable(gaggit
        main.c
        thermostat.c
        mcp9600.c
        register_map.c
        )
target_include_directories(gaggit
        PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}
        )


target_link_libraries(gaggit pico_stdlib)
target_link_libraries(gaggit hardware_i2c)

pico_enable_stdio_usb(gaggit 1)
pico_enable_stdio_uart(gaggit 0)

pico_add_extra_outputs(gaggit)
