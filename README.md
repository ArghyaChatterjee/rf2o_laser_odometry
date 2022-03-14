# Odometry from 2D Lidar or Laser Scanner
Estimation of 2D odometry based on planar laser scans. Useful for mobile robots with innacurate base odometry. 

# Platform test
Tested with Ubuntu 18.04, ros melodic and rplidar A1M8 and A2M8 (2D laser scanner).

# Testing
First on one terminal, type:
```
cd catkin_ws
source devel/setup.bash
roslaunch rf2o_laser_odometry sensors.launch
```
N.B: Common problem with rplidar 
```
[ INFO] [1647249454.182837019]: RPLIDAR running on ROS package rplidar_ros, SDK Version:2.0.0
*** buffer overflow detected ***: /home/arghya/catkin_ws/devel/lib/rplidar_ros/rplidarNode terminated
```
To solve this problem, in the same terminal, type:
```
sudo chmod 777 /dev/ttyUSB0
```
Then rerun the node to get the sensors and necessary tf frames published before rf2o node.

On another terminal, type:
```
cd catkin_ws
source devel/setup.bash
roslaunch rf2o_laser_odometry rf2o_laser_odometry.launch 
```
An rviz display will publish and after proper rviz configuration, you will be able to see the following:
<p align="center">
    <img src="assets/odom_test.giff", width="800">
</p>


# Description
RF2O is a fast and precise method to estimate the planar motion of a lidar from consecutive range scans. For every scanned point we formulate the range flow constraint equation in terms of the sensor velocity, and minimize a robust function of the resulting geometric constraints to obtain the motion estimate. Conversely to traditional approaches, this method does not search for correspondences but performs dense scan alignment based on the scan gradients, in the fashion of dense 3D visual odometry. 

Its very low computational cost (0.9 milliseconds on a single CPU core) together whit its high precission, makes RF2O a suitable method for those robotic applications that require planar odometry.

For full description of the algorithm, please refer to: **Planar Odometry from a Radial Laser Scanner. A Range Flow-based Approach. ICRA 2016** Available at: http://mapir.isa.uma.es/work/rf2o
