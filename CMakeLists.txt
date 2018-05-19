cmake_minimum_required(VERSION 3.10.2)
project(Example)

set(CMAKE_BUILD_TYPE Release)

set(Example_VERSION_MAJOR 1)
set(Example_VERSION_MINOR 0)
set(Example_VERSION_PATCH 0)
set(Example_VERSION_TWEAK 0)

include_directories(include)

#   For C
#   file(GLOB SOURCES "src/*.c")
#   set(CMAKE_C_FLAGS_RELEASE "-std=c18 -m64 -Ofast -flto -march=native -funroll-loops -fno-builtin")

#   For C++
file(GLOB SOURCES "src/*.cpp")
set(CMAKE_CXX_FLAGS_RELEASE "-std=c++17 -m64 -Ofast -flto -march=native -funroll-loops -fno-builtin")

#   For an executable
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)
add_executable(Example ${SOURCES})
target_link_libraries(Example lib1 lib2 lib3)

#   For a shared library
#   set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)
#   add_library(Example SHARED ${SOURCES})
#   target_link_libraries(Example lib1 lib2 lib3)
#   install(TARGETS Example DESTINATION /usr/lib)
