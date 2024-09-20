## 目录：

1. Moveit fake controller运行
2. 导航+Moveit+Gazebo+仿真环境运行
3. Moveit独立控制真实机械臂
4. Movet联合控制真实机械臂+底盘规划
5. Moveit独立控制真实onRobot夹爪
6. Moveit联合控制真实机械臂+onRobot夹爪
7. Moveit联合控制真实机械臂+onRobot夹爪+底盘
8. 参数的说明 


## fake controller运行
```shell
roslaunch kmriiwa_moveit move_group.launch fake_execution:=true load_realsense_topic:=false merge_real_RG2FT_kmriiwa:=false load_simulation:=false load_real_RG2FT:=false load_real_kmriiwa:=false load_realsense:=false load_real_move_base:=false
```

- 在rviz的Motion Planning中选择kmriiwa_manipulator的Planning Group即可进行机械臂的fake规划，选择gripper的Planning Group即可进行onRobot夹爪的fake规划，后面的运行同理。
##   导航+Moveit+Gazebo仿真环境运行
```shell
roslaunch kmriiwa_gazebo gazebo_pick_place_demo.launch  load_realsense:=false 
#启动gazebo
roslaunch kmriiwa_bringup planning_stack_bringup.launch load_realsense_topic:=false merge_real_RG2FT_kmriiwa:=false load_simulation:=true load_real_RG2FT:=false load_real_kmriiwa:=false load_realsense:=false load_move_group_rviz:=false load_real_move_base:=false
#启动move_group/导航/rviz

#如果不需要启动导航，只启动move_group/rviz，则:
roslaunch kmriiwa_moveit move_group.launch load_realsense_topic:=false merge_real_RG2FT_kmriiwa:=false load_simulation:=true load_real_RG2FT:=false load_real_kmriiwa:=false load_realsense:=false load_real_move_base:=false load_move_group_rviz:=true
```

- 选中打开rviz上方Panels中的Tools，点击2D Nav Goal可进行导航规划，点击2D Pose Estimate可进行机器人在map地图中的定位。
## Moveit独立控制真实机械臂
```shell
roslaunch kmriiwa_moveit move_group.launch load_realsense_topic:=false merge_real_RG2FT_kmriiwa:=false load_simulation:=false load_real_RG2FT:=false load_real_kmriiwa:=true load_realsense:=true load_real_move_base:=false
```
## Moveit联合控制真实机械臂+底盘
```shell
roslaunch kmriiwa_bringup planning_stack_bringup.launch load_realsense_topic:=false merge_real_RG2FT_kmriiwa:=false load_simulation:=false load_real_RG2FT:=false load_real_kmriiwa:=true load_realsense:=true load_real_move_base:=true

```
## Moveit独立控制真实onRobot夹爪
```shell
roslaunch kmriiwa_moveit move_group.launch load_realsense_topic:=false merge_real_RG2FT_kmriiwa:=false load_simulation:=false load_real_RG2FT:=true load_real_kmriiwa:=false load_realsense:=true load_real_move_base:=false

```
## Moveit联合控制真实机械臂+onRobot夹爪
```shell
roslaunch kmriiwa_moveit move_group.launch load_realsense_topic:=false merge_real_RG2FT_kmriiwa:=true load_simulation:=false load_real_RG2FT:=false load_real_kmriiwa:=false load_realsense:=true load_real_move_base:=false
```
## Moveit联合控制真实机械臂+onRobot夹爪+底盘
```shell
roslaunch kmriiwa_bringup planning_stack_bringup.launch load_realsense_topic:=false merge_real_RG2FT_kmriiwa:=true load_simulation:=false load_real_RG2FT:=false load_real_kmriiwa:=false load_realsense:=true load_real_move_base:=true
```
## 参数的说明

1. 如果想改变导航的速度，需访问：
```shell
kmriiwa_ros_stack/kmriiwa_navigation/config/local_planner.yaml
```

2. 要想改变局部和全局地图障碍物的半径，需访问：
```shell
src/kmriiwa_ros_stack/kmriiwa_navigation/config/local_costmap.yaml
src/kmriiwa_ros_stack/kmriiwa_navigation/config/global_costmap_static_map.yaml
```
