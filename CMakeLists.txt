cmake_minimum_required(VERSION 3.8)
project(ros2_pub_sub_cpp)


#  ____                            _                 _
# |  _ \  ___ _ __   ___ _ __   __| | ___ _ __   ___(_) ___  ___
# | | | |/ _ \ '_ \ / _ \ '_ \ / _` |/ _ \ '_ \ / __| |/ _ \/ __|
# | |_| |  __/ |_) |  __/ | | | (_| |  __/ | | | (__| |  __/\__ \
# |____/ \___| .__/ \___|_| |_|\__,_|\___|_| |_|\___|_|\___||___/
#            |_|
find_package(ament_cmake REQUIRED)

set(ROS2_REQUIRED_COMPONENTS
    rclcpp
)
foreach(COMPONENT ${ROS2_REQUIRED_COMPONENTS})
    find_package(${COMPONENT} REQUIRED)
endforeach()


#  _____                     _        _     _           
# | ____|_  _____  ___ _   _| |_ __ _| |__ | | ___  ___ 
# |  _| \ \/ / _ \/ __| | | | __/ _` | '_ \| |/ _ \/ __|
# | |___ >  <  __/ (__| |_| | || (_| | |_) | |  __/\__ \
# |_____/_/\_\___|\___|\__,_|\__\__,_|_.__/|_|\___||___/
#                                                       
# Subscriber
add_executable(
    subscriber
    ${CMAKE_CURRENT_LIST_DIR}/src/subscriber.cpp
)
ament_target_dependencies(
    subscriber
    ${ROS2_REQUIRED_COMPONENTS}
)

# Publisher
add_executable(
    publisher
    ${CMAKE_CURRENT_LIST_DIR}/src/publisher.cpp
)
ament_target_dependencies(
    publisher
    ${ROS2_REQUIRED_COMPONENTS}
)


#  ___           _        _ _
# |_ _|_ __  ___| |_ __ _| | |
#  | || '_ \/ __| __/ _` | | |
#  | || | | \__ \ || (_| | | |
# |___|_| |_|___/\__\__,_|_|_|
#
install(
    TARGETS subscriber publisher
    DESTINATION lib/${PROJECT_NAME}
)

ament_package()
