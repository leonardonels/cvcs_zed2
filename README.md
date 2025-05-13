<div align="center">
    <h1>ZED2 Wiki</h1>
</div>

## :open_file_folder: What's in this repo
- **`stereolabs/zed`**: ZED2_SDK only container
- **`zed_ros2_desktop_u22.04_sdk_4.2.3_cuda_12.6.3`**: Custom ZED2 + Ros2 Humble container
- **`zed_ros2_desktop_u22.04_sdk_4.2.3_cuda_12.6.3_rviz2`**: Custom ZED2 + Ros2 Humble + rviz2 container
    - real_world → Camera sdk + ros_wrapper→ sensor_msgs/Image

## :gear: How to build & Run
```commandline
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/arm64/cuda-keyring_1.1-1_all.deb
sudo dpkg -i cuda-keyring_1.1-1_all.deb
sudo apt-get update
sudo apt-get -y install cuda
```
```commandline
docker run -it  --gpus all --runtime nvidia --privileged -e DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v /dev:/dev -e NVIDIA_DRIVER_CAPABILITIES=all zed_ros2_desktop_u22.04_sdk_4.2.3_cuda_12.6.3_rviz2
```
```commandline
ros2 launch zed_display_rviz2 display_zed_cam.launch.py camera_model:=zed2
```


## :abacus: Parameters



🏎️ Made by [**Leonardo Nels**](https://github.com/leonardonels) - 2025
