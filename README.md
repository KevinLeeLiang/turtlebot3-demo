# turtlebot3-demo
# [ros2与turtlebot3仿真教程-安装ros2](https://www.ncnynl.com/archives/202008/3845.html)

**ros2与turtlebot3仿真教程-安装ros2**

说明：

- 介绍如何安装ros2 foxy版本

步骤：

- apt安装，[参考教程](https://www.ncnynl.com/archives/201802/2278.html)
    
- 源码安装，[参考教程](https://www.ncnynl.com/archives/201801/2274.html)
    
- 简单步骤：
    
- 安装
    

```
sudo apt install ros-foxy-ros-desktop
```

- 安装colcon

```
$ sudo apt install python3-colcon-common-extensions
```

- 安装foxy

```
$ sudo apt install ros-foxy-cartographer
```

- 安装cartographer建图

```
$ sudo apt install ros-foxy-cartographer
$ sudo apt install ros-foxy-cartographer-ros
```

- 安装导航包

```
$ sudo apt install ros-foxy-navigation2
$ sudo apt install ros-foxy-nav2-bringup
```

- 安装vcstool工具

```
$ sudo apt install python3-vcstool
```

**[利用鱼香ros提供的ros一键安装脚本](https://fishros.org.cn/forum/topic/20/%E5%B0%8F%E9%B1%BC%E7%9A%84%E4%B8%80%E9%94%AE%E5%AE%89%E8%A3%85%E7%B3%BB%E5%88%97?lang=zh-CN)**

**<font face="楷体" color=Red size=4> 因为国内墙的原因，安装过程会有各种各样无法成功的困扰，在这里使用一键安装脚本，帮助替换国内源和配置安装版本，非常方便，这里铬铁感谢[@小鱼](https://github.com/fishros) </font>**

## 一键安装指令

```shell
wget http://fishros.com/install -O fishros && . fishros
```

## 常用教程

- [一键安装微信使用指南](https://fishros.org.cn/forum/topic/140/%E4%B8%80%E9%94%AE%E5%AE%89%E8%A3%85%E5%BE%AE%E4%BF%A1%E4%BD%BF%E7%94%A8%E6%8C%87%E5%8D%97)

## 目前支持工具

- 一键安装:ROS(支持ROS和ROS2,树莓派Jetson) [贡献@小鱼](https://github.com/fishros)
- 一键安装:VsCode(支持amd64和arm64) [贡献@小鱼](https://github.com/fishros)
- 一键安装:github桌面版(小鱼常用的github客户端) [贡献@小鱼](https://github.com/fishros)
- 一键安装:nodejs开发环境(通过nodejs可以预览小鱼官网噢 [贡献@小鱼](https://github.com/fishros)
- 一键配置:rosdep(小鱼的rosdepc,又快又好用) [贡献@小鱼](https://github.com/fishros)
- 一键配置:ROS环境(快速更新ROS环境设置,自动生成环境选择) [贡献@小鱼](https://github.com/fishros)
- 一键配置:系统源(更换系统源,支持全版本Ubuntu系统) [贡献@小鱼](https://github.com/fishros)
- 一键安装:Docker(支持amd64和arm64) [贡献@alyssa](https://github.com/alyssa1024)
- 一键安装:cartographer [贡献@小鱼&Catalpa](https://github.com/fishros)
- 一键安装:微信客户端 [贡献@小鱼](https://github.com/fishros)

# [ros2与turtlebot3仿真教程-安装turtlebot3](https://www.ncnynl.com/archives/202008/3846.html)

**ros2与turtlebot3仿真教程-安装turtlebot3**

说明：

- 介绍如何在ros2安装turtlebot3

步骤：

- 下载编译

```
$ mkdir -p ~/tb3_ws/src
$ cd ~/tb3_ws
#foxy版本
$wget https://raw.githubusercontent.com/ROBOTIS-GIT/turtlebot3/foxy-devel/turtlebot3.repos

#galactic版本
#$ wget https://raw.githubusercontent.com/ROBOTIS-GIT/turtlebot3/galactic-devel/turtlebot3.repos
```

**<font face="楷体" color=Red size=4> 因为国内墙的原因，https://raw.githubusercontent.com 无法打开，本文采取方式是在 https://raw.githubusercontent.com/ROBOTIS-GIT/ 下clone turtlebot3，turtlebot3_msgs，turtlebot3_simulations，DynamixelSDK和hls_lfcd_lds_driver </font>**
```
cd src/
git clone https://github.com/ROBOTIS-GIT/turtlebot3.git
git clone https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git
git clone https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
git clone https://github.com/ROBOTIS-GIT/DynamixelSDK.git
git clone https://github.com/ROBOTIS-GIT/hls_lfcd_lds_driver.git
```
分别到clone代码的文件夹下将代码切换到foxy分支，然后执行下面质量进行编译

```
$ vcs import src < turtlebot3.repos
$ colcon build --symlink-install
```

# [ros2与turtlebot3仿真教程-启动gazebo不同环境](https://www.ncnynl.com/archives/202008/3847.html)

**ros2与turtlebot3仿真教程-启动gazebo不同环境**

说明：

- 介绍如何在ros2下使用gazebo
- 默认安装foxy已经安装了gezebo11.0

步骤：

- 下载gazebo的模型，加速运行gazebo

```
cd ~/.gazebo/ 
git clone https://github.com/osrf/gazebo_models models
```

- 需要删除.git目录，要不运行会出错

```
rm -rf models/.git
```

- 设置GAZEBO\_MODEL\_PATH变量, 指定机器人类型为burger

```
$ echo 'export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH:~/tb3_ws/src/turtlebot3/turtlebot3_simulations/turtlebot3_gazebo/models' >> ~/.bashrc
$ echo 'export TURTLEBOT3_MODEL=burger' >> ~/.bashrc
$ source ~/.bashrc
```

**启动Fake Node**

- 启动Fake Node

```
 $ ros2 launch turtlebot3_fake_node turtlebot3_fake_node.launch.py
```

- 启动后弹出rviz，并显示小车模型
- 启动键盘控制

```
$ ros2 run turtlebot3_teleop teleop_keyboard
```

- 效果图如下：

![请输入图片描述](http://images.ncnynl.com/ros2/2020/ros2-turtlebot3-fake-node.png)

**启动empty地图**

- 新开终端，启动gezebo，并带有empty地图

```
$ ros2 launch turtlebot3_gazebo empty_world.launch.py
```

- 效果如下：

![请输入图片描述](http://images.ncnynl.com/ros2/2020/turtlebot3_empty_world.png)

**启动world地图**

- 新开终端，启动gezebo，并带有world地图

```
$ ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```

- 效果如下：

![请输入图片描述](http://images.ncnynl.com/ros2/2020/gazebo_world.png)

**启动house地图**

- 新开终端，启动gezebo，并带有house地图

```
$ ros2 launch turtlebot3_gazebo turtlebot3_house.launch.py
```

- 效果如下：

![请输入图片描述](http://images.ncnynl.com/ros2/2020/turtlebot3_house.png)

![请输入图片描述](http://images.ncnynl.com/ros2/2020/turtlebot3_house1.png)

# [ros2与turtlebot3仿真教程-turtlebot3遥控](https://www.ncnynl.com/archives/202008/3848.html)

**ros2与turtlebot3仿真教程-turtlebot3遥控**

说明：

- 介绍如何控制小车移动

步骤：

- 新开终端，启动gezebo

```
$ ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```

- 启动键盘控制

```
$ ros2 run turtlebot3_teleop teleop_keyboard
```

# [ros2与turtlebot3仿真教程-rviz2模型显示](https://www.ncnynl.com/archives/202008/3850.html)

**ros2与turtlebot3仿真教程-rviz2模型显示**

说明：

- 介绍如何利用rviz2来显示小车模型

步骤：

- 启动gazebo

```
$ ros2 launch turtlebot3_gazebo turtlebot3_house.launch.py
```

- 启动rviz2

```
$ ros2 launch turtlebot3_bringup rviz2.launch.py
```

- 效果如下：

![请输入图片描述](http://images.ncnynl.com/ros2/2020/ros2-turtlebot3-rviz2.png)

# [ros2与turtlebot3仿真教程-turtlebot3建图](https://www.ncnynl.com/archives/202008/3851.html)

**ros2与turtlebot3仿真教程-turtlebot3建图**

说明：

- 介绍如何ros2下实现turtlebot3建图

步骤：

- 新开终端，运行gazebo

```
$ ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```

- 新开终端，运行建图

```
$ ros2 launch turtlebot3_cartographer cartographer.launch.py use_sim_time:=True
```

- 新开终端，启动键盘

```
$ ros2 run turtlebot3_teleop teleop_keyboard
```

- 控制小车随机移动，并进行建图，并查看建立的地图，差不多后，保存地图。
    
- 效果如下：
    

![请输入图片描述](http://images.ncnynl.com/ros2/2020/gazebo_cartographer.png)

- 新开终端，保存地图

```
$ ros2 run nav2_map_server map_saver_cli -f ~/map
```

- 地图保存在目录下

# [ros2与turtlebot3仿真教程-turtlebot3导航](https://www.ncnynl.com/archives/202008/3852.html)

**ros2与turtlebot3仿真教程-turtlebot3导航**

说明：

- 介绍如何ros2下进行导航

步骤：

- 新开终端，运行gazebo

```
$ ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```

- 新开终端，导航

```
$ ros2 launch turtlebot3_navigation2 navigation2.launch.py use_sim_time:=True map:=/home/ubuntu/map.yaml
```

- 需要指定地图的绝对路径，要不地图不能正常加载
- 需要修改navigation2.launch.py，变更nav2\_bringup\_launch.py为bringup\_launch.py要不提示文件不能找到
- 点击2D Pose Estimate初始化位姿，点击Navigation2 Goal选择目标点进行导航
- 效果如下：

![请输入图片描述](http://images.ncnynl.com/ros2/2020/gazebo_navigation2.png)