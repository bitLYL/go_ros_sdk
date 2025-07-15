# go_ros_sdk
基于go2_SDK和ROS1实现的宇树机器狗导航系统。通过改写SDK，实现了ROS1话题(IMU、机器人位姿、雷达)的发布，并构建了支持大模型语言控制的导航框架。系统支持两种导航方式：传统RVIZ目标点导航，以及通过大模型解析文本指令(如方向、距离)实现导航。文章详细说明了SDK安装、例程编译和导航框架部署的步骤，并提供了开源代码(GitHub: qoiu)。大模型部分采用本地知识库或API调用实现任务分解。该系统为go2机器狗提供了完整的ROS1导航解决方案。

csdn详细教程：
https://blog.csdn.net/qq_54038361/article/details/149361407?sharetype=blogdetail&sharerId=149361407&sharerefer=PC&sharesource=qq_54038361&spm=1011.2480.3001.8118

 ######SDK启动##########
 
 1.启动imu发布，位置发布，
 
  base_link->map 雷达发布节点
  
  进入intiree_SDK2文件夹
  
  cd build .cd bin
  
  sudo ./go2_imu_pub_6
  
  
 2.启动cmd_vel速度控制接口
 
  sudo ./go2_move_sub eth0

3.雷达信息显示，

  进入intiree_SDK2文件夹
  
  cd build .cd bin
  
  sudo ./go2_lidar_pub3 eth0
  

######传统rviz导航#####

1.进入lyl_ws文件夹

2.roslaunch robot_navigation robot_navigation.launch

3.rviz 添加goal规划

######大模型类导航######

 1.进入lyl_ws文件夹
 
 roslaunch robot_llm robot_llm.launch  
 
 2.发布测试数据
 source ~/lyl_ws/devel/setup.bash
 rostopic pub /llm custom_msgs/MoveCommand "{x: 0.0, y: 0.0, direction: [4], distance: 0.7}" 

