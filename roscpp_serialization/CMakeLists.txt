cmake_minimum_required(VERSION 2.8.3)
project(roscpp_serialization)

include(GNUInstallDirs)

# find_package(catkin REQUIRED COMPONENTS cpp_common roscpp_traits rostime)
# catkin_package(
#   INCLUDE_DIRS include
#   LIBRARIES roscpp_serialization
#   CATKIN_DEPENDS cpp_common roscpp_traits rostime
# )

set(Boost_INCLUDE_DIRS "/opt/crystax-ndk-10.3.2/sources/boost/1.59.0/include/")
#set(Boost_LIBRARIES "-L/opt/crystax-ndk-10.3.2/sources/boost/1.59.0/libs/armeabi-v7a/gnu-4.9/ -lboost_thread -lboost_system -lboost_date_time")

include_directories(include ${Boost_INCLUDE_DIRS})
#link_directories(${catkin_LIBRARY_DIRS})

add_library(roscpp_serialization src/serialization.cpp)
#target_link_libraries(rostime ${Boost_LIBRARIES})

install(TARGETS ${PROJECT_NAME}
  ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} #${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} #${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} #${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY include/
  DESTINATION ${CMAKE_INSTALL_INCLUDEDIR} #${CATKIN_GLOBAL_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.h")
