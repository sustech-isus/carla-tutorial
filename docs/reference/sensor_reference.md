# 传感器参数参考文档

---
* 传感器参数说明
  *   [__RGB camera(RGB相机)__](#rgb-camera)
  *   [__Depth camera(深度相机)__](#深度相机)
  *   [__Semantic segmentation camera(语义相机)__](#语义分割相机)
  *   [__GNSS sensor(GNSS传感器)__](#gnss传感器)
  *   [__IMU sensor(惯性传感器)__](#imu传感器)
  *   [__LIDAR sensor(激光雷达)__](#lidar-激光雷达-传感器)
  *   [__Semantic LIDAR sensor(语义激光雷达)__](#语义lidar传感器))
  *   [__Radar sensor(毫米波雷达)__](#---radar-sensor毫米波雷达)
* [__配置文件示例__](#配置文件示例)   

---
## RGB camera

> type: `sensor.camera.rgb`

| 输出Topic |输出消息类型|
|---|---|
|/carla/{role_name}/{sensor_id}/image | sensor_msgs/Image |
|/carla/{role_name}/{sensor_id}/camera_info | sensor_msgs/CameraInfo |

RGB相机的作用是作为普通摄像机捕捉场景中的RGB图像。

`sensor_tick` 定义传感器采集数据的快慢。
例如： `sensor_tick = 1.5`， 意味着传感器每1.5s采集一次。默认为0，即尽可能快的采集。

#### RGB相机参数

| 参数名称 | 参数类型     | 默认值  | 参数描述          |
| ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- |
|`id`|string|rgb_camera|传感器ID, 用于区分多路传感器  |
|`spawn_point`|object|{"x": 2.0, "y": 0.0, "z": 2.0, "roll": 0.0, "pitch": 0.0, "yaw": 0.0}|传感器安装位置（车身坐标系）
| `fov`    | float    | 90\.0    | 水平视场角 (单位: 度) |
| `image_size_x`       | int      | 800      | 图像宽度 (像素) |
| `image_size_y`       | int      | 600      | 图像高度 (像素) |
| `sensor_tick`        | float    | 0\.0     | 传感器数据间的仿真时间 (ticks).  |
| `shutter_speed`      | float    | 200\.0   | 相机快门速度 (1.0/s).       |


## 深度相机

> type: `sensor.camera.depth`

| 输出Topic |输出消息类型|
|---|---|
|/carla/{role_name}/{sensor_id}/image | sensor_msgs/Image |
|/carla/{role_name}/{sensor_id}/camera_info | sensor_msgs/CameraInfo |

深度相机可以将场景中的距离信息编码为像素生成深度图像。

在ROS-Bridge中，深度图已经被转换为单通道float32的图像，每个像素值即为实际距离(米)。

#### 深度相机参数

| 参数名称 | 参数类型     | 默认值  | 参数描述          |
| ----------------------------- | ----------------------------- | ----------------------------- | ----------------------------- |
|`id`|string|rgb_camera|传感器ID, 用于区分多路传感器  |
|`spawn_point`|object|{"x": 2.0, "y": 0.0, "z": 2.0, "roll": 0.0, "pitch": 0.0, "yaw": 0.0}|传感器安装位置（车身坐标系）
| `fov`    | float    | 90\.0    | 水平视场角 (单位: 度) |
| `image_size_x`       | int      | 800      | 图像宽度 (像素) |
| `image_size_y`       | int      | 600      | 图像高度 (像素) |
| `sensor_tick`        | float    | 0\.0     | 传感器数据间的仿真时间 (ticks).  |

## 语义分割相机

> type: `sensor.camera.semantic_segmentation`

| 输出Topic |输出消息类型|
|---|---|
|/carla/{role_name}/{sensor_id}/image | sensor_msgs/Image |
|/carla/{role_name}/{sensor_id}/camera_info | sensor_msgs/CameraInfo |

语义相机对所看到的每一个物体进行分类，根据其标签以不同的颜色显示出来。

#### 语义相机参数

| 参数名称 | 参数类型     | 默认值  | 参数描述          |
| ----------------------------- | ----------------------------- | ----------------------------- | ----------------------------- |
|`id`|string|rgb_camera|传感器ID, 用于区分多路传感器  |
|`spawn_point`|object|{"x": 2.0, "y": 0.0, "z": 2.0, "roll": 0.0, "pitch": 0.0, "yaw": 0.0}|传感器安装位置（车身坐标系）
| `fov`    | float    | 90\.0    | 水平视场角 (单位: 度) |
| `image_size_x`       | int      | 800      | 图像宽度 (像素) |
| `image_size_y`       | int      | 600      | 图像高度 (像素) |
| `sensor_tick`        | float    | 0\.0     | 传感器数据间的仿真时间 (ticks).  |

---
## GNSS传感器

> type: `sensor.other.gnss`

| 输出Topic |输出消息类型|
|---|---|
|/carla/{role_name}/gnss | sensor_msgs/NavSatFix |

反馈父对象当前的 gnss 位置。这是通过在OpenDRIVE地图的定义，结合仿真器参考位置来计算的。

#### GNSS参数


| 参数名称 | 参数类型     | 默认值  | 参数描述          |
| ------------------- | ------------------- | ------------------- | ------------------- |
|`spawn_point`|object|{"x": 2.0, "y": 0.0, "z": 2.0, "roll": 0.0, "pitch": 0.0, "yaw": 0.0}|传感器安装位置（车身坐标系）
| `noise_alt_bias`   | float  | 0\.0   | 海拔高度的噪声模型中的均值    |
| `noise_alt_stddev` | float  | 0\.0   | 海拔高度的噪声模型中的标准差 |
| `noise_lat_bias`   | float  | 0\.0   | 纬度噪声模型的均值 |
| `noise_lat_stddev` | float  | 0\.0   | 纬度噪声模型的标准差  |
| `noise_lon_bias`   | float  | 0\.0   | 经度噪声模型的均值   |
| `noise_lon_stddev` | float  | 0\.0   | 经度噪声模型的标准差 |
| `sensor_tick`      | float  | 0\.0   | 传感器数据间的仿真时间 (ticks).  |

---
## IMU传感器

> type: `sensor.other.imu`

| 输出Topic |输出消息类型|
|---|---|
|/carla/{role_name}/imu| sensor_msgs/Imu |

提供父对象的加速度计、陀螺仪、磁力计的传感器测量值。 数据由对象当前状态采集获得。

#### IMU参数


| 参数名称 | 参数类型     | 默认值  | 参数描述          |
| -------------------------------- | -------------------------------- | -------------------------------- | -------------------------------- |
|`spawn_point`|object|{"x": 2.0, "y": 0.0, "z": 2.0, "roll": 0.0, "pitch": 0.0, "yaw": 0.0}|传感器安装位置（车身坐标系）
| `noise_accel_stddev_x`          | float   | 0\.0    | 加速度计噪声模型标准差 (X轴)  |
| `noise_accel_stddev_y`          | float   | 0\.0    | 加速度计噪声模型标准差 (Y轴)   |
| `noise_accel_stddev_z`          | float   | 0\.0    | 加速度计噪声模型标准差 (Z轴)  |
| `noise_gyro_bias_x` | float   | 0\.0    | 陀螺仪噪声模型均值 (X 轴).   |
| `noise_gyro_bias_y` | float   | 0\.0    | 陀螺仪噪声模型均值 (Y 轴).   |
| `noise_gyro_bias_z` | float   | 0\.0    | 陀螺仪噪声模型均值 (Z 轴).   |
| `noise_gyro_stddev_x`           | float   | 0\.0    | 陀螺仪噪声模型标准差 (X 轴). |
| `noise_gyro_stddev_y`           | float   | 0\.0    | 陀螺仪噪声模型标准差 (Y 轴). |
| `noise_gyro_stddev_z`           | float   | 0\.0    | 陀螺仪噪声模型标准差 (Z 轴). |
| `sensor_tick`      | float  | 0\.0   | 传感器数据间的仿真时间 (ticks).  |

---
## LIDAR (激光雷达) 传感器

> type: `sensor.lidar.ray_cast`

| 输出Topic |输出消息类型|
|---|---|
|/carla/{role_name}/{sensor_id} | sensor_msgs/PointCloud2 |

#### Lidar参数

| 参数名称 | 参数类型     | 默认值  | 参数描述          |
| ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- |
|`id`|string|lidar|传感器ID, 用于区分多路传感器  |
|`spawn_point`|object|{"x": 2.0, "y": 0.0, "z": 2.0, "roll": 0.0, "pitch": 0.0, "yaw": 0.0}|传感器安装位置（车身坐标系）
| `channels`           | int    | 32         | 激光雷达线数  |
| `range`              | float  | 10\.0      | 最大探测距离 (单位: 米) |
| `points_per_second`  | int    | 56000      | 每秒扫描的所有点的个数 |
| `rotation_frequency` | float  | 10\.0      | 扫描频率 (单位: 圈/秒) |
| `upper_fov`          | float  | 10\.0      | 扫描俯仰角的最大值 (单位: 度)|
| `lower_fov`          | float  | -30\.0     | 扫描俯仰角的最小值 (单位: 度)|
| `sensor_tick`        | float  | 0\.0       | 传感器数据间的仿真时间 (ticks) |

## 语义LIDAR传感器

> type: `sensor.lidar.ray_cast_semantic`

| 输出Topic |输出消息类型|
|---|---|
|/carla/{role_name}/{sensor_id} | sensor_msgs/PointCloud2 |

#### 语义LIDAR参数

| 参数名称 | 参数类型     | 默认值  | 参数描述 |
| --- | ------------------------------------- | ------------------------------------- | --- |
|`id`|string|lidar|传感器ID, 用于区分多路传感器  |
|`spawn_point`|object|{"x": 2.0, "y": 0.0, "z": 2.0, "roll": 0.0, "pitch": 0.0, "yaw": 0.0}|传感器安装位置（车身坐标系）
| `channels`           | int    | 32         | 激光雷达线数  |
| `range`              | float  | 10\.0      | 最大探测距离 (单位: 米) |
| `points_per_second`  | int    | 56000      | 每秒扫描的所有点的个数 |
| `rotation_frequency` | float  | 10\.0      | 扫描频率 (单位: 圈/秒) |
| `upper_fov`          | float  | 10\.0      | 扫描俯仰角的最大值 (单位: 度)|
| `lower_fov`          | float  | -30\.0     | 扫描俯仰角的最小值 (单位: 度)|
| `sensor_tick`        | float  | 0\.0       | 传感器数据间的仿真时间 (ticks) |


## 毫米波雷达

> type: `sensor.other.radar`

| 输出Topic |输出消息类型|
|---|---|
|/carla/{role_name}/lidar | sensor_msgs/PointCloud2 |

| 参数名称 | 参数类型     | 默认值  | 参数描述          |
| ----------------------------- | ----------------------------- | ----------------------------- | ----------------------------- |
|`id`|string|radar_front|传感器ID, 用于区分多路传感器  |
|`spawn_point`|object|{"x": 2.0, "y": 0.0, "z": 2.0, "roll": 0.0, "pitch": 0.0, "yaw": 0.0}|传感器安装位置（车身坐标系）
| `horizontal_fov`    | float  | 30\.0 | 水平场视角 (单位: 度)   |
| `points_per_second` | int    | 1500  | 每秒扫描的所有点的个数  |
| `range`             | float  | 100   | 最大探测距离 (单位: 米)      |
| `sensor_tick`       | float  | 0\.0  | 传感器数据间的仿真时间 (ticks) |
| `vertical_fov`      | float  | 30\.0 | 垂直场视角 (单位: 度)      |


# 配置文件示例

```json
{
    "type": "vehicle.lincoln2020.mkz2020",
    "id": "ego_vehicle",
    "sensors": 
    [
        {
            "type": "sensor.camera.rgb",
            "id": "rgb_front",
            "spawn_point": {"x": 2.0, "y": 0.0, "z": 2.0, "roll": 0.0, "pitch": 0.0, "yaw": 0.0},
            "image_size_x": 800,
            "image_size_y": 600,
            "fov": 90.0
        },
        {
            "type": "sensor.lidar.ray_cast",
            "id": "lidar",
            "spawn_point": {"x": 0.0, "y": 0.0, "z": 2.4, "roll": 0.0, "pitch": 0.0, "yaw": 0.0},
            "range": 120,
            "channels": 32,
            "points_per_second": 600000,
            "upper_fov": 15.0,
            "lower_fov": -15.0,
            "rotation_frequency": 20,
            "noise_stddev": 0.0
        },
        {
            "type": "sensor.lidar.ray_cast_semantic",
            "id": "semantic_lidar",
            "spawn_point": {"x": 0.0, "y": 0.0, "z": 2.4, "roll": 0.0, "pitch": 0.0, "yaw": 0.0},
            "range": 50,
            "channels": 32,
            "points_per_second": 320000,
            "upper_fov": 2.0,
            "lower_fov": -26.8,
            "rotation_frequency": 20
        },
        {
            "type": "sensor.other.radar",
            "id": "radar_front",
            "spawn_point": {"x": 2.0, "y": 0.0, "z": 2.0, "roll": 0.0, "pitch": 0.0, "yaw": 0.0},
            "horizontal_fov": 30.0,
            "vertical_fov": 10.0,
            "points_per_second": 1500,
            "range": 100.0
        },
        {
            "type": "sensor.camera.semantic_segmentation",
            "id": "semantic_segmentation_front",
            "spawn_point": {"x": 2.0, "y": 0.0, "z": 2.0, "roll": 0.0, "pitch": 0.0, "yaw": 0.0},
            "fov": 90.0,
            "image_size_x": 400,
            "image_size_y": 70
        },
        {
            "type": "sensor.camera.depth",
            "id": "depth_front",
            "spawn_point": {"x": 2.0, "y": 0.0, "z": 2.0, "roll": 0.0, "pitch": 0.0, "yaw": 0.0},
            "fov": 90.0,
            "image_size_x": 400,
            "image_size_y": 70
        },
        {
            "type": "sensor.other.gnss",
            "id": "gnss",
            "spawn_point": {"x": 1.0, "y": 0.0, "z": 2.0},
            "noise_alt_stddev": 0.0, "noise_lat_stddev": 0.0, "noise_lon_stddev": 0.0,
            "noise_alt_bias": 0.0, "noise_lat_bias": 0.0, "noise_lon_bias": 0.0
        },
        {
            "type": "sensor.other.imu",
            "id": "imu",
            "spawn_point": {"x": 2.0, "y": 0.0, "z": 2.0, "roll": 0.0, "pitch": 0.0, "yaw": 0.0},
            "noise_accel_stddev_x": 0.0, "noise_accel_stddev_y": 0.0, "noise_accel_stddev_z": 0.0,
            "noise_gyro_stddev_x": 0.0, "noise_gyro_stddev_y": 0.0, "noise_gyro_stddev_z": 0.0,
            "noise_gyro_bias_x": 0.0, "noise_gyro_bias_y": 0.0, "noise_gyro_bias_z": 0.0
        }
    ]
}
```