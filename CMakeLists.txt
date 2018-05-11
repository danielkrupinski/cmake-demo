cmake_minimum_required(VERSION 3.10.2)
project(Example)

set(CMAKE_BUILD_TYPE Release)

set(Example_VERSION_MAJOR 1)
set(Example_VERSION_MINOR 0)
set(Example_VERSION_PATCH 0)
set(Example_VERSION_TWEAK 0)

include_directories(include)

# For C
file(GLOB SOURCES "src/*.c")

# For C++
file(GLOB SOURCES "src/*.cpp")
set(CMAKE_CXX_FLAGS_RELEASE "-m64 -Ofast -flto -march=native -funroll-loops")

# For executable
add_executable(Example ${SOURCES})

# For shared library
# add_library(Example SHARED ${SOURCES})
# install(TARGETS Example DESTINATION /usr/lib)
