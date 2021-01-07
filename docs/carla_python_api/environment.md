# 仿真环境配置

> [!NOTE]
> 本章节只会介绍几个常用的PythonAPI和其常用方法，有关Python API的具体定义和所有方法请参考官网。

在介绍CARLA的Python API之前，需要先了解几个常用Carla PythonAPI的概念。


## 常用Python API概念

### 客户端(carla.Client)

客户端是用户运行的用来获取仿真环境信息或改变仿真行为的模块。

客户端使用IP和特定端口运行。 它通过终端与服务器通信。 可以有多个客户端同时运行。 

### 世界(carla.World)

世界是对整个仿真环境的抽象。

其中包含添加车辆，更改天气，获取仿真信息等主要方法。

每个仿真环境中只有一个世界。

## 创建客户端

创建客户端需要: 
1. CARLA仿真实例的IP地址。默认值为localhost (127.0.0.1)
2. CARLA仿真实例的TCP端口。默认值为2000。

> [!NOTE]
> CARLA仿真实例在Windows下指的是CarlaUE4.exe，在Linux下指的是./CarlaUE4.sh，如果是源码编译就是运行CARLA项目的UE4。
>
>CARLA仿真实例的TCP端口是在运行仿真实例的时候设置，一般仅在端口冲突时使用。
>`
>./CarlaUE4.sh -carla-rpc-port=3000
>`

```
client = carla.Client('localhost', 2000)
```

创建客户端后，请设置其超时时间。设置超时时间避免了因为某个操作时间过长导致客户端一直挂起的情况。

> [!ATTENTION]
> 超时时间默认为5秒，对于部分需要时间较长的操作(如加载新地图)，可能由于超时时间不足导致未知错误。

```
client.set_timeout(10.0) # seconds
```

## 加载地图
可以通过客户端获取当前的仿真世界。
```
world = client.get_world()
```
客户端还可以获取可用地图列表以更改当前地图。

```
print(client.get_available_maps())

world = client.load_world('Town01')
```
如果存在部分车辆在脚本结束后未被销毁等其他错误，也可以重置当前仿真世界。
```
world = client.reload_world()
```

## 设置天气

天气本身并不是一个类，而是通过World类访问的一组参数。 可以设置的参数包括太阳高度角和方位角，云的密度，风，雾等等。 类carla.WeatherParameters用于设置自定义天气。

```
weather = carla.WeatherParameters(
    cloudiness=80.0,
    precipitation=30.0,
    sun_altitude_angle=70.0)

world.set_weather(weather)

print(world.get_weather())
```

CARLA也自定义了一组预设天气。这些列在carla.WeatherParameters中，可以作为枚举访问。也可以在运行manual_control.py脚本时按C键更换预设天气。
```
world.set_weather(carla.WeatherParameters.WetCloudySunset)
```

## 设置光照

### 路灯
当模拟进入夜间模式时，路灯会自动打开。 灯光由地图的开发人员放置，可以作为carla.Light对象访问。 颜色和强度等属性可以随意更改。 

```
# Get the light manager and lights
lmanager = world.get_lightmanager()
mylights = lmanager.get_all_lights()

# Custom a specific light
light01 = mylights[0]
light01.turn_on()
light01.set_intensity(100.0)
state01 = carla.LightState(200.0,red,carla.LightGroup.Building,True)
light01.set_light_state(state01)

# Custom a group of lights
my_lights = lmanager.get_light_group(carla.LightGroup.Building)
lmanager.turn_on(my_lights)
lmanager.set_color(my_lights,carla.Color(255,0,0))
lmanager.set_intensities(my_lights,list_of_intensities)
```

### 车灯

每辆车在carla.VehicleLightState中列出了一组灯光。到目前为止，并非所有车辆都集成了照明灯。这是撰写本文时支持设置车灯的车型列表。

> 自行车: 它们都具有前后位置灯。
> 
> 摩托车: Yamaha和Harley Davidson。
> 
> 汽车:  Audi TT, Chevrolet, Dodge (the police car), Etron, Lincoln, Mustang, Tesla 3S, Wolkswagen T2

可以使用carla.Vehicle.get_light_state和carla.Vehicle.set_light_state方法随时检索和更新车辆的光照。它们使用二进制操作来自定义灯光设置。
```
# Turn on position lights
current_lights = carla.VehicleLightState.NONE
current_lights |= carla.VehicleLightState.Position
vehicle.set_light_state(current_lights)
```
