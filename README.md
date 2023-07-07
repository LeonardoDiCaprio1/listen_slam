# 简介
- 请配合host_slam功能包操作
- 功能包地址：

# 开发环境
- Ubuntu 20.04
- ROS Noetic
# 相关操作步骤
## 1.建图
- (a) 前提需要将下位机的扣板上的IMU3PIN口和上位机的I2C线连接起来，
连接上电池，打开扣板开关,然后执行以下命令。
```
sudo ./chmod.sh
sudo chmod +777 /dev/i2c*
sudo chmod +777 /dev/mpu6050
```
- (b)主机端新建终端，开启slam节点
```
cd third_ws
source devel/setup.bash
roslaunch sophon_robot slam.launch
```
- (c)主机端新建一个终端，键盘控制小车进行建图
```
cd third_ws
source devel/setup.bash
roslaunch sophon_robot teleop_key.py 
```
- (d)主机端新建终端、保存地图
```
cd robot_ws/src/sophon_robot/maps 
./savemap.sh
```
- (e)先自行建立ros包，从机端开启slam节点，订阅相关的主题并查看
```
roslaunch sophon_robot view_slam.launch
```
## 2.导航
- (a)主机端开启导航节点
```
cd third_ws
source devel/setup.bash
roslaunch sophon_robot nav.launch
```
- (b)先自行建立ros包，从机端开启导航可视化
```
 roslaunch sophon_robot view_nav.launch 
```
## 注意事项：
- 修改速度参数：找到与线速度相关的参数，例如max_linear_velocity、min_linear_velocity、linear_acceleration等，然后修改这些参数的值来调整线速度。你可以使用rosparam命令行工具或编写一个ROS节点来修改参数。以下是一个示例使用rosparam工具修改参数的命令：
```
rosparam set /move_base/max_linear_velocity 0.4 
```
- 重新启动导航系统：一旦你修改了速度参数，你需要重新启动导航系统，以使新的参数生效。这可以通过重启导航相关的节点来实现，例如重新启动move_base节点。
```
rosnode kill /move_base  
roslaunch sophon_robot nav.launch  
```
