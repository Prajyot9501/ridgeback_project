cmake_minimum_required(VERSION 3.0.2)
project(yolov8_ros)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  sensor_msgs
  cv_bridge
  image_transport
  message_generation
)

# Add message files
add_message_files(
  FILES
  Detection2D.msg
  Detections2D.msg
)

# Generate messages
generate_messages(
  DEPENDENCIES
  std_msgs
  sensor_msgs
)

catkin_package(
  CATKIN_DEPENDS 
  roscpp
  rospy
  std_msgs
  sensor_msgs
  cv_bridge
  image_transport
  message_runtime
)

include_directories(
  ${catkin_INCLUDE_DIRS}
)

# Python scripts installation
catkin_install_python(PROGRAMS
  scripts/yolov8_detector_node.py
  scripts/gsconv.py
  scripts/modified_yolov8.py
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

# Install launch files
install(DIRECTORY launch/
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/launch
)

# Install rviz configs
install(DIRECTORY rviz/
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/rviz
)