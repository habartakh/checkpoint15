# The rb1_ros2_description package

This package contains a ROS2 robot model description for Robotnik's RB-1 mobile base.   

## Disclaimer:  
This package only modifies/adapts files from these repositories/packages:  
- [RobotnikAutomation/rb1_base_sim](https://github.com/RobotnikAutomation/rb1_base_sim) licensed under the BSD 2-Clause "Simplified" License
- [RobotnikAutomation/rb1_base_common/rb1_base_description](https://github.com/RobotnikAutomation/rb1_base_common/tree/melodic-devel/rb1_base_description), licensed under the BSD License
- [RobotnikAutomation/robotnik_sensors],(https://github.com/RobotnikAutomation/robotnik_sensors) licensed under the BSD License

## Move the robot

# Command to move the robot using teleop:

ros2 run teleop_twist_keyboard teleop_twist_keyboard --ros-args --remap /cmd_vel:=/diffbot_base_controller/cmd_vel_unstamped


# Send directly Twist commands to the robot:

ros2 topic pub --rate 10 diffbot_base_controller/cmd_vel_unstamped geometry_msgs/msg/Twist "{linear: {x: 0.0, y: 0, z: 0.0}, angular: {x: 0.0,y: 0.0, z: 0.0}}"