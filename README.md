# Setup
## Install dependencies

Install python dependencies with pip:
```bash
pip3 install -r requirements.txt
```

One of the dependencies is a modified version of the ```siyi_sdk```, which can be accessed in this repository:
```https://github.com/aimas-lund/siyi_sdk_ros2_submodule```. This repo is modified to handle zoom functionalities of the ZR30 camera specifically.


## Build ROS2 package

Build with colcon:
```bash
colcon build
```

Source the setup file:
```bash
. install/setup.bash
```

# Run
Run the camera controller and camera stream ROS2 nodes with the launch file:
```bash
ros2 launch zr30camera zr30camera_launch.py
```

# Control the camera actuators
The ZR30 camera can be controlled via the topics starting with ```/ZR30/set_```. This can either be done with a custom node that publishes, or built-in ```ros2``` functionalities.

For instance, setting the camera zoom level to 20x can be done with the following command:

```bash
ros2 topic pub --once /ZR30/set_zoom_level std_msgs/msg/Float32 'data: 20'
```

NOTE: the ```--once``` argument is important, as the camera zoom will otherwise camera controller node will hang.

## Camera control topics

### Zoom control

- ```/ZR30/set_zoom_level```, accepts ```std_msgs/msg/Float32``` type messages.

### Gimbal control

- ```/ZR30/set_gimbal_attitude```, accepts ```geometry_msgs/msg/Vector3Stamped```-type messages, where x = roll, y = pitch and z = yaw.


# Camera stream
The video stream from the UDP endpoint is parsed to the ```/ZR30/camera_stream``` topic in the ```sensor_msgs/msg/Image``` format.