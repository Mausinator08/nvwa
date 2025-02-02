cmake_minimum_required(VERSION 3.8)
project(nvwa)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

file(GLOB SRC_FILES CONFIGURE_DEPENDS ${nvwa_SOURCE_DIR}/nvwa/debug_new.cpp)

add_library(nvwa STATIC ${SRC_FILES})
add_library(nvwa::nvwa ALIAS nvwa)

target_include_directories(nvwa PUBLIC ${nvwa_SOURCE_DIR}/nvwa/)
target_compile_definitions(nvwa PUBLIC UNICODE _UNICODE)
target_compile_options(nvwa PUBLIC -m64 -fpermissive -Wno-unknown-pragmas)

if (${CMAKE_BUILD_TYPE} STREQUAL "Debug")
    target_compile_options(nvwa PUBLIC -Wall -O0 -g)
    target_compile_definitions(nvwa PUBLIC _DEBUG)
elseif(${CMAKE_BUILD_TYPE} STREQUAL "RelWithDebInfo")
    target_compile_options(nvwa PUBLIC -O2 -g)
    target_compile_definitions(nvwa PUBLIC NDEBUG)
elseif(${CMAKE_BUILD_TYPE} STREQUAL "MinSizeRel")
    target_compile_options(nvwa PUBLIC -Os)
    target_compile_definitions(nvwa PUBLIC NDEBUG)
elseif(${CMAKE_BUILD_TYPE} STREQUAL "Release")
    target_compile_options(nvwa PUBLIC -O3)
    target_compile_definitions(nvwa PUBLIC NDEBUG)
endif()
