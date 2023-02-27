cmake_minimum_required(VERSION 3.22)

if (DEFINED ENV{OPENWRT_DIR})
    message($ENV{OPENWRT_DIR} " is defined")
    set(CMAKE_C_COMPILER $ENV{OPENWRT_DIR}/staging_dir/toolchain-aarch64_cortex-a72_gcc-11.2.0_musl/bin/aarch64-openwrt-linux-gcc)
    set(CMAKE_CXX_COMPILER $ENV{OPENWRT_DIR}/staging_dir/toolchain-aarch64_cortex-a72_gcc-11.2.0_musl/bin/aarch64-openwrt-linux-g++)
    # message(${CMAKE_C_COMPILER})
    # message(${CMAKE_CXX_COMPILER})
endif()

project(iowa)

# message($ENV{IOWA_DIR})

include($ENV{IOWA_DIR}/src/iowa.cmake)

# message(${IOWA_CLIENT_SOURCES})
# message(${IOWA_CLIENT_HEADERS})

add_library(${PROJECT_NAME} STATIC
            ${CMAKE_CURRENT_LIST_DIR}/iowa_config.h
            $ENV{IOWA_DIR}/samples/abstraction_layer/core_abstraction.c
            $ENV{IOWA_DIR}/samples/abstraction_layer/connection_abstraction.c
            $ENV{IOWA_DIR}/samples/abstraction_layer/mutex_abstraction.c
            ${IOWA_CLIENT_SOURCES}
            ${IOWA_CLIENT_HEADERS})

target_include_directories(${PROJECT_NAME} PRIVATE
            ${IOWA_INCLUDE_DIR}
            ${CMAKE_CURRENT_LIST_DIR})