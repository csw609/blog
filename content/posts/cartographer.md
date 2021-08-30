---
title: "Cartographer 설치 방법 On ROS"
date: 2021-08-30T16:17:11+09:00
---
# Cartographer 설치 방법 on ROS

- 참고 자료

    [https://google-cartographer-ros.readthedocs.io/en/latest/ros_api.html](https://google-cartographer-ros.readthedocs.io/en/latest/ros_api.html)

# **Building & Installation**

Cartographer ROS를 빌드하기 위해서는 wstool과 rosdep을 권장하고 빠른 빌드를 위해 Ninja 또한 추천한다고 한다.

별도의 빌드툴을 사용하므로 catkin workspace 이외의 다른 workspace를 별도로 사용하는 것이 좋을듯하다.

둘 중에 버전을 맞는 것을 사용하면 된다. 잘 모르겠다면 되는 걸로 하자!

1.
```jsx
sudo apt-get update
sudo apt-get install -y python3-wstool python3-rosdep ninja-build stow
```
2.

On older distributions:
```jsx
sudo apt-get update
sudo apt-get install -y python-wstool python-rosdep ninja-build stow
```
cartorgrapher를 위한 workspace로  ‘carto_ws’를 생성
```jsx
mkdir carto_ws
cd carto_ws
wstool init src
wstool merge -t src https://raw.githubusercontent.com/cartographer-project/cartographer_ros/master/cartographer_ros.rosinstall
wstool update -t src
```
rosdep을 이용해 의존성 패키지들을 설치해 주어야 한다. 
```jsx
sudo rosdep init
rosdep update
rosdep install --from-paths src --ignore-src --rosdistro=*${*ROS_DISTRO*}* -y
```
해당 스크립트로 abseil.cpp 라이브러리를 설치할 것이다.

src/cartographer/scripts/install_abseil.sh

충돌이 생긴다면 제거도 고려해야 한다고 한다.
```jsx
sudo apt-get remove ros-*${*ROS_DISTRO*}*-abseil-cpp
```
빌드 및 설치!
```jsx
catkin_make_isolated --install --use-ninja
```
bashrc에 추가하여

```jsx
source ~/${워크스페이스}/install_isolated/setup.bash // 워크스페이스 => carto_ws
```

소스 설정도 잊지 말자

이후 cartographer를 사용하기 위해서는 configuration파일과 launch파일 작성이 중요하다.

configuration은 parameter들을 조작하는 것과 같다.

launch  file 구성에서 중요한 부분은 cartographer node, ouccpancy grid map node를 실행하는 것과

configuration 경로 설정이다.


