cmake_minimum_required(VERSION 3.0.2)
project(human_traj_estimator)

set(CMAKE_CXX_FLAGS "-std=c++11 ${CMAKE_CXX_FLAGS}")

find_package(catkin REQUIRED COMPONENTS
  roscpp
  std_msgs
  rosdyn_core
  geometry_msgs
  tf
  tf2
  tf2_ros
  rotations_helper
  tf_conversions
  eigen_conversions
  configuration_msgs
  )

catkin_package(
  INCLUDE_DIRS
  include
  CATKIN_DEPENDS
  rosdyn_core
  rotations_helper
)

include_directories(
include
${catkin_INCLUDE_DIRS}
)


add_library(
human_traj_estimation src/human_traj_estimation.cpp
)


add_executable(reset_pose_test src/reset_pose_test.cpp)
target_link_libraries( reset_pose_test ${catkin_LIBRARIES})
add_dependencies(reset_pose_test ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

add_executable(human_traj_estimation_node src/human_traj_estimation_node.cpp)
target_link_libraries( human_traj_estimation_node human_traj_estimation ${catkin_LIBRARIES} )
add_dependencies(human_traj_estimation_node ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
