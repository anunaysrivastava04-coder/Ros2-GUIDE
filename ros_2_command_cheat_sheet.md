# 💻 ROS 2 Essential Commands Cheat Sheet

This guide contains the most important and frequently used ROS 2 terminal commands for daily development, debugging, and workspace management. 

🔗 **Official Reference:** [ROS 2 CLI Tools Documentation](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools.html)

---

## 🌍 1. Environment & Sourcing
Before running any ROS 2 commands, your terminal must know where ROS 2 and your custom code live.

* **Source the main ROS 2 installation:**
  ```bash
  source /opt/ros/humble/setup.bash
  ```
* **Source your custom workspace:** *(Run this from inside your `ros2_ws` directory)*
  ```bash
  source install/setup.bash
  ```
* **Check your ROS environment variables:**
  ```bash
  printenv | grep -i ROS
  ```

---

## 📦 2. Workspace & Building (Colcon)
Used for compiling your custom ROS 2 C++ and Python packages.
🔗 **Reference:** [Colcon Documentation](https://colcon.readthedocs.io/)

* **Build the entire workspace:**
  ```bash
  colcon build
  ```
* **Build only a specific package:**
  ```bash
  colcon build --packages-select <package_name>
  ```
* **Build with symlink install:** *(Highly recommended for Python developers - allows changing Python code without needing to rebuild)*
  ```bash
  colcon build --symlink-install
  ```

---

## 🧩 3. Package Management
Used to create new code packages and install missing dependencies.

* **Create a new Python package:**
  ```bash
  ros2 pkg create --build-type ament_python <package_name>
  ```
* **Create a new C++ package:**
  ```bash
  ros2 pkg create --build-type ament_cmake <package_name>
  ```
* **Install missing dependencies automatically:** *(Run from the root of your workspace)*
  ```bash
  rosdep install -i --from-path src --rosdistro humble -y
  ```

---

## 🤖 4. Node Management
Nodes are the individual running programs in your ROS 2 network.

* **Start/Run a node:**
  ```bash
  ros2 run <package_name> <executable_name>
  ```
* **List all currently running nodes:**
  ```bash
  ros2 node list
  ```
* **Get detailed info about a specific node:** *(Shows its topics, services, and actions)*
  ```bash
  ros2 node info /<node_name>
  ```

---

## 📡 5. Topic Management
Topics are the continuous data streams (like camera feeds or sensor data) nodes use to talk to each other.

* **List all active topics:**
  ```bash
  ros2 topic list
  ```
* **List topics with their message types:**
  ```bash
  ros2 topic list -t
  ```
* **Read live data from a topic (Echo):**
  ```bash
  ros2 topic echo /<topic_name>
  ```
* **Check the publishing rate (Hz) of a topic:**
  ```bash
  ros2 topic hz /<topic_name>
  ```
* **Manually publish a message to a topic from the terminal:**
  ```bash
  ros2 topic pub /<topic_name> <message_type> "{data: 'Hello ROS 2'}"
  ```

---

## 🛎️ 6. Service Management
Services are for quick, synchronous "Call and Response" interactions (e.g., "turn on the light", "save this map").

* **List all available services:**
  ```bash
  ros2 service list
  ```
* **Call a service manually from the terminal:**
  ```bash
  ros2 service call /<service_name> <service_type> "{request_data}"
  ```

---

## ⚙️ 7. Parameter Management
Parameters are the configuration settings for your nodes (e.g., setting a camera's frame rate or a robot's max speed).

* **List all parameters for all nodes:**
  ```bash
  ros2 param list
  ```
* **Get the current value of a specific parameter:**
  ```bash
  ros2 param get <node_name> <parameter_name>
  ```
* **Set a new value for a parameter dynamically:**
  ```bash
  ros2 param set <node_name> <parameter_name> <new_value>
  ```
* **Save all current parameters to a file:**
  ```bash
  ros2 param dump <node_name> > settings.yaml
  ```

---

## 🚀 8. Launch Files
Launch files allow you to start multiple nodes and configure them all at once with a single command.

* **Run a launch file:**
  ```bash
  ros2 launch <package_name> <launch_file_name.launch.py>
  ```

---

## 📊 9. Recording Data (ROS 2 Bags)
"Bags" allow you to record live sensor data so you can play it back later for testing.

* **Record specific topics:**
  ```bash
  ros2 bag record /<topic_1> /<topic_2>
  ```
* **Record all active topics:**
  ```bash
  ros2 bag record -a
  ```
* **Play back a recorded bag file:**
  ```bash
  ros2 bag play <bag_file_name>
  ```