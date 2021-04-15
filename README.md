# Pasture_Monitoring_ENPM808
Use the following commands to run the gazebo simulation and save the point clouds using the hector quadcopter in Ubuntu 18:

Run the make_heights_and_xy_coords_npy_array.py file to amke the npy array for the entire pasture.  

Run the sort_lists_into_patches.py to sort that npy array into patches of specified dimensions.  

Use the npy arrays for patches in the blender script.

After generating the collada files for each patch, use spawn_patches_in_world_dae.py to combine all patches in a single .world file.

This .world file is copied in the catkin_ws. (available in google drive folder in report, will have to request ccess to view, work in progress)
# Making point clouds
```zsh

# in every new terminal do
source ~/catkin_ws/devel/setup.zsh #or setup.bash if you're using bash
#recommended to add this line in your .zshrc file

# in first terminal (relaunch and close everytime when restarting the scripts):
roscore
# in second terminal
roslaunch hector_quadrotor_demo pasture_and_quadcopter.launch
# in third terminal
rosrun point_cloud_processing transform_sim_and_save 

# to concatenate clouds, create ~/Data/Pointcloud directory, then:
rosrun point_cloud_processing concatenate_cloud <subdirectory name> <number of files>
rosrun point_cloud_processing concatenate_cloud /home/ksa/Data/PointCloud/9-18-2020/unfiltered/ 236

#controlling the quadcopter using teleop
rosservice call /enable_motors "enable: true"
rosrun teleop_twist_keyboard teleop_twist_keyboard.py 

# using autonomous navigation script
rosrun hector_quadrotor_navigation quadrotor_navigation_spawn_directly.py


#viewing the cloud
rosrun point_cloud_processing view_single_cloud /home/ksa/Data/PointCloud/concatenated_cloud.pcd

```

# Processing point clouds
```
#to use crop box filter on the point cloud for plot + 2m on each side to get plot_all
rosrun point_cloud_processing single_crop_box_filter /home/ksa/Desktop/Pasture_Monitoring/pcd_to_heights/plot_all_params.txt /home/ksa/Desktop/Pasture_Monitoring/pcd_to_heights/pasture.pcd

# for generating max_heights_point_cloud and csv files of points with height greater than mean+4*std_dev
rosrun point_cloud_processing plot_heights_std_dev_filter_with_max_heights <plot_only_params.txt>  <plot_till_2m_padding.pcd>

#plot_all path
/home/ksa/Desktop/Pasture_Monitoring/Patch_generation_pipeline1April/Python_scripts/plot_all_params.txt

#plot_only path
/home/ksa/Desktop/Pasture_Monitoring/Patch_generation_pipeline1April/Python_scripts/plot_only_params.txt


#for plot only so +0.2m on each side
rosrun point_cloud_processing single_crop_box_filter /home/ksa/Desktop/Pasture_Monitoring/pcd_to_heights/plot_only_params.txt /home/ksa/Desktop/Pasture_Monitoring/pcd_to_heights/pasture.pcd


/home/ksa/Desktop/Pasture_Monitoring/pcd_to_heights/plot_only_params.txt /home/ksa/Desktop/Pasture_Monitoring/pcd_to_heights/day91_april1_2009/april_1_day91_raw_concatenated_cloud_crop_box_filtered.pcd

rosrun point_cloud_processing plot_heights_std_dev_filter_with_max_heights <plot_only_params> <plot_all_crop_box_filtered_point_cloud>


rosrun point_cloud_processing turfgrass_heights /home/ksa/Desktop/Pasture_Monitoring/pcd_to_heights/pasture_10.2m_crop_box_filtered.pcd /home/ksa/Desktop/Pasture_Monitoring/pcd_to_heights/pasture_12m_crop_box_filtered.pcd

rosrun point_cloud_processing plot_heights plot_only_params.txt same_height_concatenated_cloud_crop_box_filtered_all.pcd


```

# Autonomous Navigation script
Install required packages:
```
pip install rospkg
pip3 install rospkg
sudo apt-get install ros-melodic-teleop-twist-keyboard
sudo apt-get install ros-melodic-teleop-twist-joy

```
Launching the script:
```
roscore
roslaunch hector_quadrotor_demo pasture_and_quadcopter.launch
rosrun hector_quadrotor_navigation quadrotor_navigation.py
```

# Recording and playing rosbag files
You can record the messages being published on all topics and view them later in Rviz(ROS Visualization) using:
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
 

# If MoveIt is required, use:
```
roslaunch hector_moveit_gazebo pasture.launch     
roslaunch hector_moveit_navigation navigate.launch
rosrun hector_moveit_navigation navigator_client
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
Use the command: 
```
sudo apt install ros-melodic-libfranka ros-melodic-franka-ros
```

If you get the error:
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


# Installing required packages:

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


# Required packages for Ubuntu 18
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


# Installing pcl in Ubuntu 18

```
sudo add-apt-repository ppa:sweptlaser/python3-pcl
sudo apt update
sudo apt install python3-pcl
```

Installing PCL1.9.1 under Ubuntu 18.04:
Recommended to compile it yourself
https://www.programmersought.com/article/5338520038/



















