cmake_minimum_required(VERSION 2.8.3)
project(rostime)

include(GNUInstallDirs)

#find_package(catkin REQUIRED COMPONENTS cpp_common)
#find_package(Boost REQUIRED COMPONENTS date_time system thread)
#catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES ${PROJECT_NAME}
#  CATKIN_DEPENDS cpp_common
#  DEPENDS Boost
#)

set(Boost_INCLUDE_DIRS "/opt/crystax-ndk-10.3.2/sources/boost/1.59.0/include/")
set(Boost_LIBRARIES "-L/opt/crystax-ndk-10.3.2/sources/boost/1.59.0/libs/armeabi-v7a/gnu-4.9/ -lboost_thread -lboost_system -lboost_date_time")

include_directories(include ${Boost_INCLUDE_DIRS})

add_library(rostime
  src/duration.cpp
  src/rate.cpp
  src/time.cpp)

target_link_libraries(rostime ${Boost_LIBRARIES})
#if(NOT APPLE)
#  target_link_libraries(rostime ${RT_LIBRARY})
#endif()

install(TARGETS ${PROJECT_NAME}
  ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} #${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} #${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} #${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY include/
  DESTINATION ${CMAKE_INSTALL_INCLUDEDIR} #${CATKIN_GLOBAL_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.h")

# if(CATKIN_ENABLE_TESTING)
#   catkin_add_gtest(${PROJECT_NAME}-test_duration test/duration.cpp)
#   if(TARGET ${PROJECT_NAME}-test_duration)
#     target_link_libraries(${PROJECT_NAME}-test_duration ${catkin_LIBRARIES} rostime)
#   endif()
#   catkin_add_gtest(${PROJECT_NAME}-test_time test/time.cpp)
#   if(TARGET ${PROJECT_NAME}-test_time)
#     set_property(TARGET ${PROJECT_NAME}-test_time APPEND_STRING PROPERTY COMPILE_FLAGS "-std=c++11")
#     target_link_libraries(${PROJECT_NAME}-test_time ${catkin_LIBRARIES} rostime)
#   endif()
# endif()
