# CVCS ZED2 — Computer Vision & Cognitive Systems Project
Repository for the Computer Vision and Cognitive Systems (CVCS) course. This
workspace implements an end-to-end stereo-camera pipeline to detect, localize,
map and plan around colored street cones — tuned for SAE Formula Student-style
courses where left/right cones are color-coded.

Overview
--------
- Sense: ZED2 stereo camera (primary) or a webcam (debug) provides images and
	depth.
- Perception: YOLO-based detector (in `yolo/`) finds cones and outputs
	bounding boxes and color labels.
- Localisation: `localisation/` maps 2D bounding boxes to 3D points using the
	ZED depth map and publishes marker messages.
- Mapping: `mapping/` fuses detections over time using a Kalman filter to
	produce a stable global cone map.
- Planning: `planning/` computes a centerline/path between cones for
	downstream vehicle guidance.

This workspace is intended for ROS 2 (target: Humble on Ubuntu 22.04) and
requires an NVIDIA GPU for real-time YOLO inference and for the ZED driver.

Packages (non-ZED)
-------------------
- `debug/` — lightweight webcam publisher for YOLO debugging.
- `yolo/` — cone detection node (YOLO models live under `yolo/models/`).
- `localisation/` — converts 2D bboxes + depth -> 3D Marker/point arrays.
- `mapping/` — Kalman-filter-based global cone mapping and data association.
- `planning/` — computes a centerline/trajectory between cones using color
	classification.

ZED packages (`zed2/`, `zed_wrapper/`, `zed_ros`, etc.) are included in the
workspace but are third-party and not authored here — they provide the camera
driver and ROS interface.

Quick start (build & run)
-------------------------
Prerequisites (high-level):
- Ubuntu 22.04
- ROS 2 Humble (source `/opt/ros/humble/setup.bash`)
- NVIDIA GPU with CUDA-supporting drivers
- ZED SDK (if using ZED2 hardware)
- Python deps for `yolo/` (see `yolo/requirements.txt`)

Build the workspace:

```bash
source /opt/ros/humble/setup.bash
colcon build --symlink-install
source install/setup.bash
```

Run with ZED2 (example sequence — inspect package `launch/` folders for exact
file names and parameters):

```bash
# start ZED driver/wrapper
ros2 launch zed_wrapper zed2.launch.py
# start YOLO detector
ros2 launch yolo yolo_launch.py
# localisation
ros2 launch localisation launch.py
# mapping
ros2 launch mapping launch.py
# planning
ros2 launch planning launch.py
```

Run with webcam for YOLO debugging (no ZED):

```bash
ros2 launch debug webcam_launch.py
ros2 launch yolo yolo_launch.py
```

Notes & caveats
---------------
- Webcam mode provides no depth — localisation and mapping that rely on
	stereo depth will not function unless a mocked depth source is provided.
- Ensure ZED SDK and ROS wrappers match your ROS/CUDA versions.
- GPU is recommended — non-GPU inference may be too slow for real-time.

Per-package README files have been added for `debug`, `yolo`,
`localisation`, `mapping`, and `planning` with concise run instructions and
key files. Inspect those for package-specific topics and parameters.

Next steps
----------
- Add unit/integration tests for projection math and mapping data association.
- Add RViz saved configurations for quick visualization of detections,
	markers and planned path.
- Document exact ZED SDK and CUDA versions used in the environment.

---

🏎️ Made by [**Leonardo Nels**](https://github.com/leonardonels) - 2025
