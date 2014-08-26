cmake_minimum_required(VERSION 2.8.3)
project(ras_lab1_world)

find_package(catkin REQUIRED COMPONENTS roscpp std_msgs)
find_package(Boost REQUIRED COMPONENTS random)

catkin_package(
  DEPENDS
  CATKIN_DEPENDS roscpp std_msgs
  INCLUDE_DIRS
)

include_directories(
  ${catkin_INCLUDE_DIRS}
  ${Boost_INCLUDE_DIRS}
)


add_executable(world_node src/world_main.cpp)
target_link_libraries(world_node ${catkin_LIBRARIES} ${Boost_LIBRARIES})

install(TARGETS world_node
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
