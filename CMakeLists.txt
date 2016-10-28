cmake_minimum_required (VERSION 3.0.2)

include("HunterGate.cmake")

HunterGate(
    URL "https://github.com/ruslo/hunter/archive/v0.16.15.tar.gz"
    SHA1 "6974c2150fc0d3b09de3ad1efcbf15d360647ffa"
    LOCAL #load cmake/Hunter/config.cmake
)

project(develab)

hunter_add_package(freetype)

find_package(freetype CONFIG REQUIRED)

hunter_add_package(Jpeg)
hunter_add_package(OpenCV)
find_package(OpenCV CONFIG REQUIRED)

add_library(lib1 STATIC lib1.cpp)
target_include_directories(lib1 PUBLIC include1)
target_include_directories(lib1 SYSTEM PUBLIC system1)
target_link_libraries(lib1 PUBLIC lib2)

add_library(lib2 STATIC lib2.cpp)
target_include_directories(lib2 PUBLIC include2)
target_include_directories(lib2 SYSTEM PUBLIC system2)
target_link_libraries(lib2 PUBLIC lib3 freetype::freetype)

add_library(lib3 STATIC lib3.cpp)
target_include_directories(lib3 PUBLIC include3)
target_include_directories(lib3 SYSTEM PUBLIC system3)

add_executable(exe1 main.cpp)
target_link_libraries(exe1 lib1)