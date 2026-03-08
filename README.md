## System Setup (Ubuntu 22.04)

### 1. The One-Line ROS 2 Humble Setup (15 mins)
Check for UTF-8 and set locales:
```bash
locale
sudo apt update && sudo apt install locales -y
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8

##Install ROS 2 Humble (The "Fast" Way):
sudo apt update && sudo apt upgrade -y
sudo apt install software-properties-common -y
sudo add-apt-repository universe
sudo apt update && sudo apt install curl -y
sudo curl -sSL [https://raw.githubusercontent.com/ros/rosdistro/master/ros.key](https://raw.githubusercontent.com/ros/rosdistro/master/ros.key) -o /usr/share/keyrings/ros-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] [http://packages.ros.org/ros2/ubuntu](http://packages.ros.org/ros2/ubuntu) $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
sudo apt update && sudo apt install ros-humble-desktop-full ros-dev-tools -y


##Setup the Shell:

echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
source ~/.bashrc

###2. The PX4 & Gazebo Setup (30 mins)

##Clone the PX4 Autopilot firmware and run the setup script. It handles Gazebo automatically.
git clone [https://github.com/PX4/PX4-Autopilot.git](https://github.com/PX4/PX4-Autopilot.git) --recursive
bash PX4-Autopilot/Tools/setup/ubuntu.sh

REBOOT YOUR LAPTOP HERE.

###3. Move Your Mars Arena (10 mins)

    Copy your mars_final.glb and your mars_arena.sdf to the new Home folder.

    Put the .glb in ~/PX4-Autopilot/Tools/simulation/gz/models/ (or wherever you prefer).

###4. Launch the Simulation

##Open a fresh terminal and run this command to spawn the drone 0.5 meters in the air so it drops perfectly onto your rough arena.
Bash

export PX4_GZ_MODEL_POSE="0,0,0.5,0,0,0"
cd ~/PX4-Autopilot
PX4_GZ_WORLD=mars_arena make px4_sitl gz_x500


