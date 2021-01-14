# 车辆控制

CARLA所用的车辆动力学模型为UE4提供的车辆动力学模型。

车辆控制都是通过提供油门，方向角和刹车等参数，再由UE4转化为车辆的加减速等行为。

## 设置车型

截至CARLA_0.9.10版为止，CARLA拥有26种车型，这些车型通过CARLA的蓝图库来获取。
```
vehicle_blueprint_list = world.get_blueprint_library().filter('vehicle.*')
print (vehicle_blueprint_list)

blueprint = random.choice(world.get_blueprint_library().filter('vehicle.*'))
```
也可以调用PythonAPI\examples下的脚本查看车型。

`python vehicle_gallery.py`

## 添加车辆

生成任意一辆车辆都需要一个蓝图(车型)和一个生成点的坐标信息。生成车辆有两种Python API: 

spawn_actor() 和 try_spawn_actor()

```
import carla

transform = Transform(Location(x=230, y=195, z=40), Rotation(yaw=180))
actor = world.spawn_actor(blueprint, transform)
```

## 控制车辆

控制车辆需要调用vehicle对象的apply_control()

包含七个参数
