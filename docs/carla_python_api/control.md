# 车辆控制

## 设置车型

截至CARLA_0.9.10版为止，CARLA拥有26种车型。

这些车型通过CARLA的蓝图库来获取。

```
vehicle_blueprint_list = world.get_blueprint_library().filter('vehicle.*')
print (vehicle_blueprint_list)

blueprint = random.choice(world.get_blueprint_library().filter('vehicle.*'))
```


## 添加车辆

生成任意一辆车辆都需要一个蓝图(车型)和一个生成点的坐标信息。生成车辆有两种Python API: 

spawn_actor() 和 try_spawn_actor()

```
import carla

transform = Transform(Location(x=230, y=195, z=40), Rotation(yaw=180))
actor = world.spawn_actor(blueprint, transform)
```

## 控制车辆

carla.VehicleControl定义了车辆控制参数，包括油门、刹车、转向角、手刹、反向、档位、是否启用档位七个变量。

### carla.VehicleControl


#### 实例方法:

- **\_\_init\_\_**(self, throttle=0.0, steer=0.0, brake=0.0, hand_brake=False, reverse=False, manual_gear_shift=False, gear=0)
  - 参数: 
    - **throttle** (float):
    
        控制车辆油门的标量值。取值范围[0.0，1.0]，默认值为0.0。

    - **steer** (float):
  
        控制车辆转向角的标量值。取值范围[-1.0，1.0]，默认值为0.0。

    - **brake** (float):

        控制车辆制动的标量值。取值范围[0.0，1.0]，默认值为0.0。

    - **hand_brake** (bool):

        确定是否使用手刹。默认值为False。

    - **reverse** (bool):
  
        确定车辆是否向后移动。默认值为False。

    - **manual_gear_shift** (bool):
  
        确定是否通过手动换档来控制车辆。默认值为False。

    - **gear** (int):
  
        车辆运行的档位。

carla.Vehicle类下的apply_control方法实现了对车辆的控制。


### carla.Vehicle

#### 实例方法:
- apply_control(self, control)
  - 参数:
    - control (carla.VehicleControl):
        在下一个tick上应用的车辆控制对象，包含诸如油门、转向或换档等参数。


## 参考代码

```

import glob
import os
import sys

try:
    #添加CARLA的python egg包路径
    sys.path.append(glob.glob('../carla/dist/carla-*%d.%d-%s.egg' % (
        sys.version_info.major,
        sys.version_info.minor,
        'win-amd64' if os.name == 'nt' else 'linux-x86_64'))[0])
except IndexError:
    pass

import carla

import random
import time


def main():


    try:

        #初始化CARLA
        client = carla.Client('localhost', 2000)
        client.set_timeout(2.0)
        world = client.get_world()
        
        #------------------------------设置车型-------------------------------
        #获取CARLA蓝图库
        blueprint_library = world.get_blueprint_library()
        
        #随机选择一种车型
        vehicle_blueprint = random.choice(blueprint_library.filter ('vehicle'))

        #随机选择一种颜色
        if vehicle_blueprint.has_attribute('color'):
            color = random.choice(bp.get_attribute('color').recommended_values)
            vehicle_blueprint.set_attribute('color', color)

        #------------------------------添加车辆-------------------------------
        #在地图上随机选一个点当作车辆位姿
        transform = random.choice(world.get_map().get_spawn_points())

        #添加车辆
        vehicle = world.spawn_actor(vehicle_blueprint, transform)

        #------------------------------控制车辆-------------------------------
        #自动驾驶脚本控制车辆(可选)
        #vehicle.set_autopilot(True)

        #


```
