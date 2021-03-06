# The version of CMake we're targeting
cmake_minimum_required (VERSION 2.8)

# The name of this project.
project (eye)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3 -mthumb -march=armv7-a -mcpu=cortex-a8 -mtune=cortex-a8 -mfloat-abi=hard -mfpu=neon -Os -Ofast -pipe -ffast-math -funsafe-math-optimizations -fassociative-math -fsingle-precision-constant -funsafe-loop-optimizations -Wunsafe-loop-optimizations")
# OpenCV
find_package(OpenCV REQUIRED)
include_directories(OpenCV_INCLUDE_DIRS)

# Video for Linux
find_path(V4L_INCLUDE_DIR NAMES libv4l2.h)
include_directories(V4L_INCLUDE_DIR)

find_library(V4L_LIB NAMES v4l2)

# Our sources
get_filename_component (my_folder . ABSOLUTE)
include_directories (${my_folder})

set (camera_sources
	${my_folder}/camera.cpp
	${my_folder}/OCVCapture.cpp)
	
# Specify an executable that includes all of the above
# sources and link libraries

add_executable(camera
	${camera_sources})

target_link_libraries(camera
	${OpenCV_LIBS}
	${V4L_LIB})

