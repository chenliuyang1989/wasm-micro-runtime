# Copyright (C) 2023 Midokura Japan KK.  All rights reserved.
# SPDX-License-Identifier: Apache-2.0 WITH LLVM-exception

cmake_minimum_required(VERSION 3.14)
project(mem_allocator_create)

string (TOLOWER ${CMAKE_HOST_SYSTEM_NAME} WAMR_BUILD_PLATFORM)
if(APPLE)
  add_definitions(-DBH_PLATFORM_DARWIN)
endif()

set(WAMR_BUILD_INTERP 1)
set(WAMR_BUILD_LIBC_BUILTIN 0)

set(WAMR_ROOT_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../..)
include(${WAMR_ROOT_DIR}/build-scripts/runtime_lib.cmake)

add_library(vmlib ${WAMR_RUNTIME_LIB_SOURCE})

add_executable(mem_alloc_test main.c)

target_link_libraries(mem_alloc_test vmlib -lm -lpthread)
