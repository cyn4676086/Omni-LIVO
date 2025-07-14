# Omni-LIVO

Omni-LIVO is a multi-camera extension of FAST-LIVO2 with enhanced robustness for LiDAR-Inertial-Visual Odometry(FAST-LIVO2-MultiCamera). This project extends the original framework to support multiple cameras for improved tracking performance in challenging environments. To match the wide field of view of modern LiDAR sensors, multiple cameras must be hardware-synchronized with external triggering to ensure precise temporal alignment.

## Status

🚧 **Work in Progress** - More documentation and examples will be added as the project develops.

📝 **Paper Under Review** - Our paper is currently under review. The complete source code will be released upon acceptance.


*Detailed documentation and paper will be available upon publication.*
## Acknowledgments

We sincerely thank the authors of [FAST-LIVO2](https://github.com/hku-mars/FAST-LIVO2) for their outstanding work and for making their code open source. This project would not have been possible without their excellent foundation in LiDAR-Inertial-Visual Odometry. We are grateful for their contribution to the robotics and SLAM community.

Special thanks to:
- The FAST-LIVO2 development team at HKU-MARS
- The entire open-source robotics community for their collaborative spirit

## Overview

This system builds upon FAST-LIVO2 to provide:
- Multi-camera visual odometry support
- Enhanced robustness in challenging scenarios
- Improved tracking performance through multiple viewpoints

## Environment Requirements
- Omni-LIVO environmrnt is as same as FAST-LIVO2

### Ubuntu and ROS
- Ubuntu 18.04~20.04
- [ROS Installation](http://wiki.ros.org/ROS/Installation)

### PCL && Eigen && OpenCV
- PCL>=1.8, Follow [PCL Installation](https://pointclouds.org/downloads/)
- Eigen>=3.3.4, Follow [Eigen Installation](https://eigen.tuxfamily.org/index.php?title=Main_Page)
- OpenCV>=4.2, Follow [OpenCV Installation](https://opencv.org/get-started/)

### Sophus
Sophus Installation for the non-templated/double-only version:

```bash
git clone https://github.com/strasdat/Sophus.git
cd Sophus
git checkout a621ff
mkdir build && cd build && cmake ..
make
sudo make install
```

### Vikit
Vikit contains camera models, some math and interpolation functions that we need. Vikit is a catkin project, therefore, download it into your catkin workspace source folder.

```bash
# Different from the one used in fast-livo1
cd catkin_ws/src
git clone https://github.com/xuankuzcr/rpg_vikit.git 
```

## Build

Clone the repository and catkin_make:

```bash
cd ~/catkin_ws/src
git clone https://github.com/your-repo/omni-livo.git
cd ../
catkin_make
source ~/catkin_ws/devel/setup.bash
```

## Configuration

### Multi-Camera Setup

1. **Camera Parameters**: Configure camera intrinsics in `config/your_dataset_cam.yaml`
2. **Multi-Camera Extrinsics**: Set camera-to-LiDAR transformations in your main config file
3. **Topics**: Update image topics for each camera

Example multi-camera configuration:
```yaml
extrin_calib:
  cameras:
    - cam_id: 0
      img_topic: "/cam0/image_raw"
      Rcl: [rotation_matrix_3x3]
      Pcl: [translation_vector_3x1]
    - cam_id: 1
      img_topic: "/cam1/image_raw"
      Rcl: [rotation_matrix_3x3]
      Pcl: [translation_vector_3x1]
```

## Run

```bash
roslaunch omni_livo your_dataset.launch
```

## Dataset Support

Currently tested with:
- Hilti SLAM Challenge 2022 dataset
- Hilti SLAM Challenge 2023 dataset
- New College dataset
- Custom multi-camera dataset with mid360 and 4 cameras


