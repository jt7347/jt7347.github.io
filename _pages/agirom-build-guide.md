---
layout: archive
title: "AgIRoM Build Guide (In Progress)"
permalink: /agirom-build-guide/
author_profile: true
---

Hi! This is AgIRoM, a replicated hardware platform for agile vision-based autonomous flight. Credits to UZH Robotics & Perception Group's work, as this platform largely builds from their own platform (Agilicious). AgIRoM explores the potential for drones that can navigate unknown, changing environments utilizing completely internal computation (onboard computers, computer vision, etc. ~ i.e. no external odometry or processing). On this page, you will find helpful information regarding how the platform works, and how to build/develop it!


**AgIRoM**             | 
:-------------------------:|
<img src='/images/AgIRoM_fullbuild.jpg' width=50%> |

# **[CITE FROM UZH RPG Agilicious](https://github.com/uzh-rpg/agilicious_internal#credits)**

## UZH RPG Agilicious Overview
UZH's Robotics and Perception Group recently open-sourced their Agilicious Platform. Agilicious contains both instructions and code to replicate the hardware platform that UZH have been using in their own research. More specifically, it provides a 'standardizable' approach to developing agile autonomous vision-based drones. This entails the inclusion of custom controllers, bridges, estimators, safety pipelines, simulators, and references. Akin to IRoM's own goal of having modular pieces of hardware that can be used in research applications, AgIRoM was built both as a means to conduct UAV research, but also to further the process of standardizing a platform (namely, UZH RPG's).
#### Their repo can be found here --> Link to UZH Agilicious: https://github.com/uzh-rpg/agilicious [need to request access]

## Hardware
_*It should be noted that AgIRoM is the platform's name, not the drones' names. Consequently, the builder of each respective quad is held responsible for naming it. For inspiration, some examples from UZH Agilicious have been "kingfisher," and "challenger."_
### Purchase List --> reach out if you'd like a copy of our purchase list!
### Betaflight Configurator Basics and Setup
You can install BTFL [here](https://github.com/betaflight/betaflight-configurator/releases). I would recommend getting the portable version as it is cleaner to uninstall (not a big deal, but if you use the regular installer and at some point you want to upgrade your configurator - to download a new version, you have to completely remove the old one - or just uninstall, you need to run the uninstaller executable - you can't manually uninstall through any other means as it won't clean up all the files correctly).
### Building the Quad
[CAD files](https://drive.google.com/drive/folders/1Tzs2kqsHFZzpwbWI1QNtdmwnGWETB-8e?usp=sharing) can be found here. Includes mounts/cases for Boson + Orin NX, T265, D435, and battery. Feel free to redesign any of the existing parts!
To build the quad, you will need M# hardware (nuts, bolts, nyloc nuts, heat set inserts), zipties, and the relevant parts listed in the purchase list. Refer to the following images for general build steps:
[add photos next time when build quad]
### Wiring
Agilicious uses serial UART to interface communications between the High-Level and Low-Level computers (Jetson Orin NX <=> Betaflight Flight Controller). In AgIRoM's case, this requires you to wire the RX/TX pads of the respective devices to each other (Note: typically, power cables for example would just wire + to +, and - to -, but in UART's case, you instead have to wire RX of one device to TX of the other and vice versa. Think of it as defining receiving and transmitting ends. If using the Boson Carrier Board + Orin NX and the SpeedyBeeF7 V3 flight controller for example, just simply find the RX/TX pins and pads on each device and wire them accordingly (manuals can also be found below in the Misc. Manuals section). Your choice of hardware may differ, and consequently the wiring may differ slightly, but ultimately the process is the same. Be sure to find out further configuration steps required to use the respective UART ports on each device --> e.g. steps to configure the serial interface for Orin found in the next section, and steps to toggle UART ports for specific purposes (telemetry, serial RX) found in Betaflight setup section.

<img src='/images/Boson_Plugs.PNG' width=20% height=20%>

[add thing about how to power orin and FC ~ cables and voltage step down module]

### Jetson Orin NX start guide
##### Physical setup
Refer to the following pictures for information on how to mount the Orin NX module
##### Booting up the Orin
First things - the Orin NX 16GB module does not have internal storage. Consequently, it relies on an external storage device on the carrier board to store the OS. However, SD cards will not work with the Boson Carrier board / Orin NX combo used in our version (Orins do not have SDIO configured). You will need to install an NVMe SSD storage card on the underside of the Boson carrier board. Once it has been inserted into the M.2 Key slot, alongside inserting the Orin NX module in place, you can begin the bootup process.

Refer to the Boson carrier board's manual for switches 2 and 3 locations - these are important, and act as the reboot, and force recovery pushbuttons respectively. 

<img src='/images/Boson.PNG' width=75%>

You will be using (https://connecttech.com/resource-center/kdb373/) to install the OS on the Orin NX. This step requires a "host" Linux computer with at least 40GB of free space. Peripherals you may find useful during this process include a mouse, keyboard, HDMI output to monitor, and an Ethernet connection.

To put the Orin NX in force recovery mode, simply hold down both switch 2 and 3, then release 2 whilst still holding 3, and then after a second, release switch 3. To verify that the device is in force recovery mode, whilst connected to the host computer via USB-C - type 'lsusb' into a terminal, after which if you have successfully put the device in force recovery mode, an NVIDIA device will be shown in the output (refer kdb373 guide). After flashing the OS successfully, you can follow (https://connecttech.com/resource-center/kdb374/) to install the extra SDK components.

During the flashing process (OS, SDKs), you may run into some kind of mount.nfs issue where the SDK manager will halt at the SSH step of the flashing. One possibility is due to the firewall being active. A quick fix for this is to temporarily disable the firewall of the host computer:
```
sudo ufw disable
```
Just remember to enable it again after (use 'enable' instead of 'disable').
##### Serial Configuration
Stuff to add: checking tty* ports available, finding which address corresponds to which port, adding user to dialout group, and useful terminal commands
### Measuring physical parameters of quad (weight, inertia matrix, max motor thrust/rpm, etc.)
### Misc. Manuals
##### [SpeedyBeeF7 V3 PDF Manual](https://store-fhxxhuiq8q.mybigcommerce.com/product_images/img_SpeedyBee%20F7V3_STACK/SpeedyBee_F7V3_Stack_Manua1.2_EN.pdf)
##### [ConnectTech Boson Carrier Board for Jetson Orin NX](https://connecttech.com/ftp/pdf/CTIM_NGX007_Manual.pdf) _(*IO expansion header pinout - for UART pins - on pg. 22-23)_
##### [Oscar Liang Flight Controller Basics](https://oscarliang.com/flight-controller-explained/)
##### [UART Basics](https://www.circuitbasics.com/basics-uart-communication/)

## Getting started
### Software Environment Setup 
##### --> Link to UZH Agilicious: https://github.com/uzh-rpg/agilicious [need to request access]. The main page contains pretty straightforward details on compiling the workspace/code and steps for launching first vision-based flight.
##### Dependencies and Misc. required installations
- Wifi: To connect the Orin NX to wifi, one option is to use an ethernet connection. However, this is only useful for the first few steps where being tethered by a wire is not a problem because you aren't actively flying the drone. ConnectTech's website refers to a wifi/bluetooth adapter for M.2 E-key wifi cards. Your other option is to use a USB wifi adapter - something similar to an [Archer T2U Nano AC600](https://www.tp-link.com/us/home-networking/usb-adapter/archer-t2u-nano/). These both should work fine, with a few additional software steps for the USB route:
> You will need to install the drivers for the AC600: I've found that both of these guides work interchangeably on occasion. Not sure which is the correct one to be honest, but one of them should work: [rtl8188au](https://github.com/aircrack-ng/rtl8812au) / [rtl8188eu](https://github.com/lwfinger/rtl8188eu/). Before doing this step, the Github pages will mention the need to install kernel headers for your system. If the boards you use do not install kernel headers by default (e.g. the Boson - Orin NX combo we use), you can follow [this](https://askubuntu.com/questions/75709/how-do-i-install-kernel-header-files) to install them. Try a few of the suggested commands here (sometimes some just work, and others don't).
- Librealsense: If you are using the T265, you will notice that it is 'deprecated' and no longer supported by Intel. This means the code for it has been removed from the newer versions of Librealsense. If you haven't made the switch to the D435i yet (TBD ~ future update here), you will need to install an build an older version of librealsense to interface with the T265. The following commands can be used to install v2.53.1:
```
git clone https://github.com/IntelRealSense/librealsense/tree/v2.53.1 # git cloning this may not work, so you can also just download the zip file (which is what I did)
cd librealsense/ # command may differ depending on how/where folder is cloned
### Install as needed...
sudo apt install libudev-dev pkg-config libgtk-2-dev
sudo apt install libudev-dev pkg-config libgtk-3-dev
sudo apt install libusb-1.0-0-dev pkg-config
sudo apt install libglfw3-dev
sudo apt install libssl-dev
sudo apt-get install libglfw3-dev libgl1-mesa-dev libglu1-mesa
sudo apt install cmake
###
sudo cp config/99-realsense-libusb.rules /etc/udev/rules.d/.
sudo udevadm control --reload-rules && udevadm trigger
mkdir build
cd build/
cmake ../ -DBUILD_EXAMPLES=true
make
sudo make install
cd tools/realsense-viewer
./realsense-viewer
```
NOTE: Some of the commands above may not work, but they may not be needed either. If one of them ends up holding you up, just ignore it and try finishing the rest --> the compiling and subsequent code may still work fine w/o those.
- Some more random steps along the way: 
```
sudo apt install ros-$ROS_DISTRO-mavros (installing mavros to get telemetry data from FC)
sudo apt install ros-$ROS_DISTRO-realsense2-camera (installing realsense2_camera for t265)
sudo /opt/ros/$ROS_DISTRO/lib/mavros/install_geographic_datasets.sh (installing geographiclib datasets ~ after catkin building the workspace, and before running vision-flight code; don't forget to re-source ros and catkin workspaces)
```
##### [Agilicious Docker Guide](https://github.com/uzh-rpg/agilicious_internal/blob/main/miscellaneous/documentation/how_to_docker.md)
Useful to avoid dependency/version conflicts. You can follow their steps for the most part ~ the step to run the docker container is a little unclear, but after you cd into the launch_container.sh directory, you can run
```
sudo sh launch_container.sh
```
to start the docker. Note that when you run the docker container, it creates an instance based on the defined 'image' of the container. This image is static and does not update inside the docker. As such, to save changes to the docker container (i.e. updating the 'image' s.t. running the docker commands will build a container based on the updated image), you will need to open a new terminal. To check active running docker images, you can use this command:
```
sudo docker ps
```
To update the current docker image with any added changes you want to keep, you can use:
```
sudo docker commit <container_id> ros_agilicious:latest
```
where \<container_id> is replaced by the CONTAINER ID string found by checking the running docker containers.

##### Config / parameter files
Agilicious contains many different config files, each specifying different run parameters. Knowing which to use, what each do, and which lines to edit is important, as plugging in a different config file without knowing what it does can be catastrophic (e.g. don't randomly sub in ekf_full_imu.yaml for the default ekf_full_no_imu.yaml in the pilot config definition, as this causes the T265's uptilt to be accounted for in the estimator and subsequently aggressively pitch the quad during takeoff - leading to a pretty fatal crash).

The important ones you'll need to edit to get the code running are [outdoor_betaflight_pilot.yaml](https://github.com/uzh-rpg/agilicious_internal/blob/main/agiros/agiros/parameters/outdoor_pilot_betaflight.yaml), [sbus.yaml](https://github.com/uzh-rpg/agilicious_internal/blob/main/agilib/params/sbus.yaml), and [betaflight.launch](https://github.com/uzh-rpg/agilicious_internal/blob/main/agiros/agiros/launch/mavros/betaflight.launch). In outdoor_betaflight_pilot.yaml, you'll need to sub in your "quadrotor" yaml file (default is kingfisher.yaml ~ these specify physical parameters of quad like weight, inertia, etc.); you will need to create one for each 'new' quad design you build. For sbus.yaml and betaflight.launch, you will need to specify the serial address each file is interfacing with. These addresses correspond differently for different carrier boards, but there should be a unique one for each UART port used. Make sure to put the UART address that corresponds to sending out data (TX) in the sbus.yaml file, and the UART address that corresponds to receiving data (RX) in betaflight.launch. This is done accordingly so because SBUS is the signal being sent out, whereas the betaflight mavros interface is used to receive telemetry input.

##### Launch your first real flight!

For 'Vision-Based Flight,' the Pilot will use the T265's VIO data for state estimation. By default, this information is not streamed so you will need to add a few lines of code to toggle these arguments on. In the t265_only.launch file, you will need to add the following as args:
```
<arg name="enable_accel" value="true"/>
<arg name="enable_gyro" value="true"/>
<arg name="enable_pose" value="true"/>
```
Doing so will start the pose stream, which can be confirmed by reasonable odometry values shown on the GUI when running the code.

To run the base code, you will need a basecomputer which will be used to communicate with the Orin. Run the following commands on both the Orin and basecomputer:

*NOTE: Desktop/Laptop and Drone must be on EXACT same wifi network. For example, even though Eduroam and ServiceNet are sort of 'linked,' this will not work --> they must be the same network (e.g. GasDyn for both devices...)
=> ROS Networking IPs below uses GasDyn wifi

_Commands for Basecomputer_

If you're using a docker container:
```
cd agirom/agilicious_internal/scripts
sudo sh launch_container.sh
```
else, you only need the following:
```
cd catkin_ws/src/agilicious_internal/agiros/agiros/launch/real_world
source /opt/ros/melodic/setup.bash
source ~/catkin_ws/devel/setup.bash
export ROS_IP=<IP_OF_THIS_DEVICE>
export ROS_MASTER_URI=http://<IP_OF_MASTER_HERE>:11311
roslaunch outdoor_basecomputer.launch quad_name:=agirom
```
_Commands for Quad (ssh from basecomputer in a different terminal)_
```
ssh agirom@<IP_ADDR_OF_ORIN>
cd catkin_ws/src/agilicious_internal/agiros/agiros/launch/real_world
source /opt/ros/noetic/setup.bash
source ~/catkin_ws/devel/setup.bash
export ROS_IP=<IP_OF_THIS_DEVICE>
export ROS_MASTER_URI=http://<IP_OF_MASTER_HERE>:11311
roslaunch outdoor_quadrotor.launch quad_name:=agirom
```
++ Designate either the quad or the basecomputer as the master, and use that device's IP address for \<IP_OF_MASTER_HERE>. \<IP_OF_THIS_DEVICE> on the other hand, is just the device's own IP address. These export steps set up the devices for ROS Networking.

[follow agilicious steps, mention key safety stuff]

***
# More Information regarding Agilicious

## Control
### Radio receivers, and SBUS protocol 
### Agilicious' custom SBUS bridge interface

### High-level Control
##### T265/D435 fusion
##### Simulation Softwares
##### Vision-Based Flight
##### Safety Pipelines and State Estimation

### Low-level Control
##### Controllers (MPC, GEO, INDI, PID)

## Sensors / Cameras Guide
### Intel Realsense T265
### Intel Realsense D435
### Realsense Commands
