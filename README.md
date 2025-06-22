# Jackal Navigation Project 

 This project demonstrates mapping and autonomous navigation using the Jackal
robot in Gazebo and ROS.

## Files 

 - my_jackal_map.pgm: The map image.
 - my_jackal_map.yaml: Map metadata for ROS navigation.

## How to use 

 1. **Open a terminal and source the ROS Kinetic environment and
    your workspace:**

	source /opt/ros/kinetic/setup.bash
	souce ~/catkin_ws/devel/setup.bash
	
 2. **Start the Jackal simulation in Gazebo with the front laser enabled:**

	roslaunch jackal_gazebo jackal_world.launch config:=front_laser

 3. **(Optional) In a new terminal, source the ROS environment,
    your workspase and start RVIZ to visualize the robot and the map:**

	source /opt/ros/kinetic/setup.bash
	source ~/catkin_ws/devel/setup.bash
	roslaunch jackal_viz view_robot.launch config:=gmapping

 4. **(Optional: Mapping step, if you want to create a new map)** 
    In a new terminal, source the ROS environment and your workspace and start
    SLAM mapping:

    If your lidar publishes on the default topic `/front/scan`:

	source /opt/ros/kinetic/setup.bash
	source ~/catkin_ws/devel/setup.bash
	roslaunch jackal_navigation gmapping_demo.launch

    If your lidar uses a different topic, specify it with the `scan_topic` 
    argument:

        source /opt/ros/kinetic/setup.bash
        source ~/catkin_ws/devel/setup.bash
        roslaunch jackal_navigation gmapping_demo.launch 
	scan_topic:=/your_scan_topic

    You do not need to run both commands - choose the one that matches 
    your setup. If you're unsure about your scan topic, you can check it with:
	
	rostopic list

 5. Drive the robot around the environment to build the map. 
    When finished, save the map:

        source /opt/ros/kinetic/setup.bash
        source ~/catkin_ws/devel/setup.bash
        rosrun map_server map_saver -f ~/my_jackal_map

    This will create `my_jackal_map.pgm` and `my_jackal_map.yaml`.
 
 6. **To use your saved map for autonomous navigation, in a new terminal 
    source the ROS environment and your workspace and run:**

	If your lidar publishes on the default topic `/front/scan`:

        source /opt/ros/kinetic/setup.bash
        source ~/catkin_ws/devel/setup.bash
        roslaunch jackal_navigation amcl_demo.launch 
    map_file:=/home/YOUR_USERNAME/Jjackal_navigation_project/my_jackal_map.yaml 

    Replace `YOUR_USERNAME` with your Ubuntu username.

 6. **In RViz, use the 2D Nav Goal tool (green arrow icon) to click
    on the map and set a goal for the robot.**

    The robot will plan a path and drive to the goal automatically.

