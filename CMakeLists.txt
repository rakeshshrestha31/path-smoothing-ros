cmake_minimum_required(VERSION 2.8.3)
project(path_smoothing_ros)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  geometry_msgs
  nav_msgs
)

catkin_package(
 INCLUDE_DIRS
  include
 CATKIN_DEPENDS
  roscpp
  geometry_msgs
  nav_msgs
 LIBRARIES
  path_smoothing_ros
)

include_directories(include ${catkin_INCLUDE_DIRS})

add_library(${PROJECT_NAME} src/cubic_spline_interpolator.cpp)
target_link_libraries(${PROJECT_NAME} ${catkin_LIBRARIES})

add_executable(demo src/demo.cpp)
target_link_libraries(demo ${PROJECT_NAME} ${catkin_LIBRARIES})

install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  PATTERN ".svn" EXCLUDE)
