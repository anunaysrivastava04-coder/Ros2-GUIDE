# ROS Installation & Getting Started Guide

This repository contains step-by-step instructions for installing the Robot Operating System (ROS) on Ubuntu, as well as a complete beginner's guide to starting and using ROS 2.

> **Note:** The primary instructions below are for **ROS 2 Humble Hawksbill** (supported on Ubuntu 22.04). If you are looking for ROS 1 (Noetic) instructions based on the [ROS Wiki](https://wiki.ros.org/Installation/Ubuntu), please scroll to the bottom section.

---

## 🛠️ Part 1: Installing ROS 2 Humble (Ubuntu 22.04)

Follow these standard Debian package installation steps in your terminal to get ROS 2 up and running.

### 1. Check Locale
Make sure you have a locale that supports `UTF-8`.
```bash
locale  # check for UTF-8

sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
```

### 2. Enable the Universe Repository
Ensure the Ubuntu Universe repository is enabled on your system:
```bash
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository universe
```

### 3. Add the ROS 2 GPG Key and Repository
Add the official ROS 2 repository to your system so `apt` knows where to download the packages from:
```bash
sudo apt update && sudo apt install curl -y

# Download the ROS GPG key
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg

# Add the repository to your sources list
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

### 4. Install ROS 2 Packages
Update your system packages to recognize the new repository, and install ROS 2.

**Option A: Desktop Install (Recommended)** - *Includes ROS, RViz, demos, tutorials, and standard tools.*
```bash
sudo apt update
sudo apt upgrade
sudo apt install ros-humble-desktop
```

**Option B: ROS-Base Install (Bare Bones)** - *No GUI tools.*
```bash
sudo apt install ros-humble-ros-base
```

### 5. Source the Environment
You must source the setup script every time you open a new terminal. To do this automatically, add it to your `.bashrc`:
```bash
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

---

## 🚀 Part 2: How to Start and Use ROS 2 (Full Guide)

ROS 2 doesn't have a single desktop icon you click to "open" it. Instead, it is a collection of command-line tools, background processes, and visual interfaces. Here is your complete guide to starting and using ROS 2 on Ubuntu.

### 1. The Basic Test: Talker & Listener
To prove ROS 2 is running, you run "nodes" (individual ROS programs) from the terminal. 
1. Open a terminal (`Ctrl` + `Alt` + `T`).
2. Run the talker node:
   ```bash
   ros2 run demo_nodes_cpp talker
   ```
3. Open a **second** terminal (`Ctrl` + `Alt` + `T`) and run the listener node:
   ```bash
   ros2 run demo_nodes_cpp listener
   ```
*(Stop them anytime by pressing `Ctrl` + `C` in the terminal).*

### 2. Essential ROS 2 Commands
While your talker and listener are running in the background, open a **third** terminal. Here are the commands you will use every day to inspect what is happening inside your ROS 2 network:

* **List running nodes:** See all active ROS 2 programs.
  ```bash
  ros2 node list
  ```
* **List active topics:** See the communication channels where data is flowing.
  ```bash
  ros2 topic list
  ```
* **Echo a topic:** Actually read the live data flowing through a specific topic (like the chatter topic).
  ```bash
  ros2 topic echo /chatter
  ```

### 3. Opening ROS 2 Visual Tools (GUIs)
If you installed the `desktop` version, you have powerful visual tools built-in. You open these simply by typing their names into the terminal.

* **Launch RViz 2 (3D Visualization):** Used to see your robot's sensors, cameras, and 3D environment.
  ```bash
  rviz2
  ```
* **Launch RQt (Graph and Data Interface):** Used to plot data, view node graphs, and manage parameters.
  ```bash
  rqt
  ```
  *(Tip: Inside rqt, go to Plugins -> Introspection -> Node Graph to see a visual map of your running nodes).*

### 4. Setting up a Workspace (To write your own code)
To actually build your own robot, you need to create a ROS 2 workspace. 

1. **Install Colcon** (The ROS 2 build tool):
   ```bash
   sudo apt install python3-colcon-common-extensions python3-rosdep
   sudo rosdep init
   rosdep update
   ```
2. **Create the workspace folders:**
   ```bash
   mkdir -p ~/ros2_ws/src
   cd ~/ros2_ws
   ```
3. **Build the workspace:**
   ```bash
   colcon build
   ```
4. **Source your new workspace:** (Do this so the terminal knows about your custom code).
   ```bash
   source ~/ros2_ws/install/setup.bash
   ```

You are now ready to create custom ROS 2 packages inside the `~/ros2_ws/src` directory!

---

## 📜 Appendix: Installing ROS 1 Noetic (Ubuntu 20.04)

*Reference: [ROS 1 Ubuntu Installation Wiki](https://wiki.ros.org/Installation/Ubuntu)*

If you are using an older system (**Ubuntu 20.04**) and need ROS 1, use these steps:

```bash
# 1. Setup sources
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'

# 2. Setup keys
sudo apt install curl
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -

# 3. Installation
sudo apt update
sudo apt install ros-noetic-desktop-full

# 4. Environment setup
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
source ~/.bashrc

# 5. Dependencies
sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
sudo rosdep init
rosdep update
```