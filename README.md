# xsens_imu_module

This module includes all necessary drivers to use the XSens IMU on the Silvanus robot with ROS. The module is completely containerized and can easily adapted to work with other robots because of Docker.

The xsens_imu_module is used in the [ball_picking_project repository](https://github.com/IFRoS-ELTE/ball_picking_project).
<br><br>
**Created by:** <br>
Kevin Schmidt: cbsx3q@inf.elte.hu

---

## Requirements

- Docker (engine)
- Docker Compose

Specific requirements and dependencies for the included ROS packages can be found in the Dockerfile. For more information about the containerization approach, refer to [this page](https://github.com/IFRoS-ELTE/ball_picking_project/blob/main/docs/docker.md).

## Setup for stand-alone use

### 0. IMPORTANT NOTE BEFORE USING THE PACKAGE

If you are running this on an x86 platform, everything is fine. Should you want to set this up on an ARM-based system like the Pomona robot (NVIDIA Jetson AGX Xavier with ARM CPU), you need to research where to get the version that can run on ARM. On the official website, there is no download link for that, so you have to do the digging yourself. An alternative could be to use the driver directly from the host OS, assuming there already exists an installation of the Suite and ROS driver.

### 1. Clone this repository recursively on the Scout2.0

```bash
git clone --recurse-submodules https://github.com/IFRoS-ELTE/xsens_imu_module.git
```

### 2. Build and launch the containers

```bash
cd ./xsens_imu_module/docker && sudo docker compose up
```

### Stopping and re-launching

To stop and close the nodes, simply use `CTRL+C`, this will stop all containers. You can use `sudo docker compose up` if you want to re-launch. If you, for some reason, want to remove the containers, you can do so with the `sudo docker compose down` command. This means that at the next startup using `sudo docker compose up`, the containers will be newly created and all the ros workspaces inside will have to be freshly built as well.

## Submodules

### [xsens_mti_driver](https://github.com/nobleo/xsens_mti_driver)

Repository by Nobleo that adapts the original ROS example from the MT SDK and provides a ROS wrapper for Kinetic, Melodic and Noetic.
