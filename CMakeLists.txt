cmake_minimum_required(VERSION 3.0.0)
project(gazebo_tag_ranges_plugin)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)

SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}  -std=c++11")


add_definitions(-std=c++11)


## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
  gazebo_ros
  roscpp
  std_msgs
  gtec_msgs
  tf
)

# Depend on system install of Gazebo
find_package(gazebo REQUIRED)

link_directories(${GAZEBO_LIBRARY_DIRS})
include_directories(${Boost_INCLUDE_DIR} ${catkin_INCLUDE_DIRS} ${GAZEBO_INCLUDE_DIRS})

add_library(tag_ranges_plugin src/RelativeDistancePlugin.cpp)
target_link_libraries(tag_ranges_plugin ${catkin_LIBRARIES} ${GAZEBO_LIBRARIES} ${Boost_LIBRARIES})
add_dependencies(tag_ranges_plugin ${catkin_EXPORTED_TARGETS})


catkin_package(
  DEPENDS 
    roscpp 
    gazebo_ros
    gtec_msgs
)
##add_dependencies(${PROJECT_NAME} gtec_generate_messages_cpp)
