cmake_minimum_required(VERSION 2.8.3)
project(calibration_publisher)

add_compile_options(-std=c++11)

find_package(catkin REQUIRED COMPONENTS
    cv_bridge
    image_transport
    pcl_conversions
    pcl_ros
    roscpp
    sensor_msgs
    geometry_msgs
    tf
    rosconsole
    std_msgs
    smartcar_msgs
    yunle_sensor_msgs
)

find_package(Qt5Core REQUIRED)
find_package(OpenCV REQUIRED)
find_package(PCL)

catkin_package(CATKIN_DEPENDS
    cv_bridge
    image_transport
    roscpp
    sensor_msgs
    pcl_conversions
    pcl_ros
    geometry_msgs
    tf
    std_msgs
    rosconsole
    smartcar_msgs
    yunle_sensor_msgs
)

set(CMAKE_CXX_FLAGS "-O3 -g -Wall ${CMAKE_CXX_FLAGS}")

include_directories(
    ${catkin_INCLUDE_DIRS}
    ${Boost_INCLUDE_DIRS}
    ${PCL_INCLUDE_DIRS}
)

link_directories(${PCL_LIBRARY_DIRS})
link_directories(${OpenCV_LIBRARY_DIRS})

add_executable(calibration_pub_node 
               src/calibration_publisher.cpp)

add_dependencies(calibration_pub_node ${catkin_EXPORTED_TARGETS})

target_link_libraries(calibration_pub_node ${catkin_LIBRARIES})   
