cmake_minimum_required(VERSION 2.8.3)
project(surfel_cloud_rviz_plugin)

add_compile_options(-std=c++11)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  rviz
  sensor_msgs
  roslib
)

find_package(PCL REQUIRED)

set(CMAKE_AUTOMOC ON)
find_package(Qt5 COMPONENTS Core Widgets OpenGL REQUIRED)

set( QT_LINK_LIBRARIES Qt5::Core Qt5::Widgets Qt5::OpenGL )
include_directories( 
	${CMAKE_BINARY_DIR} 
	${Qt5Core_INCLUDE_DIRS}
	${Qt5Widgets_INCLUDE_DIRS}	
	${Qt5OpenGL_INCLUDE_DIRS}
	${catkin_INCLUDE_DIRS}
  	${PCL_INCLUDE_DIRS}
	)
catkin_package()
add_definitions( ${QT_DEFINITIONS} )

#https://github.com/hakuturu583/gps_rviz_plugin/blob/master/CMakeLists.txt
add_definitions(-DQT_NO_KEYWORDS)

add_library( surfel_cloud_rviz_plugin src/surfel_cloud_display.cpp src/point_cloud_common.cpp src/point_cloud.cpp )

add_dependencies(surfel_cloud_rviz_plugin ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

target_link_libraries(surfel_cloud_rviz_plugin ${catkin_LIBRARIES} ${PCL_LIBRARIES} )
