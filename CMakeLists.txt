cmake_minimum_required(VERSION 2.8.3)
project(test_dual_trajectory)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

LIST( APPEND CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}/cmake" )

find_package(catkin REQUIRED COMPONENTS
  roscpp
  dynamic_reconfigure
  controller_interface
  # franka_hw
  # franka_gripper
  geometry_msgs
  hardware_interface
  ##pluginlibcf
  realtime_tools
  roscpp
  rospy
  roslib
  moveit_ros_planning
  moveit_ros_planning_interface
  moveit_core
  assembly_msgs
  moveit_resources
)
find_package(Eigen3 REQUIRED)
find_package(RBDL REQUIRED)
find_package(Franka 0.5.0 REQUIRED)
find_package(Boost REQUIRED system filesystem date_time thread)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES ${PROJECT_NAME}
  CATKIN_DEPENDS
  roscpp
  franka_gripper
  geometry_msgs
  roscpp
  rospy
  roslib
  assembly_msgs
  actionlib
  actionlib_msgs
  DEPENDS Franka
)


set(SOURCES

)

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
  ${EIGEN3_INCLUDE_DIRS}
  ${Franka_INCLUDE_DIRS}
  ${RBDL_INCLUDE_DIRS}  
)
add_definitions(-Ddof=7)


add_executable(${PROJECT_NAME}
  src/main.cpp)

target_link_libraries(${PROJECT_NAME}
  ${catkin_LIBRARIES}
)
