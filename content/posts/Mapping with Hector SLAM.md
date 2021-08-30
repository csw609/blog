---
title: "Mapping with Hector SLAM (ROS)"
date: 2021-08-31T06:04:44+09:00
---

# Mapping with Hector SLAM

---
LiDAR : RPLIDAR A3 

패키지 : hector_slam (hector_mapping, hector_geotiff)

환경 : ubuntu 18.04, ROS

---

LiDAR를 이용해 연구실 map을 만들고자 한다.

이를 위해 2D LiDAR SLAM알고리즘인 Hector SLAM을 사용하려한다.

RPLIDAR 패키지 [http://wiki.ros.org/rplidar](http://wiki.ros.org/rplidar)

{{< figure src="/Mapping with Hector SLAM/_2021-05-04_04-40-44.png">}}

현재는 LiDAR만으로 mapping을 진행하므로 hector mapping에 별도의 odom을 제공할 수가 없다

따라서 hector mapping이 만드는 odom transform을 사용한다.

⇩ hector mapping ros wiki

{{< figure src="/Mapping with Hector SLAM/_2021-05-03_01-30-21.png">}}

rplidar_a3.launch 파일을 보면

{{< figure src="/Mapping with Hector SLAM/_2021-05-03_01-33-10.png">}}

rplidar의 frame_id는 **laser**이므로

```
    <param name="base_frame" value="laser" />
```

baser_frame에 대한 위와 같은 설정이 필요하다 value를 **"laser"** 로 하였

hector mapping with rplidar a3

baudrate : 256000

Topic : map(/map), LaserScan(/scan), Pose(/slam_out_pose)

{{< figure src="/Mapping with Hector SLAM/_2021-05-03_02-59-03.png">}}

Map을 저장하기 위해서는 hector_geotiff package를 사용해야한다.

해당 패키지를 실행 후 

{{< figure src="/Mapping with Hector SLAM/_2021-05-03_03-02-05.png">}}

"savegeotiff"라는 syscommand를 publish해주어야한다.

{{< figure src="/Mapping with Hector SLAM/_2021-05-03_02-59-48.png">}}

{{< figure src="/Mapping with Hector SLAM/_2021-05-03_03-13-32.png">}}

주기적으로 자동 저장하기를 원한다면

{{< figure src="/Mapping with Hector SLAM/_2021-05-03_03-17-28.png">}}

"geotiff_save_period" 해당 파라미터의 값을 원하는 주기(sec)로 조작하면 된다.

{{< figure src="/Mapping with Hector SLAM/_2021-05-03_08-39-30.png">}}

{{< figure src="/Mapping with Hector SLAM/_2021-05-03_08-40-41.png">}}