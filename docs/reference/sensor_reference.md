# 传感器参数参考文档

---
*   [__RGB camera__](#rgb-camera)
*   [__Depth camera(深度相机)__](#depth-camera)
*   [__Semantic segmentation camera(语义相机)__](#semantic-segmentation-camera)
*   [__GNSS sensor(GNSS传感器)__](#gnss-sensor)
*   [__IMU sensor(惯性传感器)__](#imu-sensor)
*   [__LIDAR sensor(激光雷达)__](#lidar-sensor)
*   [__Semantic LIDAR sensor(语义激光雷达)__](#semantic-lidar-sensor)
*   [__Radar sensor(毫米波雷达)__](#radar-sensor)

---
## RGB camera
  
| 输出Topic |输出消息类型|
|---|---|
|/carla/{role_name}/{sensor_id}/image | sensor_msgs/Image |
|/carla/{role_name}/{sensor_id}/camera_info | sensor_msgs/CameraInfo |

RGB相机的作用是作为普通摄像机捕捉场景中的RGB图像。

`sensor_tick` 定义传感器采集数据的快慢。
例如： `sensor_tick = 1.5`， 意味着传感器每1.5s采集一次。默认为0，即尽可能快的采集。

#### 相机基本参数

| 参数名称 | 参数类型     | 默认值  | 参数描述          |
| ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- |
|`id`|string|rgb_camera|传感器ID, 用于区分多路传感器  |
| `fov`    | float    | 90\.0    | 水平视场角 (单位: 度) |
| `image_size_x`       | int      | 800      | 图像宽度 (像素) |
| `image_size_y`       | int      | 600      | 图像高度 (像素) |
| `sensor_tick`        | float    | 0\.0     | 传感器数据间的仿真时间 (ticks).  |
| `shutter_speed`      | float    | 200\.0   | 相机快门速度 (1.0/s).       |


## 深度相机

| 输出Topic |输出消息类型|
|---|---|
|/carla/{role_name}/{sensor_id}/image | sensor_msgs/Image |
|/carla/{role_name}/{sensor_id}/camera_info | sensor_msgs/CameraInfo |

深度相机可以将场景中的距离信息编码为像素生成深度图像。

在ROS-Bridge中，深度图已经被转换为单通道float32的图像，每个像素值即为实际距离(米)。

#### 相机基本参数

| 参数名称 | 参数类型     | 默认值  | 参数描述          |
| ----------------------------- | ----------------------------- | ----------------------------- | ----------------------------- |
|`id`|string|rgb_camera|传感器ID, 用于区分多路传感器  |
| `fov`    | float    | 90\.0    | 水平视场角 (单位: 度) |
| `image_size_x`       | int      | 800      | 图像宽度 (像素) |
| `image_size_y`       | int      | 600      | 图像高度 (像素) |
| `sensor_tick`        | float    | 0\.0     | 传感器数据间的仿真时间 (ticks).  |

---
## GNSS sensor

| 输出Topic |输出消息类型|
|---|---|
|/carla/{role_name}/gnss | sensor_msgs/NavSatFix |

反馈父对象当前的 gnss 位置。这是通过在OpenDRIVE地图的定义，结合仿真器参考位置来计算的。

#### GNSS参数


| 参数名称 | 参数类型     | 默认值  | 参数描述          |
| ------------------- | ------------------- | ------------------- | ------------------- |
| `noise_alt_bias`   | float  | 0\.0   | 海拔高度的噪声模型中的均值    |
| `noise_alt_stddev` | float  | 0\.0   | 海拔高度的噪声模型中的标准差 |
| `noise_lat_bias`   | float  | 0\.0   | 纬度噪声模型的均值 |
| `noise_lat_stddev` | float  | 0\.0   | 纬度噪声模型的标准差  |
| `noise_lon_bias`   | float  | 0\.0   | 经度噪声模型的均值   |
| `noise_lon_stddev` | float  | 0\.0   | 经度噪声模型的标准差 |
| `sensor_tick`      | float  | 0\.0   | 传感器数据间的仿真时间 (ticks).  |

---
## IMU sensor

| 输出Topic |输出消息类型|
|---|---|
|/carla/{role_name}/imu| sensor_msgs/Imu |

提供父对象的加速度计、陀螺仪、磁力计的传感器测量值。 数据由对象当前状态采集获得。

#### IMU参数


| 参数名称 | 参数类型     | 默认值  | 参数描述          |
| -------------------------------- | -------------------------------- | -------------------------------- | -------------------------------- |
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
## LIDAR sensor

* __Blueprint:__ sensor.lidar.ray_cast
* __Output:__ [carla.LidarMeasurement](python_api.md#carla.LidarMeasurement) per step (unless `sensor_tick` says otherwise).

This sensor simulates a rotating LIDAR implemented using ray-casting.
The points are computed by adding a laser for each channel distributed in the vertical FOV. The rotation is simulated computing the horizontal angle that the Lidar rotated in a frame. The point cloud is calculated by doing a ray-cast for each laser in every step.
`points_per_channel_each_step = points_per_second / (FPS * channels)`

A LIDAR measurement contains a package with all the points generated during a `1/FPS` interval. During this interval the physics are not updated so all the points in a measurement reflect the same "static picture" of the scene.

This output contains a cloud of simulation points and thus, it can be iterated to retrieve a list of their [`carla.Location`](python_api.md#carla.Location):

```py
for location in lidar_measurement:
    print(location)
```

The information of the LIDAR measurement is enconded 4D points. Being the first three, the space points in xyz coordinates and the last one intensity loss during the travel. This intensity is computed by the following formula.
<br>
![LidarIntensityComputation](img/lidar_intensity.jpg)

`a` — Attenuation coefficient. This may depend on the sensor's wavelenght, and the conditions of the atmosphere. It can be modified with the LIDAR attribute `atmosphere_attenuation_rate`.
`d` — Distance from the hit point to the sensor.

For a better realism, points in the cloud can be dropped off. This is an easy way to simulate loss due to external perturbations. This can done combining two different.

*   __General drop-off__ — Proportion of points that are dropped off randomly. This is done before the tracing, meaning the points being dropped are not calculated, and therefore improves the performance. If `dropoff_general_rate = 0.5`, half of the points will be dropped.
*   __Instensity-based drop-off__ — For each point detected, and extra drop-off is performed with a probability based in the computed intensity. This probability is determined by two parameters. `dropoff_zero_intensity` is the probability of points with zero intensity to be dropped. `dropoff_intensity_limit` is a threshold intensity above which no points will be dropped. The probability of a point within the range to be dropped is a linear proportion based on these two parameters.

Additionally, the `noise_stddev` attribute makes for a noise model to simulate unexpected deviations that appear in real-life sensors. For positive values, each point is randomly perturbed along the vector of the laser ray. The result is a LIDAR sensor with perfect angular positioning, but noisy distance measurement.

The rotation of the LIDAR can be tuned to cover a specific angle on every simulation step (using a [fixed time-step](adv_synchrony_timestep.md)). For example, to rotate once per step (full circle output, as in the picture below), the rotation frequency and the simulated FPS should be equal. <br> __1.__ Set the sensor's frequency `sensors_bp['lidar'][0].set_attribute('rotation_frequency','10')`. <br> __2.__ Run the simulation using `python3 config.py --fps=10`.

![LidarPointCloud](img/lidar_point_cloud.jpg)

#### Lidar attributes


| Blueprint attribute  | Type   | Default    | Description     |
| ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- |
| `channels`         | int    | 32     | Number of lasers.  |
| `range`            | float  | 10.0  | Maximum distance to measure/raycast in meters (centimeters for CARLA 0.9.6 or previous).  |
| `points_per_second` | int    | 56000  | Points generated by all lasers per second.    |
| `rotation_frequency`            | float  | 10.0  | LIDAR rotation frequency.       |
| `upper_fov`        | float  | 10.0  | Angle in degrees of the highest laser.        |
| `lower_fov`        | float  | -30.0 | Angle in degrees of the lowest laser.         |
| `atmosphere_attenuation_rate`     | float  | 0.004 | Coefficient that measures the LIDAR instensity loss per meter. Check the intensity computation above. |
| `dropoff_general_rate`          | float  | 0.45  | General proportion of points that are randomy dropped.    |
| `dropoff_intensity_limit`       | float  | 0.8   | For the intensity based drop-off, the threshold intensity value above which no points are dropped.    |
| `dropoff_zero_intensity`        | float  | 0.4   | For the intensity based drop-off, the probability of each point with zero intensity being dropped.    |
| `sensor_tick`      | float  | 0.0   | Simulation seconds between sensor captures (ticks). |
| `noise_stddev`     | float  | 0.0   | Standard deviation of the noise model to disturb each point along the vector of its raycast. |




#### Output attributes

| Sensor data attribute            | Type  | Description        |
| ----------------------- | ----------------------- | ----------------------- |
| `frame`            | int   | Frame number when the measurement took place.      |
| `timestamp`        | double | Simulation time of the measurement in seconds since the beginning of the episode.        |
| `transform`        | [carla.Transform](<../python_api#carlatransform>)  | Location and rotation in world coordinates of the sensor at the time of the measurement. |
| `horizontal_angle`   | float | Angle (radians) in the XY plane of the LIDAR in the current frame.           |
| `channels`         | int   | Number of channels (lasers) of the LIDAR.    |
| `get_point_count(channel)`       | int   | Number of points per channel captured this frame.  |
| `raw_data`         | bytes | Array of 32-bits floats (XYZI of each point).      |


<br>

## Radar sensor

* __Blueprint:__ sensor.other.radar
* __Output:__ [carla.RadarMeasurement](python_api.md#carla.RadarMeasurement) per step (unless `sensor_tick` says otherwise).

The sensor creates a conic view that is translated to a 2D point map of the elements in sight and their speed regarding the sensor. This can be used to shape elements and evaluate their movement and direction. Due to the use of polar coordinates, the points will concentrate around the center of the view.

Points measured are contained in [carla.RadarMeasurement](python_api.md#carla.RadarMeasurement) as an array of [carla.RadarDetection](python_api.md#carla.RadarDetection), which specifies their polar coordinates, distance and velocity.
This raw data provided by the radar sensor can be easily converted to a format manageable by __numpy__:
```py
# To get a numpy [[vel, altitude, azimuth, depth],...[,,,]]:
points = np.frombuffer(radar_data.raw_data, dtype=np.dtype('f4'))
points = np.reshape(points, (len(radar_data), 4))
```

The provided script `manual_control.py` uses this sensor to show the points being detected and paint them white when static, red when moving towards the object and blue when moving away:

![ImageRadar](img/ref_sensors_radar.jpg)

| Blueprint attribute       | Type    | Default | Description   |
| ----------------------------- | ----------------------------- | ----------------------------- | ----------------------------- |
| `horizontal_fov`          | float   | 30\.0   | Horizontal field of view in degrees.    |
| `points_per_second`       | int     | 1500    | Points generated by all lasers per second.          |
| `range` | float   | 100     | Maximum distance to measure/raycast in meters.      |
| `sensor_tick` | float   | 0\.0    | Simulation seconds between sensor captures (ticks). |
| `vertical_fov`            | float   | 30\.0   | Vertical field of view in degrees.      |

<br>

#### Output attributes

| Sensor data attribute | Type            | Description     |
| ---------------- | ---------------- | ---------------- |
| `raw_data`      | [carla.RadarDetection](<../python_api#carlaradardetection>) | The list of points detected.      |

<br>

| RadarDetection attributes    | Type             | Description      |
| ---------------------------- | ---------------------------- | ---------------------------- |
| `altitude`       | float            | Altitude angle in radians.   |
| `azimuth`        | float            | Azimuth angle in radians.    |
| `depth`          | float            | Distance in meters.          |
| `velocity`       | float            | Velocity towards the sensor. |




#### Camera lens distortion attributes


<br>

| Blueprint attribute      | Type         | Default      | Description  |
| ------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------- |
| `lens_circle_falloff`    | float        | 5\.0         | Range: [0.0, 10.0]       |
| `lens_circle_multiplier` | float        | 0\.0         | Range: [0.0, 10.0]       |
| `lens_k`     | float        | \-1.0        | Range: [-inf, inf]       |
| `lens_kcube` | float        | 0\.0         | Range: [-inf, inf]       |
| `lens_x_size`            | float        | 0\.08        | Range: [0.0, 1.0]        |
| `lens_y_size`            | float        | 0\.08        | Range: [0.0, 1.0]        |


---
## Semantic LIDAR sensor

* __Blueprint:__ sensor.lidar.ray_cast_semantic
* __Output:__ [carla.SemanticLidarMeasurement](python_api.md#carla.SemanticLidarMeasurement) per step (unless `sensor_tick` says otherwise).

This sensor simulates a rotating LIDAR implemented using ray-casting that exposes all the information about the raycast hit. Its behaviour is quite similar to the [LIDAR sensor](#lidar-sensor), but there are two main differences between them.

*   The raw data retrieved by the semantic LIDAR includes more data per point.
	*   Coordinates of the point (as the normal LIDAR does).
	*   The cosine between the angle of incidence and the normal of the surface hit.
	*   Instance and semantic ground-truth. Basically the index of the CARLA object hit, and its semantic tag.
*   The semantic LIDAR does not include neither intensity, drop-off nor noise model attributes.

The points are computed by adding a laser for each channel distributed in the vertical FOV. The rotation is simulated computing the horizontal angle that the LIDAR rotated in a frame. The point cloud is calculated by doing a ray-cast for each laser in every step.
```sh
points_per_channel_each_step = points_per_second / (FPS * channels)
```

A LIDAR measurement contains a package with all the points generated during a `1/FPS` interval. During this interval the physics are not updated so all the points in a measurement reflect the same "static picture" of the scene.

This output contains a cloud of lidar semantic detections and therefore, it can be iterated to retrieve a list of their [`carla.SemanticLidarDetection`](python_api.md#carla.SemanticLidarDetection):

```py
for detection in semantic_lidar_measurement:
    print(detection)
```

The rotation of the LIDAR can be tuned to cover a specific angle on every simulation step (using a [fixed time-step](adv_synchrony_timestep.md)). For example, to rotate once per step (full circle output, as in the picture below), the rotation frequency and the simulated FPS should be equal. <br>
__1.__ Set the sensor's frequency `sensors_bp['lidar'][0].set_attribute('rotation_frequency','10')`. <br>
__2.__ Run the simulation using `python3 config.py --fps=10`.

![LidarPointCloud](img/semantic_lidar_point_cloud.jpg)

#### SemanticLidar attributes


<br>

| Blueprint attribute  | Type           | Description    |
| ------------------------------------- | ------------------------------------- | ------------------------------------- |
| `channels`         | int   | 32    | Number of lasers.  |
| `range`            | float | 10.0 | Maximum distance to measure/raycast in meters (centimeters for CARLA 0.9.6 or previous). |
| `points_per_second`    | int   | 56000 | Points generated by all lasers per second.   |
| `rotation_frequency`   | float | 10.0 | LIDAR rotation frequency.       |
| `upper_fov`        | float | 10.0 | Angle in degrees of the highest laser.    |
| `lower_fov`        | float | -30.0 | Angle in degrees of the lowest laser.     |
| `sensor_tick`      | float | 0.0  | Simulation seconds between sensor captures (ticks).   |



<br>


#### Output attributes


| Sensor data attribute  | Type           | Description    |
| ------------------------------------- | ------------------------------------- | ------------------------------------- |
| `frame`        | int            | Frame number when the measurement took place.  |
| `timestamp`    | double         | Simulation time of the measurement in seconds since the beginning of the episode.   |
| `transform`    | [carla.Transform](<../python_api#carlatransform>)     | Location and rotation in world coordinates of the sensor at the time of the measurement. |
| `horizontal_angle`         | float          | Angle (radians) in the XY plane of the LIDAR in the current frame.     |
| `channels`     | int            | Number of channels (lasers) of the LIDAR.      |
| `get_point_count(channel)` | int            | Number of points per channel captured in the current frame.            |
| `raw_data`     | bytes          | Array containing the point cloud with instance and semantic information. For each point, four 32-bits floats are stored. <br>  XYZ coordinates. <br> cosine of the incident angle. <br> Unsigned int containing the index of the object hit. <br>  Unsigned int containing the semantic tag of the object it. |



## Semantic segmentation camera

*   __Blueprint:__ sensor.camera.semantic_segmentation
*   __Output:__ [carla.Image](python_api.md#carla.Image) per step (unless `sensor_tick` says otherwise).

This camera classifies every object in sight by displaying it in a different color according to its tags (e.g., pedestrians in a different color than vehicles).
When the simulation starts, every element in scene is created with a tag. So it happens when an actor is spawned. The objects are classified by their relative file path in the project. For example, meshes stored in `Unreal/CarlaUE4/Content/Static/Pedestrians` are tagged as `Pedestrian`.

![ImageSemanticSegmentation](img/ref_sensors_semantic.jpg)

The server provides an image with the tag information __encoded in the red channel__: A pixel with a red value of `x` belongs to an object with tag `x`.
This raw [carla.Image](python_api.md#carla.Image) can be stored and converted it with the help of __CityScapesPalette__  in [carla.ColorConverter](python_api.md#carla.ColorConverter) to apply the tags information and show picture with the semantic segmentation.

```py
...
raw_image.save_to_disk("path/to/save/converted/image",carla.cityScapesPalette)
```

The following tags are currently available:

| Value          | Tag            | Converted color  | Description      |
| ----------------------------------- | ----------------------------------- | ----------------------------------- | ----------------------------------- |
| `0`            | Unlabeled      | `(0, 0, 0)`      | Elements that have not been categorized are considered `Unlabeled`. This category is meant to be empty or at least contain elements with no collisions.     |
| `1`            | Building       | `(70, 70, 70)`   | Buildings like houses, skyscrapers,... and the elements attached to them. <br> E.g. air conditioners, scaffolding, awning or ladders and much more.       |
| `2`            | Fence          | `(100, 40, 40)`  | Barriers, railing, or other upright structures. Basically wood or wire assemblies that enclose an area of ground.           |
| `3`            | Other          | `(55, 90, 80)`   | Everything that does not belong to any other category.       |
| `4`            | Pedestrian       | `(220, 20, 60)`  | Humans that walk or ride/drive any kind of vehicle or mobility system. <br> E.g. bicycles or scooters, skateboards, horses, roller-blades, wheel-chairs, etc.         |
| `5`            | Pole           | `(153, 153, 153)`            | Small mainly vertically oriented pole. If the pole has a horizontal part (often for traffic light poles) this is also considered pole. <br> E.g. sign pole, traffic light poles.     |
| `6`            | RoadLine       | `(157, 234, 50)`             | The markings on the road.    |
| `7`            | Road           | `(128, 64, 128)`             | Part of ground on which cars usually drive. <br> E.g. lanes in any directions, and streets.       |
| `8`            | SideWalk       | `(244, 35, 232)`             | Part of ground designated for pedestrians or cyclists. Delimited from the road by some obstacle (such as curbs or poles), not only by markings. This label includes a possibly delimiting curb, traffic islands (the walkable part), and pedestrian zones. |
| `9`            | Vegetation       | `(107, 142, 35)`             | Trees, hedges, all kinds of vertical vegetation. Ground-level vegetation is considered `Terrain`.   |
| `10`           | Vehicles       | `(0, 0, 142)`    | Cars, vans, trucks, motorcycles, bikes, buses, trains.       |
| `11`           | Wall           | `(102, 102, 156)`            | Individual standing walls. Not part of a building.         |
| `12`           | TrafficSign      | `(220, 220, 0)`  | Signs installed by the state/city authority, usually for traffic regulation. This category does not include the poles where signs are attached to. <br> E.g. traffic- signs, parking signs, direction signs...     |
| `13`           | Sky            | `(70, 130, 180)`             | Open sky. Includes clouds and the sun.   |
| `14`           | Ground         | `(81, 0, 81)`    | Any horizontal ground-level structures that does not match any other category. For example areas shared by vehicles and pedestrians, or flat roundabouts delimited from the road by a curb.        |
| `15`           | Bridge         | `(150, 100, 100)`            | Only the structure of the bridge. Fences, people, vehicles, an other elements on top of it are labeled separately.          |
| `16`           | RailTrack      | `(230, 150, 140)`            | All kind of rail tracks that are non-drivable by cars. <br> E.g. subway and train rail tracks.    |
| `17`           | GuardRail      | `(180, 165, 180)`            | All types of guard rails/crash barriers. |
| `18`           | TrafficLight     | `(250, 170, 30)`             | Traffic light boxes without their poles. |
| `19`           | Static         | `(110, 190, 160)`            | Elements in the scene and props that are immovable. <br> E.g. fire hydrants, fixed benches, fountains, bus stops, etc.    |
| `20`           | Dynamic        | `(170, 120, 50)`             | Elements whose position is susceptible to change over time. <br> E.g. Movable trash bins, buggies, bags, wheelchairs, animals, etc.         |
| `21`           | Water          | `(45, 60, 150)`  | Horizontal water surfaces. <br> E.g. Lakes, sea, rivers.   |
| `22`           | Terrain        | `(145, 170, 100)`            | Grass, ground-level vegetation, soil or sand. These areas are not meant to be driven on. This label includes a possibly delimiting curb.      |

<br>

!!! Note
    Read [this](tuto_D_create_semantic_tags.md) tutorial to create new semantic tags. 

#### Basic camera attributes

| Blueprint attribute       | Type    | Default | Description   |
| ----------------------------- | ----------------------------- | ----------------------------- | ----------------------------- |
| `fov`   | float   | 90\.0   | Horizontal field of view in degrees.    |
| `image_size_x`            | int     | 800     | Image width in pixels.      |
| `image_size_y`            | int     | 600     | Image height in pixels.     |
| `sensor_tick` | float   | 0\.0    | Simulation seconds between sensor captures (ticks). |



---

#### Camera lens distortion attributes

| Blueprint attribute      | Type         | Default      | Description  |
| ---------------------------- | ---------------------------- | ---------------------------- | ---------------------------- |
| `lens_circle_falloff`    | float        | 5\.0         | Range: [0.0, 10.0]       |
| `lens_circle_multiplier` | float        | 0\.0         | Range: [0.0, 10.0]       |
| `lens_k`     | float        | \-1.0        | Range: [-inf, inf]       |
| `lens_kcube` | float        | 0\.0         | Range: [-inf, inf]       |
| `lens_x_size`            | float        | 0\.08        | Range: [0.0, 1.0]        |
| `lens_y_size`            | float        | 0\.08        | Range: [0.0, 1.0]        |
