cmake_minimum_required(VERSION 2.8.3)
project(ras_lab1_distance_sensor)

find_package(catkin REQUIRED COMPONENTS roscpp std_msgs)
find_package(Boost REQUIRED COMPONENTS random)

catkin_package(
  DEPENDS
  CATKIN_DEPENDS roscpp std_msgs
  INCLUDE_DIRS include 
  LIBRARIES 
)

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
  ${Boost_INCLUDE_DIRS}
)

add_custom_target(
  copy_distance_sensor_lib ALL
  COMMAND cmake -E copy ${PROJECT_SOURCE_DIR}/lib/libdistance_sensor.so ${CATKIN_DEVEL_PREFIX}/${CATKIN_GLOBAL_LIB_DESTINATION}/libdistance_sensor.so
)

link_directories(${CATKIN_DEVEL_PREFIX}/${CATKIN_GLOBAL_LIB_DESTINATION})

add_executable(distance_sensor_test_node src/distance_sensor_test_node.cpp)
add_dependencies(distance_sensor_test_node copy_distance_sensor_lib)
target_link_libraries(distance_sensor_test_node ${catkin_LIBRARIES} ${Boost_LIBRARIES} distance_sensor)

install(TARGETS distance_sensor_test_node
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
