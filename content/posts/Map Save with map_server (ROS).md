---
title: "Map Save with map_server (ROS)"
date: 2021-08-31T07:04:44+09:00
---
# Map Save with map_server (ROS)

SLAM으로 Mapping후 해당 Map을 저장하고 다시 불러오기 위해서는 

map_server라는 패키지를 사용할 수 있다.

해당 패키지를 사용하면 저장한 맵을 이후에 map_server node를 사용해 손쉽게 publish할 수도 있다.

{{< figure src="/Map Save with map_server (ROS)/_2021-05-07_02-50-02.png">}}

해당 패키지는 navigation package에 포함되어있다.

따라서 navigation package를 설치하면 map_server 패키지도 사용할 수 있다.

navigation package를 다운로드하고 build하다 보면 설치되지 않은 의존성 패키지들에 의해 오류가 많이 발생한다.

 본인은 tf2_sensor_msgs에 관한 오류를 만났는데

```
sudo apt-get install ros-melodic-tf2-sensor-msgs (melodic 기준)
```

관련 package를 설치함으로써 해결할 수 있다.