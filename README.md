# multi livox lidar connection with docker macvlan

Docker based implememtation to use multiple livox lidars simultaneously without livox hub.


* [Prerequisites](#prereqs)
* [Building docker image for different types of lidar](#build_image)
* [docker run](#docker_run)
* [Output](#output)

<a name="prereqs"></a>
## Prerequisites

* ROS noetic/melodic docker image as base image
* https://hub.docker.com/_/ros/
* docker pull ros:noetic

<a name="build_image"></a>
## Building docker image for different models like Livox MID360 and Livox Avia
```
just run the command to build the docker image.
docker built -t mid360 -f Dockerfile . -> mid360 docker image
docker built -t avia -f Dockerfile . -> avia docker image
```

<a name="docker_run"></a>
## running the application
Each docker image is configured in docker-compose.yml. Just run docker-compose up to run the containers. You can provide the Entrypoints to start the livox-ros-driver inside the container or just put the commands to run in docker-compose.yml. I prefer to use in docker-compose.yml for easy debugging.

```
docker-compose up -d
/opt/catking_ws -> to run the livox-ros-driver and publish the output in common ROS_MASTER_URI.
```

<a name="output"></a>
## Output
You will get the output in 3rd container which is a bridge between the 2 containers (i used 2 lidars and hence 2 containers respectively). You can mount any host directry and just dump/use the published /livox/lidar or /livox/imu messages here in 3rd container.


