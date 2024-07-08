First we had to setup our computers for working on the assingned task.i did my work on Virtual machine because of which it turned out to be slow . but I am sharing all that I could learn while executing the task.first for the task 1 we had to install tb3 in our systems.for which I gave th efollowing commonds I  the terminal.

mkdir ws(which just creates a folder having name ws)
cd ws(which changes the directory to ws)
Mkdir src(making src folder in ws)
Cd src
Git clone https://github.com/ROBOTIS-GIT/turtlebot3.git (this will create a turtlebot3 flie inside the src folder)
git clone https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git(this will create turtlebot3_simulations folder inside thsrc folder)
cd turtlebot3_simulations/(change directory)

git checkout noetic-devel (this will change the branch to noetic devel)

cp . .. -r(this commond is copying the content of the current directory  which is the turtlebot3_simulations to the parent directory which is the src folder)
cd ..
 rm -rf turtlebot3_simulations/(by this we are deleting the turtlebot3_simulations folder)
cd ..
rosdep install --from-paths src --ignore-src -r -y(by this commond we are installing all the dependencies requires for packages in the src folder)
catkin_make(this will develop the ws)
export TURTLEBOT3_MODE =waffle
cd ~/ws/
source devel/setup.bash
(these commonds will install the required turtlebot3 package )


Now after the installation tb3 we need to clone the worlds provided 
Cd ws
Cd src
Git clone https://github.com/mlherd/Dataset-of-Gazebo-Worlds-Models-and-Maps.git (this will create a folder named datasets-of-……. In the the src folder(I have renamed it as custom_worlds))
(Now I wanted to use the hospital world so I putted the world file of the hospital in the turtlebot3_gazebo/worlds folder)and after that put all the models of the hospital world in the .gazebo/models directory (this is a hidden directroy)
Which can be seen by typing (ctrl-H).and give commond on terminal as 
Export GAZEBO_MODEL_PATH=/home/nitika/.gazebo/models

And also put a launch file(named hospital.launch) inside the launch folder of the turtlebot3_gazebo/launch directory.

After this your world is ready to be launched in the gazebo enviroment.

Give the commond and also add the commond export TURTLEBOT3_MODEL=waffle before that. (roslaunch turtlebot3_gazebo hospital.launch )to launch the world in the gazebo enviroment.


And after that launch the RVIZ enviroment  
-export TURTLEBOT3_MODEL=waffle 
-roslaunch turltebot3_slam turltebot3_slam.launch slam_methods:=gmapping

Also add topics (map topic,robot,sensors in the rviz enviroment.)


And then teleop the robot
-export TURTLEBOT3_MODEL=waffle 
-roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch 

This will teleop the robot and after providing it with linear velocities and angular velocities we are going to map the world.


And then finally add the commond when allthe ma is ready in rviz enviroment 
Rosrun map_server map_saver  ~f/hospital.yaml
This will save the fmap with the file_name.yaml extension and also save other file having extension .pgm .

And after this to perform navigation.

Open terminal and the following commonds in the terminal.
On one terminal add the commond
-export TURTLEBOT3_MODEL=waffle 
Roslaunch turtlebot3_gazebo hospital.launch
(this will open the world in gazebo)


And on another terminal give the following commonds
-export TURTLEBOT3_MODEL=waffle 
-roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/hospital.yaml


And after this do the point estimate of the inital position of the robot in the gazebo enviroment using the 2D point estimate. Click on the point where you think the robot is in the gazebo enviroment.
Then click on 2D nav goal commond and select the final position where you want your robot to be and and also specify the angle. The robot will start moving towards the final destination as we specify the final position and angle.
