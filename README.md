rosbag中发布的节点有：
    /clock
    /driver/encoder
    /driver/eul
    /driver/imu
    /driver/mag
    /driver/scan
    /rosout
    /rosout_agg

一、diver/scan
Scan是激光数据,按一圈激光扫描的顺序和参数定义点云数据。
其中含有的字段有：
Header header              # Header是一个结构体,包含了seq,stamp,frame_id,其中seq指的是扫描顺序增加的id,stamp包含了开始扫描的时间和与开始扫描的时间差,frame_id是扫描的参考系名称.注意扫描是逆时针从正前方开始扫描的.
float32 angle_min          # 开始扫描的角度(角度)
float32 angle_max          # 结束扫描的角度(角度)
float32 angle_increment    # 每一次扫描增加的角度(角度)
float32 time_increment     # 测量的时间间隔(s)
float32 scan_time          # 扫描的时间间隔(s)
float32 range_min          # 距离最小值(m)
float32 range_max          # 距离最大值(m)
float32[] ranges           # 距离数组(长度360)(注意: 值 < range_min 或 > range_max 应当被丢弃)
float32[] intensities      # 与设备有关,强度数组(长度360)
订阅数据见附件

二、diver/imu
imu是 ROS 中用于表示惯性测量单元（IMU）数据的消息类型。通常用于表示物体的线性加速度、角速度和方向信息。
其中含有的主要字段有：
1. header                  #消息头，包含时间戳和坐标系信息，用于关联消息的时间和空间信息。
2. linear_acceleration     #包含线性加速度的三个分量（x、y 和 z 方向）。
3. angular_velocity        #包含角速度的三个分量（绕 x、y 和 z 轴的旋转速度）。
4. orientation             #表示物体的方向。Quaternion 是一种四元数表示法，用于描述物体的旋转。

三、diver/encoder
encoder应该表示的是导航中的里程计消息。
含有的字段有：
Header header                                  # 像前面的一样，包含有包含了seq,stamp,frame_id
string child_frame_id                          # 字符串消息child_frame_id
geometry_msgs/PoseWithCovariance pose          # 这表示在具有不确定性的自由空间中的姿势。
geometry_msgs/TwistWithCovariance twist        # 这表示自由空间中具有不确定性的速度。

四、diver/mag
mag应该是磁场传感器的数据，测量特定位置的磁场矢量。
含有的字段有：
Header header                                  # 时间戳是测量场的时间，frame_id 是场测量的位置和方向
geometry_msgs/Vector3 magnetic_field           # 场向量的x、y 和 z 分量
float64[9] magnetic_field_covariance           # 关于 x、y、z 轴的行主数

五、clock
clock话题由playbag节点发布 提供仿真时间，而其他所有使用时间信息的节点会订阅该话题获得仿真时间，从而使整个系统使用仿真时间。

六、rosout
rosout用来收集和记录节点调试输出信息

七、rosout_agg
_agg 后缀是指消息由 rosout 节点汇集。在 /rosout 主题上发布的每条消息都会由 rosout 节点发布在 /rosout_agg 主题上。这是为了减少调试的开销。
