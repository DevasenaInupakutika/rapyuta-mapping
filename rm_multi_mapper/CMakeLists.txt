cmake_minimum_required(VERSION 2.4.6)
include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
#set(ROS_BUILD_TYPE RelWithDebInfo)

rosbuild_init()

include_directories(/usr/include/suitesparse)

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

#uncomment if you have defined messages
#rosbuild_genmsg()
#uncomment if you have defined services
#rosbuild_gensrv()

#common commands for building c++ executables and libraries
#rosbuild_add_library(${PROJECT_NAME} src/example.cpp)
#target_link_libraries(${PROJECT_NAME} another_library)
#rosbuild_add_boost_directories()
#rosbuild_link_boost(${PROJECT_NAME} thread)

rosbuild_add_executable(multi_mapper src/main.cpp src/robot_mapper.cpp src/keypoint_map.cpp)
target_link_libraries(multi_mapper cholmod vtkCommon vtkFiltering rm_localization_util)

rosbuild_add_executable(ransac_test src/test.cpp src/robot_mapper.cpp src/keypoint_map.cpp)
target_link_libraries(ransac_test cholmod vtkCommon vtkFiltering rm_localization_util)

rosbuild_add_executable(test2 src/test2.cpp src/robot_mapper.cpp src/keypoint_map.cpp)
target_link_libraries(test2 cholmod vtkCommon vtkFiltering rm_localization_util)

rosbuild_add_executable(ba_demo src/ba_demo.cpp)
target_link_libraries(ba_demo cholmod)