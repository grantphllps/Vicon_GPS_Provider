# Azimuth Vicon GPS System
The azimuth GPS system gets postion data from a vicon system and turns it into NMEA position messages: GGA, VTG, RMC, HDT

- GGA for global postioning data
- VTG for course over ground
- RMC for course over ground and postion
- HDT for heading

## Enabling Heading from GPS
To enable heading From GPS, the following paramaters need to be set in Mission Planner:
		
- AHRS_EKF_TYPE=3
- GPS_TYPE=16
- COMPASS_USE=0
- COMPASS_USE2=0
- EK3_MAG_CAL=5
- EK3_SRC1_YAW=2

## Building the container
To build the container, clone the repository to the host machine and
Navigate to Vicon_GPS_Provider/docker/azimuth-gps and run:

```console
foo@bar:~$ docker build .
```

## Running the docker container
To use the docker container, there must be a vicon_bridge ROS node instance running somewhere on the ROS network. The container takes the following paramaters from a .env file:
		
- serial_port=/dev/ttyUSB0
- baud=115200
- lat={origin point latitude}
- lon={origin point longitude}
- vicon_targert={the path to the object's rostopic you want to track ex. "/vicon/AZIMUTH/AZIMUTH"}

The container must have access to a serial line the goes to the GPS port on the vehicle. Currently, the system runs as a privileged container to that it has access to the host device file.

Once the variables have been set, you can run the container with:

```console
foo@bar:~$ docker-compose --env-file .env up
```

run the above command in the same directory as the docker-compose.yml file, or provide docker-compose with the path to the file.


