cmake_minimum_required(VERSION 2.8.3)
project(cpp_common)

include(GNUInstallDirs)

set(Boost_INCLUDE_DIRS "/opt/crystax-ndk-10.3.2/sources/boost/1.59.0/include/")
set(Boost_LIBRARIES "-L/opt/crystax-ndk-10.3.2/sources/boost/1.59.0/libs/armeabi-v7a/gnu-4.9/ -lboost_thread -lboost_system")
#find_package(Boost REQUIRED COMPONENTS system thread)
find_package(console_bridge REQUIRED)
#find_package(catkin REQUIRED)
#catkin_package(
#  DEPENDS Boost console_bridge
#  INCLUDE_DIRS include
#  LIBRARIES ${PROJECT_NAME})

# include(CheckIncludeFile)
# include(CheckFunctionExists)
# include(CheckCXXSourceCompiles)

include_directories(include ${Boost_INCLUDE_DIRS} ${console_bridge_INCLUDE_DIRS})

# # execinfo.h is needed for backtrace on glibc systems
# CHECK_INCLUDE_FILE(execinfo.h HAVE_EXECINFO_H)
# if(HAVE_EXECINFO_H)
#   add_definitions(-DHAVE_EXECINFO_H=1)
#   message(STATUS "-DHAVE_EXECINFO_H=1")
# endif(HAVE_EXECINFO_H)
# # do we have demangle capability?
# # CHECK_INCLUDE_FILE doesn't work here for some reason
# CHECK_CXX_SOURCE_COMPILES("#include<cxxabi.h>\nintmain(intargc,char**argv){}" HAVE_CXXABI_H)
# if(HAVE_CXXABI_H)
#   add_definitions(-DHAVE_CXXABI_H=1)
#   message(STATUS "-DHAVE_CXXABI_H=1")
# endif()
# CHECK_FUNCTION_EXISTS(backtrace HAVE_GLIBC_BACKTRACE)
# if(HAVE_GLIBC_BACKTRACE)
#   add_definitions(-DHAVE_GLIBC_BACKTRACE)
#   message(STATUS "-DHAVE_GLIBC_BACKTRACE")
# endif(HAVE_GLIBC_BACKTRACE)

add_library(${PROJECT_NAME} src/debug.cpp src/header.cpp)
target_link_libraries(${PROJECT_NAME} ${Boost_LIBRARIES} ${console_bridge_LIBRARIES})

install(TARGETS ${PROJECT_NAME}
  ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} #${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} #${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} #${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY include/
  DESTINATION ${CMAKE_INSTALL_INCLUDEDIR} #${CATKIN_GLOBAL_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.h")
