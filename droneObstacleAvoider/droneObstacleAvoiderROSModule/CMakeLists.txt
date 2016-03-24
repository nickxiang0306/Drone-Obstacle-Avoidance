cmake_minimum_required(VERSION 2.8.3)

set(PROJECT_NAME droneObstacleAvoiderROSModule)
project(${PROJECT_NAME})

### Use version 2011 of C++ (c++11). By default ROS uses c++98
#see: http://stackoverflow.com/questions/10851247/how-to-activate-c-11-in-cmake
#see: http://stackoverflow.com/questions/10984442/how-to-detect-c11-support-of-a-compiler-with-cmake
#add_definitions(-std=c++11)
#add_definitions(-std=c++0x)
add_definitions(-std=c++03)

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries

 

set(DRONE_OBSTACLE_AVOIDER_ROS_SOURCE_DIR
	src/source) 
	
set(DRONE_OBSTACLE_AVOIDER_ROS_INCLUDE_DIR
	src/include)

set(DRONE_OBSTACLE_AVOIDER_ROS_SOURCE_FILES
        ${DRONE_OBSTACLE_AVOIDER_ROS_SOURCE_DIR}/droneObstacleAvoiderROSModule.cpp

)
 
set(DRONE_OBSTACLE_AVOIDER_ROS_HEADER_FILES
        ${DRONE_OBSTACLE_AVOIDER_ROS_INCLUDE_DIR}/droneObstacleAvoiderROSModule.h
)

find_package(catkin REQUIRED
                COMPONENTS roscpp std_msgs geometry_msgs droneModuleROS droneObstacleAvoider droneMidLevelAutopilot droneMsgsROS)


catkin_package(
        CATKIN_DEPENDS roscpp std_msgs geometry_msgs droneModuleROS droneObstacleAvoider droneMidLevelAutopilot droneMsgsROS
  )


include_directories(${DRONE_OBSTACLE_AVOIDER_ROS_INCLUDE_DIR})
include_directories(${catkin_INCLUDE_DIRS})



add_library(droneObstacleAvoiderROSModule ${DRONE_OBSTACLE_AVOIDER_ROS_SOURCE_FILES} ${DRONE_OBSTACLE_AVOIDER_ROS_HEADER_FILES})
add_dependencies(droneObstacleAvoiderROSModule ${catkin_EXPORTED_TARGETS})
target_link_libraries(droneObstacleAvoiderROSModule ${catkin_LIBRARIES})


add_executable(droneObstacleAvoiderROSModuleNode ${DRONE_OBSTACLE_AVOIDER_ROS_SOURCE_DIR}/droneObstacleAvoiderROSModuleNode.cpp)
add_dependencies(droneObstacleAvoiderROSModuleNode ${catkin_EXPORTED_TARGETS})
target_link_libraries(droneObstacleAvoiderROSModuleNode droneObstacleAvoiderROSModule)
target_link_libraries(droneObstacleAvoiderROSModuleNode ${catkin_LIBRARIES})

