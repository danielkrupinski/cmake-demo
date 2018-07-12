cmake_minimum_required(VERSION 3.10.2)
project(C_Shared_Library)

set(CMAKE_BUILD_TYPE Release)

set(C_Shared_Library_VERSION_MAJOR 1)
set(C_Shared_Library_VERSION_MINOR 0)
set(C_Shared_Library_VERSION_PATCH 0)
set(C_Shared_Library_VERSION_TWEAK 0)

include_directories(include)

file(GLOB SOURCES "src/*.c")

set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)
add_library(C_Shared_Library SHARED ${SOURCES})
target_link_libraries(C_Shared_Library lib1 lib2 lib3)
install(TARGETS C_Shared_Library DESTINATION ${CMAKE_SOURCE_DIR}/lib)

if(UNIX)
    if(APPLE)
        # macOS
        message(FATAL_ERROR "macOS is unsupported!")
    else(APPLE)
        # Linux
        if("${CMAKE_C_COMPILER_ID}" STREQUAL "GNU")
            set(CMAKE_C_FLAGS_DEBUG "-std=c18 -m64 -g -Wall -march=native")
            set(CMAKE_C_FLAGS_RELEASE "-std=c18 -m64 -Wall -Ofast -march=native -flto -fuse-linker-plugin -funroll-loops -fno-builtin -s -ffunction-sections -fdata-sections -Wl,--gc-sections -fno-rtti")
        else("${CMAKE_C_COMPILER_ID}" STREQUAL "GNU")
            message(FATAL_ERROR "Please install GCC!")
        endif("${CMAKE_C_COMPILER_ID}" STREQUAL "GNU")
    endif(APPLE)
elseif(WIN32)
    # Windows
    if("${CMAKE_C_COMPILER_ID}" STREQUAL "MSVC")
        set(CMAKE_C_FLAGS_RELEASE "/GL /Gy /OPT:REF /OPT:ICF /fp:fast /arch:AVX2")
    else("${CMAKE_C_COMPILER_ID}" STREQUAL "MSVC")
        message(FATAL_ERROR "Please install Microsoft Visual Studio!")
    endif("${CMAKE_C_COMPILER_ID}" STREQUAL "MSVC")
else(UNIX)
    message(FATAL_ERROR "Unknown platform!")
endif(UNIX)
