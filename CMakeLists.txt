cmake_minimum_required(VERSION 3.8)
project(meamr_joystick)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(sensor_msgs REQUIRED)
find_package(std_msgs REQUIRED)
# uncomment the following section in order to fill in
# further dependencies manually.
# find_package(<dependency> REQUIRED)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # comment the line when a copyright and license is added to all source files
  set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # comment the line when this package is in a git repo and when
  # a copyright and license is added to all source files
  set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

install(
  DIRECTORY 
  launch/
  DESTINATION share/${PROJECT_NAME}/launch
)

install(
  DIRECTORY 
  config/
  DESTINATION share/${PROJECT_NAME}/config
)

include_directories(include)

add_executable(joystick_extra_node
  src/joystick_extra_node.cpp
  src/main.cpp
)

ament_target_dependencies(joystick_extra_node
  rclcpp
  sensor_msgs
  std_msgs
)

install(TARGETS
  joystick_extra_node
  DESTINATION lib/${PROJECT_NAME}
)


ament_package()
