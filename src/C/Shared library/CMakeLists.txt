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
install(TARGETS C_Shared_Library DESTINATION /usr/lib)

if(UNIX)
    if(APPLE)
        # macOS
        message(FATAL_ERROR "macOS is unsupported!")
    else(APPLE)
        # Linux
        set(CMAKE_C_FLAGS_RELEASE "-std=c18 -m64 -Ofast -flto -march=native -funroll-loops -fno-builtin -s")
    endif(APPLE)
elseif(WIN32)
    # Windows
else(UNIX)
    message(FATAL_ERROR "Unknown platform!")
endif(UNIX)
