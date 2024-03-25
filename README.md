# LIO-SAM ROS2

*****

## Dependencies

*****

Tested with ROS2 versions foxy and galactic on Ubuntu 20.04 and humble on Ubuntu 22.04

ROS2

```
sudo apt install ros-<ros2-version>-perception-pcl \
  	   ros-<ros2-version>-pcl-msgs \
  	   ros-<ros2-version>-vision-opencv \
  	   ros-<ros2-version>-xacro
```

gtsam (Georgia Tech Smoothing and Mapping library)

```
# Add GTSAM-PPA
sudo add-apt-repository ppa:borglab/gtsam-release-4.1
sudo apt install libgtsam-dev libgtsam-unstable-dev
```

## Install

*****

Use the following commands to download and compile the package.

```
cd ~/ros2_ws/src
git clone https://github.com/TixiaoShan/LIO-SAM.git
cd lio-sam
git checkout ros2
cd ..
colcon build
```

```colcon build``` 중 아래와 같은 오류가 발생할 수도 있음.

```
CMake Error at CMakeLists.txt:50 (add_executable):
  Target "lio_sam_imuPreintegration" links to target "Boost::thread" but the
  target was not found.  Perhaps a find_package() call is missing for an
  IMPORTED target, or an ALIAS target is missing?


CMake Error at CMakeLists.txt:50 (add_executable):
  Target "lio_sam_imuPreintegration" links to target "Boost::timer" but the
  target was not found.  Perhaps a find_package() call is missing for an
  IMPORTED target, or an ALIAS target is missing?


CMake Error at CMakeLists.txt:50 (add_executable):
  Target "lio_sam_imuPreintegration" links to target "Boost::chrono" but the
  target was not found.  Perhaps a find_package() call is missing for an
  IMPORTED target, or an ALIAS target is missing?


CMake Error at CMakeLists.txt:54 (add_executable):
  Target "lio_sam_mapOptimization" links to target "Boost::thread" but the
  target was not found.  Perhaps a find_package() call is missing for an
  IMPORTED target, or an ALIAS target is missing?


CMake Error at CMakeLists.txt:54 (add_executable):
  Target "lio_sam_mapOptimization" links to target "Boost::timer" but the
  target was not found.  Perhaps a find_package() call is missing for an
  IMPORTED target, or an ALIAS target is missing?


CMake Error at CMakeLists.txt:54 (add_executable):
  Target "lio_sam_mapOptimization" links to target "Boost::chrono" but the
  target was not found.  Perhaps a find_package() call is missing for an
  IMPORTED target, or an ALIAS target is missing?
```

위와 같은 오류가 발생했으면 CMakeLists.txt 파일에 아래의 내용을 추가

```
find_package(Boost REQUIRED COMPONENTS thread timer chrono)

if(Boost_FOUND)
    include_directories(${Boost_INCLUDE_DIRS})
endif()
```
