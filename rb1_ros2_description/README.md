# The rb1_ros2_description package

This package contains a ROS2 robot model description for Robotnik's RB-1 mobile base.   

## Disclaimer:  
This package only modifies/adapts files from these repositories/packages:  
- [RobotnikAutomation/rb1_base_sim](https://github.com/RobotnikAutomation/rb1_base_sim) licensed under the BSD 2-Clause "Simplified" License
- [RobotnikAutomation/rb1_base_common/rb1_base_description](https://github.com/RobotnikAutomation/rb1_base_common/tree/melodic-devel/rb1_base_description), licensed under the BSD License
- [RobotnikAutomation/robotnik_sensors],(https://github.com/RobotnikAutomation/robotnik_sensors) licensed under the BSD License


## Launch the simulation and spawn the robot

This will also launch the diff drive controller 
```
ros2 launch rb1_ros2_description rb1_ros2_xacro.launch.py
```

## Move the robot:

### Command to move the robot using teleop:
```
ros2 run teleop_twist_keyboard teleop_twist_keyboard --ros-args --remap /cmd_vel:=/diffbot_base_controller/cmd_vel_unstamped
```

### Send directly Twist commands to the robot:
```
ros2 topic pub --rate 10 diffbot_base_controller/cmd_vel_unstamped geometry_msgs/msg/Twist "{linear: {x: 0.0, y: 0, z: 0.0}, angular: {x: 0.0,y: 0.0, z: 0.0}}"
```

## Lift the elevator

### Load the elevator controller 
After launching the simulation, you can load the elevator lifting unit 
controller via the following command: 
```
ros2 control load_controller --set-state start effort_controllers
```
*Please note that the maximum effort command that can be sent to the elevator joint is 10.0 
to move it up, and the minimum one is 0.0 to move it down.*

### Command to move the elevator up
```
ros2 topic pub /effort_controllers/commands std_msgs/msg/Float64MultiArray "data: [10.0]" --once
```

### Command to move the elevator down
```
ros2 topic pub /effort_controllers/commands std_msgs/msg/Float64MultiArray "data: [0.0]" --once
```




