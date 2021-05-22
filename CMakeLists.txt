cmake_minimum_required(VERSION 3.12)

# Pull in SDK (must be before project)
include($ENV{PICO_SDK_PATH}/external/pico_sdk_import.cmake)

project(pico_msd C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)


# Initialize the SDK
pico_sdk_init()

add_executable(${PROJECT_NAME}
        main.c
        msc_disk.c
        usb_descriptors.c
)

target_include_directories(${PROJECT_NAME} PRIVATE ${CMAKE_CURRENT_LIST_DIR})

target_link_libraries(${PROJECT_NAME} 
        PRIVATE 
        pico_stdlib 
        tinyusb_device 
        tinyusb_board
)
pico_add_extra_outputs(${PROJECT_NAME})

