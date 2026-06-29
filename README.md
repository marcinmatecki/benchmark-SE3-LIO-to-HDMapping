# [SE3-LIO](https://github.com/url-kaist/se3-lio) converter to [HDMapping](https://github.com/MapsHD/HDMapping)

## Hint

Please change branch to:

[Bunker-DVI-Dataset-reg-1](https://github.com/MapsHD/benchmark-SE3-LIO-to-HDMapping/tree/Bunker-DVI-Dataset-reg-1)

for quick experiment.

---

## Intended use

This repository integrates **SE3-LIO** with **HDMapping**.

It contains:

- SE3-LIO workspace
- tested SE3-LIO configuration
- converter for HDMapping output

SE3-LIO provides odometry and registered point clouds:

```
/local/cloud_registered_body
/local/odometry
```

---

## Dependencies

```bash
sudo apt install -y nlohmann-json3-dev
```

---

## Build

Clone repository:

```bash
mkdir -p ~/test_ws/src

cd ~/test_ws/src

git clone https://github.com/MapsHD/benchmark-SE3-LIO-to-HDMapping.git --recursive

cd ~/test_ws

catkin_make
```

Source workspace:

```bash
source /opt/ros/noetic/setup.bash
source ~/test_ws/devel/setup.bash
```

---

# Usage

## Start SE3-LIO

Run:

```bash
roslaunch se3_lio run_se3lio_ncd.launch use_sim_time:=true
```

---

## Play dataset

In another terminal:

```bash
source /opt/ros/noetic/setup.bash
source ~/test_ws/devel/setup.bash

rosbag play <dataset.bag> --clock
```

---

## Record SE3-LIO output

Record topics:

```bash
rosbag record \
/local/cloud_registered_body \
/local/odometry \
-O recorded-se3-lio.bag
```

---

## Convert to HDMapping

After recording:

```bash
source /opt/ros/noetic/setup.bash
source ~/test_ws/devel/setup.bash

rosrun se3-lio-to-hdmapping listener \
recorded-se3-lio.bag \
output_hdmapping
```

Output:

```
output_hdmapping/
```

---

## Stop

Stop launch and recording:

```
CTRL+C
```