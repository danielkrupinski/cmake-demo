cmake_minimum_required (VERSION 3.10.2)
project (Example)

set (Example_VERSION_MAJOR 1)
set (Example_VERSION_MINOR 0)
set (Example_VERSION_PATCH 0)
set (Example_VERSION_TWEAK 0)

include_directories(include)
file(GLOB_RECURSE SOURCE_FILES "${CMAKE_SOURCE_DIR}/src/*.cpp")
