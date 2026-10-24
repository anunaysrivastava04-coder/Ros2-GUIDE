# 💻 ROS 2 System Requirements

While ROS 2 can run on lightweight embedded systems (like a Raspberry Pi), doing active development, 3D visualization, and physics simulation requires a more capable machine. 

Here are the general minimum and recommended system requirements for a smooth ROS 2 experience.

## 🖥️ Hardware Requirements

| Component | Minimum (Basic Node Execution) | Recommended (Development & Simulation) |
| :--- | :--- | :--- |
| **Processor (CPU)** | Dual-core processor (x86_64 or ARM64) | Quad-core (Intel i5/i7, AMD Ryzen) or better |
| **Memory (RAM)** | 4 GB | 8 GB to 16+ GB (Crucial for Gazebo) |
| **Storage** | 10 GB free space (SSD preferred) | 30+ GB free space (NVMe/SSD strongly recommended) |
| **Graphics (GPU)** | Integrated Graphics | Dedicated GPU (NVIDIA preferred for Gazebo/CUDA) |
| **Network** | Basic Wi-Fi or Ethernet | Network router that supports **UDP Multicast** (Required for DDS peer-to-peer discovery) |

> **Note on Architecture:** ROS 2 natively supports standard `x86_64` (typical PC/laptop architecture) as well as `ARM64` (aarch64), making it fully compatible with single-board computers like the **Raspberry Pi 4 / 5** and **NVIDIA Jetson** series.

## 🐧 Supported Operating Systems (Tier 1)

ROS 2 targets specific operating system releases for each of its distributions. To get "Tier 1" support (meaning binary packages are provided and fully tested by the developers), you should use the following OS versions:

### For ROS 2 Humble Hawksbill (LTS)
* **Ubuntu Linux 22.04 LTS** (Jammy Jellyfish) - *Primary platform*
* **Windows 10 / 11** (Visual Studio 2019)
* **RHEL 9** (Red Hat Enterprise Linux)
* *macOS is supported natively, but is considered Tier 3 (must be built from source).*

### For ROS 2 Jazzy Jalisco (LTS)
* **Ubuntu Linux 24.04 LTS** (Noble Numbat) - *Primary platform*
* **Windows 10 / 11** 
* **RHEL 9**

*(Always check the specific target OS for the ROS 2 distribution you intend to install, as installing ROS 2 Humble on Ubuntu 24.04, for example, is not natively supported without containers).*

## 📦 Software & Dependency Requirements

If you are developing your own packages or building ROS 2 from source, your system will need to support the following modern programming standards:

* **Python:** Python 3.8+ (Python 3.10+ recommended for newer distros)
* **C++:** A compiler that supports **C++17** (or C++20 for newer distros like Jazzy). E.g., GCC 11+ or Clang.
* **Build Tools:** CMake and Colcon (ROS 2's default build system).
* **Middleware:** Fast DDS or Cyclone DDS (installed automatically with ROS 2 desktop packages).

## 🚀 Virtual Machines & Containers (Alternative)
If your primary machine does not run a supported OS (e.g., you are on a Mac or an incompatible version of Windows/Linux), you can run ROS 2 using:
* **Docker:** Official `osrf/ros` Docker images are available and are highly recommended.
* **WSL 2 (Windows Subsystem for Linux):** You can install Ubuntu 22.04/24.04 via WSL 2 on Windows and run ROS 2 seamlessly, including GUI tools like RViz.
* **VirtualBox / VMware:** Note that physics simulations (Gazebo) will run very slowly in standard VMs without direct GPU pass-through.