# 车辆控制

## 设置车型和车辆生成位姿
在CARLA中，每一个物体(Actor)都有自己的蓝图(blueprint)。蓝图可以理解成物体的类型。

每一个CARLA Server都有其对应的蓝图库，可以通过调用`carla.World`类下的`get_blueprint_library`来获取。`carla.BlueprintLibrary`提供了`filter`方法，可以筛选自己想要的车辆类型。

```
vehicle_blueprint_list = world.get_blueprint_library().filter('vehicle.*')
print (vehicle_blueprint_list)

blueprint = random.choice(world.get_blueprint_library().filter('vehicle.*'))
```


## 添加车辆

生成车辆需要调用调用`carla.World`类下的 `spawn_actor` 或 `try_spawn_actor` 方法。

`spawn_actor` 和 `try_spawn_actor` 的参数相同。但是在失败时 `spawn_actor` 会引发异常， `try_spawn_actor` 返回None。

### carla.World

- **spawn_actor**(self, blueprint, transform, attach_to=None, attachment=Rigid)
  - **blueprint** (carla.ActorBlueprint):
    
    生成Actor的蓝图

  - **transform** (carla.Transform):
    
    生成Actor的xyz坐标和绕三个轴的旋转角度。


  - **attach_to** (carla.Actor):
    
    生成Actor的需要跟随的父物体，比如车载相机Actor需要跟随的父物体是车辆Actor。默认值为空。

  - **attachment** (carla.AttachmentType):
    
    生成Actor跟随父物体的移动方式。默认值为Rigid，子物体和父物体的相对位置保持绝对不变。

- **try_spawn_actor**(self, blueprint, transform, attach_to=None, attachment=Rigid)


  - **blueprint** (carla.ActorBlueprint):
    
    生成Actor的蓝图

  - **transform** (carla.Transform):
    
    生成Actor的xyz坐标和绕三个轴的旋转角度。


  - **attach_to** (carla.Actor):
    
    生成Actor的需要跟随的父物体，比如车载相机Actor需要跟随的父物体是车辆Actor。默认值为空。

  - **attachment** (carla.AttachmentType):
    
    生成Actor跟随父物体的移动方式。默认值为Rigid，子物体和父物体的相对位置保持绝对不变。

## 控制车辆
carla.Vehicle类下的apply_control方法实现了对车辆的控制。需要传递carla.VehicleControl类的参数。

carla.VehicleControl定义了车辆控制参数，包括油门、刹车、转向角、手刹、反向、档位、是否启用档位七个变量。

### carla.Vehicle

- **apply_control**(self, control)
  - **control** (carla.VehicleControl):
    
    在下一个tick上应用的车辆控制对象，包含诸如油门、转向或换档等参数。


### carla.VehicleControl

- **\_\_init\_\_**(self, throttle=0.0, steer=0.0, brake=0.0, hand_brake=False, reverse=False, manual_gear_shift=False, gear=0)
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
        
        #轮胎左转一半，油门最大，倒车
        vc = carla.VehicleControl(throttle=1.0, steer=0.5, brake=0.0, hand_brake=False, reverse=True, manual_gear_shift=False, gear=0)
        
        #应用车辆控制
        vehicle.apply_control(vc)


```
