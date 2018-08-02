cmake_minimum_required(VERSION 3.11.0)
project(CPP_Static_Library)

if(CMAKE_CONFIGURATION_TYPES)
  set(CMAKE_CONFIGURATION_TYPES Debug Release)
  set(CMAKE_CONFIGURATION_TYPES "${CMAKE_CONFIGURATION_TYPES}" CACHE STRING "" FORCE)
endif(CMAKE_CONFIGURATION_TYPES)

set(CMAKE_BUILD_TYPE Release)

set(CPP_Static_Library_VERSION_MAJOR 1)
set(CPP_Static_Library_VERSION_MINOR 0)
set(CPP_Static_Library_VERSION_PATCH 0)
set(CPP_Static_Library_VERSION_TWEAK 0)

include_directories(include)

file(GLOB SOURCES "src/*.cpp")

set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)
add_library(CPP_Static_Library ${SOURCES})
target_link_libraries(CPP_Static_Library lib1 lib2 lib3)
install(TARGETS CPP_Static_Library DESTINATION ${CMAKE_SOURCE_DIR}/lib)

if(UNIX)
    if(APPLE)
        # macOS
        message(FATAL_ERROR "macOS is unsupported!")
    else(APPLE)
        # Linux
        if("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
            set(CMAKE_CXX_FLAGS_DEBUG "-std=c++17 -m64 -g -Wall -march=native")
            set(CMAKE_CXX_FLAGS_RELEASE "-std=c++17 -m64 -Wall -Ofast -march=native -flto -fuse-linker-plugin -funroll-loops -fno-builtin -s -ffunction-sections -fdata-sections -Wl,--gc-sections -fno-rtti")
        else("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
            message(FATAL_ERROR "Please install GCC!")
        endif("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
    endif(APPLE)
elseif(WIN32)
    # Windows
    if("${CMAKE_CXX_COMPILER_ID}" STREQUAL "MSVC")
        set(CMAKE_CXX_FLAGS_RELEASE "/std:c++17 /GR- /Ox /MP /GL /Gy /fp:fast /arch:AVX2 /GF /Gw /Ob2 /Oi /Ot /Oy")
        set(CMAKE_EXE_LINKER_FLAGS_RELEASE "/OPT:REF /OPT:ICF /LTCG:incremental")
    else("${CMAKE_CXX_COMPILER_ID}" STREQUAL "MSVC")
        message(FATAL_ERROR "Please install Microsoft Visual Studio!")
    endif("${CMAKE_CXX_COMPILER_ID}" STREQUAL "MSVC")
else(UNIX)
    message(FATAL_ERROR "Unknown platform!")
endif(UNIX)
