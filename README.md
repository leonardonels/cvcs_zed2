<div align="center">
    <h1>ZED2 Wiki</h1>
</div>

## :open_file_folder: What's in this repo [XAVIER]
- [**JetPAck 5.1.5**](https://docs.nvidia.com/jetson/archives/jetpack-archived/jetpack-515/release-notes/index.html)
- [**ROS2 FOXY**](https://docs.ros.org/en/foxy/index.html)
- [**ZED SDK 5.0**](https://github.com/leonardonels/cvcs_zed2/edit/main/README.md)
- [**zed-ros2-interfaces 4.0.5**](https://github.com/stereolabs/zed-ros2-interfaces/releases)

- [**zed-ros2 wrapper 4.0.5**](https://github.com/stereolabs/zed-ros2-wrapper/releases)
    - real_world → Camera sdk + ros_wrapper→ sensor_msgs/Image

## :gear: How to build & Run
```commandline
jetson_clocks --fan
```
```commandline
sudo date --set "16 MAY 2025 10:25:30"
```
```commandline
sudo apt install ros-foxy-robot-localization ros-foxy-nmea-mesgs ros-foxy-xacro
```

## :hammer_and_wrench: Docker [WIP]
```commandline
docker run -it  --gpus all --runtime nvidia --privileged -e DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v /dev:/dev -e NVIDIA_DRIVER_CAPABILITIES=all zed_ros2_desktop_u22.04_sdk_4.2.3_cuda_12.6.3_rviz2
```
```commandline
ros2 launch zed_display_rviz2 display_zed_cam.launch.py camera_model:=zed2
```


## :abacus: Parameters



🏎️ Made by [**Leonardo Nels**](https://github.com/leonardonels) - 2025
