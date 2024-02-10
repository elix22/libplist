cmake_minimum_required(VERSION 3.0)
project(libplist)


set(CMAKE_CXX_STANDARD 20)

if(CMAKE_SYSTEM_NAME STREQUAL "Windows")
    add_definitions(-DHAVE_STRNDUP -DPACKAGE_VERSION="v1.3")
elseif(CMAKE_SYSTEM_NAME STREQUAL "Linux")
    add_definitions(-DHAVE_STRNDUP -DPACKAGE_VERSION="v1.3")
elseif(CMAKE_SYSTEM_NAME STREQUAL "Darwin")
    add_definitions(-DHAVE_STRNDUP -DPACKAGE_VERSION="v1.3")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -stdlib=libc++ -x objective-c++ ")
endif()

# Collect all .cpp files recursively
file(GLOB_RECURSE PLIST_SOURCES src/*.cpp src/*.c src/*.h)
file(GLOB_RECURSE CNARY_SOURCES libcnary/*.c )

add_library(libplist SHARED ${PLIST_SOURCES} ${CNARY_SOURCES})

target_include_directories(libplist PRIVATE include libcnary/include src)