<div align="center">
    <h1>ZED2 Wiki</h1>
</div>

## :open_file_folder: Docs [HP-4060]
- [**ROS2 HUMBLE**](https://docs.ros.org/en/humble/Installation.html)
- [**ZED SDK 4.2.5**](https://www.stereolabs.com/en-it/developers/release/4.2)
- [**ZED WRAPPER FOR ROS2**](https://github.com/stereolabs/zed-ros2-wrapper)
    - real_world → Camera sdk + ros_wrapper → sensor_msgs/Image
- [**WEBCAM ROS2 NODE**](https://github.com/leonardonels/webcam_ros2_node.git)
    - real_world → webcam ros2 node → sensor_msgs/Image
- [**YOLO ROS2 HUMBLE**](https://github.com/mgonzs13/yolo_ros/tree/main?tab=readme-ov-file)
    - sensor_msgs/Image → yolo_ros → ??
  

## :gear: How to build & Run
> first download and install the SDK
```commandline
cd ~/Downloads
sudo apt install zstd
chmod +x ZED_SDK_Ubuntu22_cuda12.1_v4.2.5.zstd.run
./ZED_SDK_Ubuntu22_cuda12.1_v4.2.5.zstd.run
```
> next install the ros2 wrapper from stereolabs, **make sure to install it from a release version, not from the main branch!!**
```commandline
cd ~/ros2_ws/src
sudo apt install ros-humble-zed-msgs
git clone https://github.com/stereolabs/zed-ros2-wrapper.git
cd zed-ros2-wrapper
git checkout -b origin/master humble-v4.2.5
cd ~/ros2_ws
colcon build --symlink-install --cmake-args=-DCMAKE_BUILD_TYPE=Release --parallel-workers $(nproc)
```
> to run the wrapper
```commandline
cd ~/ros2_ws
source install/setup.bash
ros2 launch zed_wrapper zed_camera.launch.py  camera_model:=zed2
```
> to use the webcam instead, but first prepare the virtual environment
```commandline
cd ~/ros2_ws
python3 -m venv .venv
source .venv/bin/activate
```
> and then the camera node
```commandline
cd ~/ros2_ws/src
git clone https://github.com/leonardonels/webcam_ros2_node.git
cd ~/ros2_ws
colcon build --symlink-install --cmake-args=-DCMAKE_BUILD_TYPE=Release --parallel-workers $(nproc)
ros2 launch webcam_publisher webcam_launch.py
```
> install the yolo ros node, but first prepare the virtual environment
```commandline
cd ~/ros2_ws
python3 -m venv .venv
source .venv/bin/activate
```
> next build the yolo node
```commandline
cd ~/ros2_ws/src
git clone https://github.com/mgonzs13/yolo_ros.git
pip3 install -r yolo_ros/requirements.txt
cd ~/ros2_ws
rosdep install --from-paths src --ignore-src -r -y
colcon build --symlink-install --cmake-args=-DCMAKE_BUILD_TYPE=Release --parallel-workers $(nproc)
```
> at last start the node
```commandline
cd ~/ros2_ws
source .venv/bin/activate
export PYTHONPATH=$PYTHONPATH:~/ros2_ws/.venv/lib/python3.10/site-packages
ros2 launch yolo_bringup yolo.launch.py model:=best.pt input_image_topic:=camera/image_raw
```

> extras...
```commandline
docker run -it  --gpus all --runtime nvidia --privileged --network host -e DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v /dev:/dev -e NVIDIA_DRIVER_CAPABILITIES=all <docker image id>
```
```commandline
ros2 launch zed_display_rviz2 display_zed_cam.launch.py camera_model:=zed2
```
```commandline
ros2 launch zed_display_rviz2 display_zed_cam.launch.py camera_model:=<camera_model>
```
```commandline
ros2 launch yolo_bringup yolov8.launch.py input_image_topic:=/zed/zed_node/left/image_rect_color model:=best.pt
```

## :abacus: Parameters [WIP]



## :open_file_folder: Docs [XAVIER]
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


## :abacus: Parameters [WIP]



🏎️ Made by [**Leonardo Nels**](https://github.com/leonardonels) - 2025
