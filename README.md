# Path_Planning

# README

## 引言

本实验为差分导航局部路径规划实验，重点是要掌握导航地图局部路径规划算法，大地主题解算方法以及UTM投影算法。实验中，首先要加载先前存储的全局地图文件，并将接收的实时车辆位姿信息与地图中的点匹配，在找到对应点之后，规划出当前位置前方10~30米范围的局部路径。本实验包含2个ROS包和1个.py文件：xfgps_parse、xfpath_plan和main.py。其中，xfgps_parse的ROS包为差分导航驱动模块，负责读取导航串口数据并解析，将解析后的实时经纬度、高度、航向角、RTK状态、车速等信息发送给xfpath_plan节点。xfpath_plan的ROS包为局部路径规划模块，负责加载全局地图文件，并将接收到的车辆实时位置信息与全局地图进行匹配，在找到对应位置点之后，规划前方的局部路径。main.py为UI控制界面，负责开始程序、绘制地图路径等使能信号的发送，车辆当前位姿信息的显示，规划路径长度的选择和全局路径、局部路径的绘制与显示。各ROS包之间的消息通信如下图所示：

![node](https://raw.githubusercontent.com/GuoXiaoxiao1/Path_Planning/master/Plan/Node.png)

## 依赖

- ros kinect(Ubuntu 16.04)
- pyqt5

## 编译

```
% cd PathPlanning_Projection/src
% sudo chmod -R 777 *
% cd ..
% catkin_make
    
```

## 运行

本实验有两种运行方式，既可在线运行，也可离线运行。在线运行是指直接从导航设备的串口读取数据并解析，因此需要运行导航驱动xfgps_parse的ROS包，利用其来提供解析后的车辆实时经纬度、航向角、RTK状态、车速等信息；离线运行是指在有采集好的解析后导航数据的前提下，可通过播放bag包的形式来提供实时的经纬度信息。

1.在线运行：

```
% cd PathPlanning_Projection
% source devel/setup.bash
% roslaunch xfpath_plan path_plan_online.launch

```

2.离线运行：

```
% cd PathPlanning_Projection
% source devel/setup.bash
% roslaunch xfpath_plan path_plan_offline.launch

```

- 在UI界面中，点击“Start”按钮开始程序。
- 点击“Load map”按钮加载利用《差分导航数据解析及单路径地图采集模块》采集的全局地图，并显示地图存储的路径信息。
- 点击“Draw map”按钮绘制全局地图，并在右侧画图区显示。
- 选择想要规划的局部路径长度：10~30米，点击“Path planning”按钮开始规划。根据接收到的当前车辆位置与全局地图中的点进行匹配，从而规划出前方一定范围内的局部路径，并显示在右侧画图区。
- 画图区域的不同路径分别用三种颜色表示，其中：紫色表示全局路径，红色表示车辆的当前位置，绿色表示根据车辆位置规划的前方局部路径。
- 更多UI界面操作信息与显示信息可参考本实验的实验指导书中示例软件展示部分。

## 示例demo

![demo](https://raw.githubusercontent.com/GuoXiaoxiao1/Path_Planning/master/Plan/UI.png) 

## 联系我们

如果您有相关实验课件的其他需要，或向我们反馈一些本实验存在的BUG,或想向我们提供一些特殊场景的实验数据，请联系我们：

```
Email: lemonxiaoxiao9@163.com

```

注：反馈数据的格式应为rosbag包
