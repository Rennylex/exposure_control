cmake_minimum_required(VERSION 3.0.2)
project(exposure_control)
catkin_package()

find_package(catkin REQUIRED COMPONENTS
roscpp
std_msgs
message_generation
cv_bridge
image_transport
sensor_msgs
dynamic_reconfigure
nodelet
stag_ros

)

find_package(OpenCV "3.2.0" REQUIRED)
catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES exposure_control
#  CATKIN_DEPENDS roscpp rospy std_msgs
#  DEPENDS system_lib
)

include_directories(
# include      
${PROJECT_INCLUDE_DIR}
${catkin_INCLUDE_DIRS}
${SPINNAKER_INCLUDE_DIR}
${OpenCV_INCLUDE_DIRS}
${Boost_INCLUDE_DIR}
${LibUnwind_INCLUDE_DIRS}
)

set (LIBS ${LibUnwind_LIBRARIES} Spinnaker ${OpenCV_LIBS} ${Boost_GENERAL})

add_executable(changeParam src/changeParam.cpp)
target_link_libraries(changeParam ${catkin_LIBRARIES})

install(DIRECTORY param/ DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/param)
install(DIRECTORY launch/ DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/launch)
install(DIRECTORY robots/ DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/robots)

install(TARGETS changeParam
   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
