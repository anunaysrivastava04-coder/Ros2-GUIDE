# 🖥️ Ubuntu Virtual Machine (VM) Installation Guide

Running Ubuntu in a Virtual Machine is a great way to use Linux and ROS 2 without altering your host operating system (Windows or macOS). 

> ⚠️ **Note for ROS Users:** While VMs are excellent for basic ROS 2 programming and terminal tools, 3D physics simulations (like Gazebo) may run slowly because VMs do not always have direct access to your dedicated graphics card (GPU).

## 📥 Step 1: Download Virtual Machine Software

First, you need a hypervisor program to run the virtual machine.

*   **For Windows & Intel Macs: Oracle VirtualBox (Recommended & Free)**
    *   VirtualBox is open-source and widely used for Ubuntu VMs.
    *   🔗 [Download VirtualBox here](https://www.virtualbox.org/wiki/Downloads) *(Select "Windows hosts" or "macOS / Intel hosts")*
*   **For Apple Silicon Macs (M1/M2/M3): UTM (Recommended & Free)**
    *   VirtualBox does not work on Apple Silicon. You must use virtualization software built for ARM architecture.
    *   🔗 [Download UTM here](https://mac.getutm.app/)

## 💿 Step 2: Download the Ubuntu ISO

You will need the Ubuntu disk image (ISO) to install inside your VM. Choose the version based on your needs (e.g., ROS 2 version):

*   **For ROS 2 Jazzy (Ubuntu 24.04 LTS):**
    *   🔗 [Download Ubuntu 24.04 (Noble Numbat)](https://releases.ubuntu.com/24.04/) *(Click "64-bit PC (AMD64) desktop image")*
*   **For ROS 2 Humble (Ubuntu 22.04 LTS):**
    *   🔗 [Download Ubuntu 22.04 (Jammy Jellyfish)](https://releases.ubuntu.com/22.04/) *(Click "64-bit PC (AMD64) desktop image")*

*(Mac M1/M2/M3 Users: You must download the **ARM64** version of Ubuntu to use with UTM).*

## ⚙️ Step 3: Create and Configure the VM (VirtualBox)

1. Open **VirtualBox** and click the **"New"** button.
2. **Name and OS:** 
   * Name: `Ubuntu ROS2` (or whatever you prefer)
   * ISO Image: Select the Ubuntu `.iso` file you downloaded in Step 2.
   * *Check the box that says "Skip Unattended Installation" so you can configure it manually.*
3. **Hardware (Crucial for ROS):**
   * **Base Memory (RAM):** Allocate at least **4096 MB (4GB)**, but **8192 MB (8GB)** is highly recommended.
   * **Processors (CPU):** Allocate at least **2 CPUs**, but **4 CPUs** is recommended. *(Do not go past the green zone on the slider).*
4. **Virtual Hard disk:**
   * Select "Create a Virtual Hard Disk Now".
   * Allocate at least **30 GB** (50 GB+ is better if you plan to install full ROS 2 desktop and build packages).
5. Click **Finish**.

## 🚀 Step 4: Install Ubuntu

1. Select your new VM in VirtualBox and click **"Start"** (the green arrow).
2. The VM will boot up the Ubuntu ISO. When the GRUB menu appears, select **"Try or Install Ubuntu"** and press Enter.
3. Follow the standard Ubuntu installation wizard:
   * Select your language and click **Install Ubuntu**.
   * Choose **"Normal installation"** and check "Download updates while installing".
   * For Installation Type, select **"Erase disk and install Ubuntu"**. *(Don't worry, this only erases the virtual hard drive you created, NOT your actual computer's hard drive!)*
   * Set your timezone, name, username, and a memorable password (needed for `sudo`).
4. Wait for the installation to finish and click **Restart Now** when prompted. 
5. VirtualBox should automatically eject the ISO. Press Enter if the screen asks you to remove the installation medium.

## 🛠️ Step 5: Install VirtualBox Guest Additions (Highly Recommended)

Once logged into your new Ubuntu VM, the screen resolution might be tiny, and copy/pasting from Windows won't work. You must install Guest Additions to fix this:

1. Inside the running Ubuntu VM, open a terminal (`Ctrl` + `Alt` + `T`).
2. Run these commands to update your system and install build tools:
   ```bash
   sudo apt update
   sudo apt upgrade -y
   sudo apt install build-essential dkms linux-headers-$(uname -r) -y
   ```
3. In the top VirtualBox menu bar (on your host machine), click **Devices** -> **Insert Guest Additions CD image...**
4. A disk icon will appear on your Ubuntu desktop. Click it, run the software, and authorize it with your password.
5. Once the terminal says it is finished, restart your VM.
6. You can now resize the VM window to full screen, and enable Shared Clipboard by going to **Devices -> Shared Clipboard -> Bidirectional**.