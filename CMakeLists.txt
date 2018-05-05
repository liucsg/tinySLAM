cmake_minimum_required(VERSION 2.8.3)
project(tinySLAM)

set(CMAKE_BUILD_TYPE "Release")
set(CMAKE_CXX_FLAGS "-std=c++11")
set(CMAKE_CXX_FLAGS_RELEASE "-O3 -Wall -g")

SET(CMAKE_C_COMPILER "/usr/bin/g++")

find_package(OpenCV REQUIRED)

include_directories(include)


# library
add_library(tinySLAM SHARED
	src/CoreSLAM.c)
target_link_libraries(tinySLAM)

# exe
add_executable(test_lab_reverse test/test_lab_reverse.c)
target_link_libraries(test_lab_reverse 
	${OpenCV_LIBRARIES}
	${PROJECT_SOURCE_DIR}/build/libtinySLAM.so)

add_dependencies(test_lab_reverse tinySLAM)
