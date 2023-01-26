cmake_minimum_required(VERSION 2.8.3)
project(graph_manager_msgs)

# Can we use C++17 in indigo?
add_definitions(-msse -msse2 -msse3 -msse4 -msse4.1 -msse4.2)
set(CMAKE_CXX_FLAGS "-msse -msse2 -msse3 -msse4 -msse4.1 -msse4.2")
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_LIST_DIR}/cmake")

# pcl 1.7 causes a segfault when it is built with debug mode
set(CMAKE_BUILD_TYPE "RELEASE")

find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  pcl_ros
  sensor_msgs
  geometry_msgs
  message_generation
)
########################
## message generation ##
########################
add_message_files(FILES
  Attribute.msg
  Edge.msg
  Graph.msg
  Node.msg
  Match.msg
)

add_service_files(FILES
SubgraphMatch.srv
)

generate_messages(DEPENDENCIES std_msgs geometry_msgs sensor_msgs)
catkin_package(
 CATKIN_DEPENDS pcl_ros roscpp sensor_msgs
 DEPENDS system_lib
)
