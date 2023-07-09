# 简介
- 请结合host_slam功能包操作
- 功能包地址：https://github.com/LeonardoDiCaprio1/host_slam

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
