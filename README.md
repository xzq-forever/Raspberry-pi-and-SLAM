# Raspberry-pi-and-SLAM
Use Kinect XBOX 360 and Rasberry pi 3 to do SLAM, dispalyed on PC at the same time.<br>

1.Install Ubuntu 16.04 mate for your pi:<br>
https://ubuntu-mate.org/download/<br>

2.Install ROS for your pi:<br>
```
$ sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
$ sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo apt-get install ros-kinetic-desktop-full
$ sudo rosdep init
$ rosdep update
$ source /opt/ros/kinetic/setup.bash
$ echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
$ sudo apt-get install python-rosinstall
```
It may take quite a long time, just let it alone and do anything else.<br>

3.Install something for your pi:<br>
```
$ sudo apt-get install freenect-*
$ sudo apt-get install rtabmap-*
```

4.Export IP(on every terminal):<br>
(1)On your pi:<br>
```
$ export ROS_IP =             //pi's IP
$ export ROS_MASTER_URI =     //pi's IP
```
(2)On your pc:<br>
```
$ export ROS_IP =             //pc's IP
$ export ROS_MASTER_URI =     //pi's IP
```

5.Do it:<br>
(1)On your pi:<br>
```
$ roscore
$ roslaunch freenect_launch freenect.launch depth_registration:=true
$ roslaunch rtabmap_ros rgbd_mapping.launch rtabmap_args:="--delete_db_on_start --Vis/MaxFeatures 500 --Vis/CorType 1 --Mem/ImagePreDecimation 2 --Mem/ImagePostDecimation 2 --Kp/DetectorStrategy 6 --OdomF2M/MaxSize 1000 --Vis/MaxFeatures 600 --Odom/ImageDecimation 2" rtabmapviz:=false
```
http://wiki.ros.org/rtabmap_ros/Tutorials/Advanced%20Parameter%20Tuning<br>
(2)On your pc:<br>
```
$ rosrun rviz rviz //subsribe the topic you need
```
or<br>
```
$ ROS_NAMESPACE=rtabmap rosrun rtabmap_ros rtabmapviz _subscribe_odom_info:=false _frame_id:=camera_link
```

TODO:<br>
Use robot to navigate<br>
