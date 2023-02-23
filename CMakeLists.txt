cmake_minimum_required(VERSION 3.8)
project(my_package)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(kobuki_ros_interfaces REQUIRED)
find_package(std_msgs REQUIRED)

set(dependencies
  rclcpp
  kobuki_ros_interfaces
  std_msgs
)

include_directories(include)

add_library(${PROJECT_NAME} SHARED
  src/my_package/DebugNode.cpp
)
ament_target_dependencies(${PROJECT_NAME} ${dependencies})

add_executable(my_package_exec src/my_package_main.cpp)
ament_target_dependencies(avoid_obstacle ${dependencies})
target_link_libraries(avoid_obstacle ${PROJECT_NAME})

install(TARGETS
  my_package_exec
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION lib/${PROJECT_NAME}
)

install(DIRECTORY config launch DESTINATION share/${PROJECT_NAME})

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()

  set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
