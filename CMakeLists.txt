#### CMake Settings ####

cmake_minimum_required(VERSION 2.8 FATAL_ERROR)
cmake_policy(SET CMP0015 OLD)	#// Do not add relative path if the designated path is not exist
add_definitions(-DUNICODE -D_UNICODE)	#// Set Unicode, not MultiBytes


#### Solution Settings ####		* MODIFY HERE*

# OpenCV
set(OPENCV_INC_DIRS "D:/opencv/build/include")
set(OPENCV_LIB_DIRS "D:/opencv/build/x86/vc12/lib")
set(OPENCV300_LIB_RELEASE optimized opencv_ts300.lib optimized opencv_world300.lib)
set(OPENCV300_LIB_DEBUG debug opencv_ts300d.lib debug opencv_world300d.lib)
set(OPENCV_LIB ${OPENCV300_LIB_RELEASE} ${OPENCV300_LIB_DEBUG})

# OpenNI2
set(OPENNI2_INC_DIRS "C:/Program Files (x86)/OpenNI2/Include")
set(OPENNI2_LIB_DIRS "C:/Program Files (x86)/OpenNI2/Lib")
set(OPENNI2_LIB OpenNI2.lib)

#### Solution Settings ####

project(structure_grabber)


#### Includes and Libraries ####

find_package(PCL 1.7 REQUIRED)
include_directories(include ${PCL_INCLUDE_DIRS} ${PCL_INCLUDE_DIRS_PLUS} ${OPENCV_INC_DIRS} ${OPENNI2_INC_DIRS})
link_directories(${PCL_LIBRARY_DIRS} ${OPENCV_LIB_DIRS} ${OPENNI2_LIB_DIRS})
add_definitions(${PCL_DEFINITIONS})


#### Required files ####

set(ONI2_GRABBER oni2_grabber.h oni2_grabber.cpp)
set(STRUCTURE_GRABBER structure_grabber.h structure_grabber.cpp ${ONI2_GRABBER})


#### Projects Settings ####

add_library(structure_depth_image_viewer structure_depth_image_viewer.cpp ${STRUCTURE_GRABBER})
target_link_libraries(structure_depth_image_viewer ${OPENNI2_LIB} ${OPENCV_LIB})

add_library(structure_colored_depth_image_viewer structure_colored_depth_image_viewer.cpp ${STRUCTURE_GRABBER})
target_link_libraries(structure_colored_depth_image_viewer ${OPENNI2_LIB} ${OPENCV_LIB})

add_library(structure_point_cloud_viewer structure_point_cloud_viewer.cpp ${STRUCTURE_GRABBER})
target_link_libraries(structure_point_cloud_viewer ${OPENNI2_LIB} ${PCL_LIBRARIES})