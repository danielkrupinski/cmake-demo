cmake_minimum_required(VERSION 3.10.2)
project(Example)

set(CMAKE_BUILD_TYPE Release)

set(Example_VERSION_MAJOR 1)
set(Example_VERSION_MINOR 0)
set(Example_VERSION_PATCH 0)
set(Example_VERSION_TWEAK 0)

include_directories(include)
file(GLOB SOURCES "src/*.cpp")

add_executable(Example ${SOURCES})
