cmake_minimum_required(VERSION 3.5)
project(i2c_device_ros)

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

# Find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)

# Include directories
include_directories(
  include
  ${rclcpp_INCLUDE_DIRS}
)

# Declare the package
find_package(ament_lint_auto)
ament_package()

# Add a shared library
add_library(${PROJECT_NAME} SHARED
  src/i2c_device.cpp
)

# Link against ROS 2 libraries
target_link_libraries(${PROJECT_NAME}
  ${rclcpp_LIBRARIES}
)

# Install rules
install(TARGETS ${PROJECT_NAME}
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin
)

install(DIRECTORY include/
  DESTINATION include
)

# Add test targets if needed
if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()
