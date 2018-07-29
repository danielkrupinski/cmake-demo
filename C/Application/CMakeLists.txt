cmake_minimum_required(VERSION 3.11.0)
project(C_Application)

if(CMAKE_CONFIGURATION_TYPES)
  set(CMAKE_CONFIGURATION_TYPES Debug Release)
  set(CMAKE_CONFIGURATION_TYPES "${CMAKE_CONFIGURATION_TYPES}" CACHE STRING "" FORCE)
endif(CMAKE_CONFIGURATION_TYPES)

set(CMAKE_BUILD_TYPE Release)

set(C_Application_VERSION_MAJOR 1)
set(C_Application_VERSION_MINOR 0)
set(C_Application_VERSION_PATCH 0)
set(C_Application_VERSION_TWEAK 0)

include_directories(include)

file(GLOB SOURCES "src/*.c")

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)
add_executable(C_Application ${SOURCES})
target_link_libraries(C_Application lib1 lib2 lib3)

if(UNIX)
    if(APPLE)
        # macOS
        message(FATAL_ERROR "macOS is unsupported!")
    else(APPLE)
        # Linux
        if("${CMAKE_C_COMPILER_ID}" STREQUAL "GNU")
            set(CMAKE_C_FLAGS_DEBUG "-std=c18 -m64 -g -Wall -march=native")
            set(CMAKE_C_FLAGS_RELEASE "-std=c18 -m64 -Wall -Ofast -march=native -flto -fuse-linker-plugin -funroll-loops -fno-builtin -s -ffunction-sections -fdata-sections -Wl,--gc-sections")
        else("${CMAKE_C_COMPILER_ID}" STREQUAL "GNU")
            message(FATAL_ERROR "Please install GCC!")
        endif("${CMAKE_C_COMPILER_ID}" STREQUAL "GNU")
    endif(APPLE)
elseif(WIN32)
    # Windows
    if("${CMAKE_C_COMPILER_ID}" STREQUAL "MSVC")
        set(CMAKE_C_FLAGS_RELEASE "/Ox /MP /GL /Gy /fp:fast /arch:AVX2 /GF /Gw /Ob2 /Oi /Ot")
        set(CMAKE_EXE_LINKER_FLAGS_RELEASE "/OPT:REF /OPT:ICF /LTCG:incremental")
    else("${CMAKE_C_COMPILER_ID}" STREQUAL "MSVC")
        message(FATAL_ERROR "Please install Microsoft Visual Studio!")
    endif("${CMAKE_C_COMPILER_ID}" STREQUAL "MSVC")
else(UNIX)
    message(FATAL_ERROR "Unknown platform!")
endif(UNIX)
