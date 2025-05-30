cmake_minimum_required(VERSION 3.8)
project(moveit2_scripts)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(rclcpp_action REQUIRED)
find_package(moveit_core REQUIRED)
find_package(moveit_ros_planning REQUIRED)
find_package(moveit_ros_planning_interface REQUIRED)
find_package(interactive_markers REQUIRED)
find_package(geometric_shapes REQUIRED)
find_package(control_msgs REQUIRED)
find_package(moveit_msgs REQUIRED)

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

# Generate the executable
add_executable(joint_space_trajectory src/joint_space_trajectory.cpp)
target_include_directories(joint_space_trajectory PUBLIC include)
ament_target_dependencies(joint_space_trajectory
    ament_cmake
    rclcpp
    rclcpp_action
    moveit_core
    moveit_ros_planning_interface
    interactive_markers
    moveit_ros_planning
    control_msgs)

add_executable(goal_pose_trajectory src/goal_pose_trajectory.cpp)
target_include_directories(goal_pose_trajectory PUBLIC include)
ament_target_dependencies(goal_pose_trajectory
    ament_cmake
    rclcpp
    rclcpp_action
    moveit_core
    moveit_ros_planning_interface
    interactive_markers
    moveit_ros_planning
    control_msgs
)

add_executable(double_motion_trajectory src/double_motion_trajectory.cpp)
target_include_directories(double_motion_trajectory PUBLIC include)
ament_target_dependencies(double_motion_trajectory
    ament_cmake
    rclcpp
    rclcpp_action
    moveit_core
    moveit_ros_planning_interface
    interactive_markers
    moveit_ros_planning
    control_msgs
)

# Gripper control
add_executable(gripper_control src/gripper_control.cpp)
target_include_directories(gripper_control PUBLIC include)
ament_target_dependencies(gripper_control
    ament_cmake
    rclcpp
    rclcpp_action
    moveit_core
    moveit_ros_planning_interface
    interactive_markers
    moveit_ros_planning
    control_msgs
)

# approach retreat node
add_executable(approach_retreat_trajectory src/approach_retreat_trajectory.cpp)
target_include_directories(approach_retreat_trajectory PUBLIC include)
ament_target_dependencies(approach_retreat_trajectory
    ament_cmake
    rclcpp
    rclcpp_action
    moveit_core
    moveit_ros_planning_interface
    interactive_markers
    moveit_ros_planning
    control_msgs
)

# cartesian approach retreat node
add_executable(cartesian_trajectory src/cartesian_trajectory.cpp)
target_include_directories(cartesian_trajectory PUBLIC include)
ament_target_dependencies(cartesian_trajectory
    ament_cmake
    rclcpp
    rclcpp_action
    moveit_core
    moveit_ros_planning_interface
    interactive_markers
    moveit_ros_planning
    control_msgs
)

# draw x cartesian approach retreat node
add_executable(draw_x_cartesian_trajectory src/draw_x_cartesian_trajectory.cpp)
target_include_directories(draw_x_cartesian_trajectory PUBLIC include)
ament_target_dependencies(draw_x_cartesian_trajectory
    ament_cmake
    rclcpp
    rclcpp_action
    moveit_core
    moveit_ros_planning_interface
    interactive_markers
    moveit_ros_planning
    control_msgs
)

# kinematic plugin trajectory
add_executable(kinematics_plugin_trajectory src/kinematics_plugin_trajectory.cpp)
target_include_directories(kinematics_plugin_trajectory PUBLIC include)
ament_target_dependencies(kinematics_plugin_trajectory
    ament_cmake
    rclcpp
    rclcpp_action
    moveit_core
    moveit_ros_planning_interface
    interactive_markers
    moveit_ros_planning
    control_msgs
)

# kinematic plugin trajectory
add_executable(pick_and_place_trajectory src/pick_and_place_trajectory.cpp)
target_include_directories(pick_and_place_trajectory PUBLIC include)
ament_target_dependencies(pick_and_place_trajectory
    ament_cmake
    rclcpp
    rclcpp_action
    moveit_core
    moveit_ros_planning_interface
    interactive_markers
    moveit_ros_planning
    control_msgs
)

# Install the executable
install(TARGETS 
    joint_space_trajectory
	goal_pose_trajectory
	double_motion_trajectory
	gripper_control
	approach_retreat_trajectory
	cartesian_trajectory
	draw_x_cartesian_trajectory
	kinematics_plugin_trajectory
	pick_and_place_trajectory
    DESTINATION lib/${PROJECT_NAME}
)

# Install the launch file
install(DIRECTORY 
    launch
    DESTINATION share/${PROJECT_NAME}
)

ament_package()
