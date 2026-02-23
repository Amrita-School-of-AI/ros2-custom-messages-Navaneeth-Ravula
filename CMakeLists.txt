cmake_minimum_required(VERSION 3.8)
project(ros2_custom_msgs)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(rosidl_default_generators REQUIRED)

# TODO: Generate message interfaces
# Use rosidl_generate_interfaces to generate code for msg/RobotStatus.msg

rosidl_generate_interfaces(${PROJECT_NAME}
  "msg/RobotStatus.msg"
)

# TODO: Add executable target named 'status_publisher'
# 1. Add executable using src/status_publisher.cpp
# 2. Add dependencies for rclcpp
# 3. Link with the generated message interfaces using:
#    rosidl_get_typesupport_target(cpp_typesupport_target ${PROJECT_NAME} "rosidl_typesupport_cpp")
#    target_link_libraries(status_publisher "${cpp_typesupport_target}")
# 4. Install the target
add_executable(status_publisher src/status_publisher.cpp)
ament_target_dependencies(status_publisher rclcpp)

rosidl_get_typesupport_target(cpp_typesupport_target
  ${PROJECT_NAME} "rosidl_typesupport_cpp")

target_link_libraries(status_publisher
  ${cpp_typesupport_target}
)

install(TARGETS
  status_publisher
  DESTINATION lib/${PROJECT_NAME}
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
