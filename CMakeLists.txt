cmake_minimum_required(VERSION 2.8.3)
# Compile options so compiles with ROS Kinetic
# Future releases may want to 
add_compile_options(-std=c++11)
project(vectornav)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS roscpp std_msgs message_generation)

## Generate messages in the 'msg' folder
 add_message_files(FILES
   	Vn_ins_status.msg
 	)
 
 
## Generate added messages and services with any dependencies listed here
 generate_messages (DEPENDENCIES
 	std_msgs
 	)

###################################
## catkin specific configuration ##
###################################
catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES vectornav
   CATKIN_DEPENDS roscpp sensor_msgs message_runtime std_msgs
#  DEPENDS system_lib
)

###########
## Build ##
###########

#include(vnproglib-1.1/cpp/CMakeLists.txt)
add_subdirectory(vnproglib-1.1.5.0/cpp)

## Specify additional locations of header files
## Your package locations should be listed before other locations
include_directories(vnproglib-1.1.5.0/cpp/include ${catkin_INCLUDE_DIRS} ~/catkin_ws/devel/include/vectornav)

## Declare a cpp library
## Declare a cpp executable
add_executable(vnpub src/main.cpp)

## Specify libraries to link a library or executable target against
target_link_libraries(vnpub
  libvncxx
  ${catkin_LIBRARIES}
)

add_dependencies(vnpub vectornav_generate_messages_cpp)

## Mark executables and/or libraries for installation
install(TARGETS vnpub
   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
