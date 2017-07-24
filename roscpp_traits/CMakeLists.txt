cmake_minimum_required(VERSION 2.8.3)
project(roscpp_traits)

include(GNUInstallDirs)

#find_package(catkin REQUIRED)
#catkin_package(
#  INCLUDE_DIRS include
#  CATKIN_DEPENDS cpp_common rostime)

install(DIRECTORY include/
  DESTINATION ${CMAKE_INSTALL_INCLUDEDIR} #${CATKIN_GLOBAL_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.h")
