# Pasture_Monitoring_ENPM808

Install the following packages to run pasture_generation.py:

```
sudo apt install python3-sympy  
sudo apt install collada-urdf-tools -y
sudo apt-get install python3-lxml python3-numpy python3-dateutil -y
#
#installing collada
sudo apt-get update -y
sudo apt install python3-pip -y
pip3 install pycollada
# you can also install:
sudo apt-get install python3-numpy python3-scipy python3-matplotlib ipython ipython-notebook python3-pandas  python3-nose
```

Install xlrd module for python3 in order to read the .xlsx file provided by APSIM:
```
pip3 install xlrd
```
Install octomap:
```
sudo apt-get install ros-melodic-octomap
sudo apt-get install ros-melodic-octomap-msgs
sudo apt-get install ros-melodic-octomap-ros
```
This was helpful: https://darienmt.com/autonomous-flight/2018/11/15/installing-ethz-rotors.html



# Learning Blender Scripting

1. To copy model - ```Shift + D```
2. To move model - Select model, Press ```G``` followed by x, y or z to move in that direction
3. To toggle between edit and object mode, use ```TAb```.
4. To select all vertices in edit mode, press ```A```
5. To apply all transforms to a model, aka set the current position as the default position: ```Ctrl```+```A```
6. To add models, use ```SHIFT```+```A```
7. Best view of camera at focal length of 200mm.


To copy the full data-path of the property under the mouse pointer press ```CTRL+ALT+SHIFT+C```

press ```CTRL+SPACE``` for command completion
 
# Installing Blender
Choose your version from the drop down list at: https://snapcraft.io/blender  
```
sudo snap install blender --classic
```
 
# Reinstallig Blender 
```
sudo snap remove blender
sudo apt-get purge teamviewer
wget https://download.teamviewer.com/download/linux/teamviewer_amd64.deb
sudo apt install -y ./teamviewer_amd64.deb
```

# Solving errors

When trying to do catkin_make you might get the error:
```
/home/kulbir/catkin_ws/src/hector_quadrotor_tutorial/hector_quadrotor/hector_quadrotor_navigation/src/quadrotor_navigation.cpp:5:10: fatal error: hector_uav_msgs/PoseAction.h: No such file or directory
 #include <hector_uav_msgs/PoseAction.h>
          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
compilation terminated.
hector_quadrotor_tutorial/hector_quadrotor/hector_quadrotor_navigation/CMakeFiles/quadrotor_navigation.dir/build.make:62: recipe for target 'hector_quadrotor_tutorial/hector_quadrotor/hector_quadrotor_navigation/CMakeFiles/quadrotor_navigation.dir/src/quadrotor_navigation.cpp.o' failed
make[2]: *** [hector_quadrotor_tutorial/hector_quadrotor/hector_quadrotor_navigation/CMakeFiles/quadrotor_navigation.dir/src/quadrotor_navigation.cpp.o] Error 1
CMakeFiles/Makefile2:9378: recipe for target 'hector_quadrotor_tutorial/hector_quadrotor/hector_quadrotor_navigation/CMakeFiles/quadrotor_navigation.dir/all' failed
```
Follow the link:https://github.com/tahsinkose/hector-moveit/issues/2 

Install moveit from source and install ROS again as well : https://moveit.ros.org/install/source/

### On linux mint, when installing ROS Melodic:
Use the first command:
```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu bionic main" > /etc/apt/sources.list.d/ros-latest.list'
```
So you have to write "bionic" instea of "$(lsb_release -sc)" as mentioned in the instructions for installing ROS on Ubuntu 18.04.
For Ubuntu 18.04 bionic beaver, its:  
```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list
```
Refer: https://forums.linuxmint.com/viewtopic.php?f=47&t=286659





When trying to do catkin_make you might get the error:
```
/home/ksa/catkin_ws/src/hector_quadrotor_tutorial/hector_moveit_gazebo_plugins/src/fruit_generator.cc: In member function ‘virtual void gazebo::FruitGenerator::Load(gazebo::physics::WorldPtr, sdf::ElementPtr)’:
/home/ksa/catkin_ws/src/hector_quadrotor_tutorial/hector_moveit_gazebo_plugins/src/fruit_generator.cc:23:32: error: ‘class gazebo::physics::World’ has no member named ‘GetModels’; did you mean ‘Models’?
         auto models = _parent->GetModels();
                                ^~~~~~~~~
                                Models
/home/ksa/catkin_ws/src/hector_quadrotor_tutorial/hector_moveit_gazebo_plugins/src/fruit_generator.cc:24:22: error: unable to deduce ‘auto&&’ from ‘models’
         for(auto m : models){
                      ^~~~~~

```

sudo apt install ros-melodic-libfranka ros-melodic-franka-ros


```
CMake Error at /opt/ros/melodic/share/catkin/cmake/catkinConfig.cmake:83 (find_package):
  Could not find a package configuration file provided by "moveit_core" with
  any of the following names:

    moveit_coreConfig.cmake
    moveit_core-config.cmake

  Add the installation prefix of "moveit_core" to CMAKE_PREFIX_PATH or set
  "moveit_core_DIR" to a directory containing one of the above files.  If
  "moveit_core" provides a separate development package or SDK, be sure it
  has been installed.
Call Stack (most recent call first):
  hector_quadrotor_tutorial/hector_moveit_exploration/CMakeLists.txt:6 (find_package)
  
```
do ```sudo apt-get install ros-melodic-moveit*```


```
sudo apt-get install ros-melodic-octomap
sudo apt-get install ros-melodic-octomap-msgs
sudo apt-get install ros-melodic-octomap-ros
```


# hector_quadrotor_tutorial
Hector quadrotor with modified files

Installed required packages
# For Ubuntu 18
```
sudo apt install qt4-default

sudo apt-get install ros-melodic-moveit ros-melodic-velodyne-gazebo-plugins ros-melodic-geographic-info ros-melodic-geographic-msgs ros-melodic-ros-control ros-melodic-hardware-interface ros-melodic-controller-interface ros-melodic-gazebo-ros-control ros-melodic-joy ros-melodic-teleop-twist-keyboard

git clone https://aur.archlinux.org/ros-melodic-geographic-msgs.git
```


After you download the repo, to change into a branch, do:
```
git checkout "name of branch"

git checkout "melodic"
```

Go to ```/home/$user/catkin_ws/src/hector_quadrotor_tutorial/hector_moveit_gazebo_plugins/src/fruit_generator.cc``` and change its contents.
Paste the contents from hector-moveit/src/hector_moveit_gazebo_plugins/src/fruit_generator.cc. It is available at https://github.com/tahsinkose/hector-moveit/blob/melodic-devel/src/hector_moveit_gazebo_plugins/src/fruit_generator.cc


If you get the error:
```
[Err] [REST.cc:205] Error in REST request

libcurl: (51) SSL: no alternative certificate subject name matches target host name 'api.ignitionfuel.org'
```
Follow the steps on: 
https://varhowto.com/how-to-fix-libcurl-51-ssl-no-alternative-certificate-subject-name-matches-target-host-name-api-ignitionfuel-org-gazebo-ubuntu-ros-melodic/

# Making point clouds
```zsh

# in every new terminal do
source ~/catkin_ws/devel/setup.zsh #or setup.bash if you're using bash
#recommended to add this line in your .zshrc file

# in first terminal:
roscore
# in second terminal
roslaunch hector_quadrotor_demo pasture_and_quadcopter.launch
# in third terminal
roslaunch point_cloud_processing sim_transform.launch 
# in fourth terminal
rosrun point_cloud_processing save_cloud
#or
rosrun point_cloud_processing transform_sim_and_save 

# to concatenate clouds
rosrun point_cloud_processing concatenate_cloud <subdirectory name> <number of files>
rosrun point_cloud_processing concatenate_cloud /home/ksa/Data/PointCloud/9-18-2020/unfiltered/ 236

#controlling the quadcopter
rosservice call /enable_motors "enable: true"
rosrun teleop_twist_keyboard teleop_twist_keyboard.py 

#viewing the cloud
rosrun point_cloud_processing view_single_cloud /home/ksa/Data/PointCloud/concatenated_cloud.pcd

```


# Autonomous Navigation script
```
pip install rospkg
pip3 install rospkg
sudo apt-get install ros-melodic-teleop-twist-keyboard
sudo apt-get install ros-melodic-teleop-twist-joy

```

```
roscore
roslaunch hector_quadrotor_demo pasture_and_quadcopter.launch
rosrun hector_quadrotor_navigation quadrotor_navigation.py



#do not do roslaunch hector_quadrotor_demo cafe.launch

# the following command launches moveit as well
roslaunch hector_moveit_gazebo pasture.launch     
roslaunch hector_moveit_navigation navigate.launch
rosrun hector_moveit_navigation navigator_client
# Installing pcl in Ubuntu 18
```
```
sudo add-apt-repository ppa:sweptlaser/python3-pcl
sudo apt update
sudo apt install python3-pcl
```
# Recording and playing rosbag files
```
#to record a rosbag file
rosbag record -a

#to play the rosbag file and see it in rviz
#in first terminal
rosparam set /use_sim_time "true"
#toggle spacebar to play/pause the rosbag file
rosbag play --pause -l --clock 2020-09-23-21-46-48.bag
#in another terminal
rviz rviz
```





Installing PCL1.9.1 under Ubuntu 18.04:
Recommended to compile it yourself
https://www.programmersought.com/article/5338520038/

# Using the PS4 controller to control the quadcopter




# Installing pcl dependencies

```
sudo apt-get update  
sudo apt-get install git build-essential linux-libc-dev  
sudo apt-get install cmake cmake-gui 
sudo apt-get install libusb-1.0-0-dev libusb-dev libudev-dev  
sudo apt-get install mpi-default-dev openmpi-bin openmpi-common  
```

```
sudo apt-get install libflann1.8 libflann-dev  
sudo apt-get install libeigen3-dev   
sudo apt-get install libboost-all-dev   
sudo apt-get install libvtk5.10-qt4 libvtk5.10 libvtk5-dev  
```

```
sudo apt-get install libqhull* libgtest-dev    
sudo apt-get install freeglut3-dev pkg-config  
sudo apt-get install libxmu-dev libxi-dev   
sudo apt-get install mono-complete  
sudo apt-get install qt-sdk openjdk-8-jdk openjdk-8-jre 
```

```
git clone https://github.com/PointCloudLibrary/pcl.git 
cd pcl 
mkdir release 
cd release
cmake -DCMAKE_BUILD_TYPE=None -DCMAKE_INSTALL_PREFIX=/usr \ -DBUILD_GPU=ON-DBUILD_apps=ON -DBUILD_examples=ON \ -DCMAKE_INSTALL_PREFIX=/usr ..
make
sudo make install
```

```
 sudo apt-get install libopenni-dev 
 sudo apt-get install libopenni2-dev
```
just follow the link above for further commands...


```


# DroneBody not found error

```
[ERROR] [1600650400.794297166, 316.434000000]: Robot semantic description not found. Did you forget to define or remap '/robot_description_semantic'?
[ INFO] [1600650400.795942937, 316.436000000]: Loading robot model 'quadrotor'...
[ INFO] [1600650400.796035342, 316.436000000]: No root/virtual joint specified in SRDF. Assuming fixed joint
[FATAL] [1600650400.850831323, 316.490000000]: Group 'DroneBody' was not found.
terminate called after throwing an instance of 'std::runtime_error'
  what():  Group 'DroneBody' was not found.
[hector_navigator-2] process has died [pid 14128, exit code -6, cmd /home/ksa/catkin_ws/devel/lib/hector_moveit_navigation/hector_navigator __name:=hector_navigator __log:=/home/ksa/.ros/log/e17ae0b2-fba5-11ea-91ca-e454e856a08c/hector_navigator-2.log].
log file: /home/ksa/.ros/log/e17ae0b2-fba5-11ea-91ca-e454e856a08c/hector_navigator-2*.log
```


```


```



















