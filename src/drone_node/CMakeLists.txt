cmake_minimum_required(VERSION 2.8.3)
project(drone_node)

find_package(catkin REQUIRED COMPONENTS 
    roscpp 
    std_msgs
    nav_msgs
    visualization_msgs
    waypoint_trajectory_generator
    geometry_msgs 
)

find_package(Eigen3 REQUIRED)
find_package(PCL REQUIRED)

set(Eigen3_INCLUDE_DIRS ${EIGEN3_INCLUDE_DIR})


include_directories(
    include 
    SYSTEM 
    third_party
    ${catkin_INCLUDE_DIRS} 
    ${Eigen3_INCLUDE_DIRS} 
    ${PCL_INCLUDE_DIRS}
)

catkin_package(
  INCLUDE_DIRS include
)

set(CMAKE_CXX_FLAGS "-std=c++11 ${CMAKE_CXX_FLAGS} -O3 -Wall") # -Wextra -Werror

add_executable( drone_node 
	src/drone_node.cpp

    )

target_link_libraries(drone_node
    ${catkin_LIBRARIES}
    ${PCL_LIBRARIES} 
)

