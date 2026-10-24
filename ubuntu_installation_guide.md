# 🐧 Ubuntu Linux Installation Guide

If you are setting up a machine for ROS development, it is highly recommended to install a native Linux environment. This guide covers how to download and install Ubuntu, the official operating system supported by ROS 2.

## 📥 Step 1: Download the Ubuntu ISO

You will need to download an Ubuntu "ISO" file (a disc image) from the official Ubuntu website. 

Choose the version that matches the ROS 2 distribution you want to use:

*   **For ROS 2 Jazzy Jalisco:**
    *   Download **Ubuntu 24.04 LTS (Noble Numbat)**
    *   🔗 [Official Download Link](https://releases.ubuntu.com/24.04/) *(Click on "64-bit PC (AMD64) desktop image")*
*   **For ROS 2 Humble Hawksbill:**
    *   Download **Ubuntu 22.04 LTS (Jammy Jellyfish)**
    *   🔗 [Official Download Link](https://releases.ubuntu.com/22.04/) *(Click on "64-bit PC (AMD64) desktop image")*

## 💽 Step 2: Create a Bootable USB Drive

You cannot just copy the ISO file to a USB drive; you must "flash" it to make the USB bootable. You will need a USB flash drive with at least **8GB of space** (Note: all data on the USB drive will be erased).

**Recommended Flashing Tools:**
1.  **Rufus** (For Windows users): 
    *   🔗 [Download Rufus here](https://rufus.ie/)
2.  **BalenaEtcher** (For Windows, macOS, or Linux): 
    *   🔗 [Download BalenaEtcher here](https://etcher.balena.io/)

**How to flash:**
1. Insert your USB drive.
2. Open Rufus or BalenaEtcher.
3. Select your USB drive as the target.
4. Select the Ubuntu ISO file you downloaded as the source.
5. Click "Start" or "Flash" and wait for the process to finish.

## 💻 Step 3: Boot from the USB

1. Plug the flashed USB drive into the computer where you want to install Ubuntu.
2. Turn on (or restart) the computer.
3. Immediately press your computer's **Boot Menu key** repeatedly (usually `F12`, `F10`, `F8`, or `F2` depending on your PC manufacturer).
4. In the Boot Menu, select your USB flash drive (it might be labeled as "UEFI OS", "USB Disk", or your USB brand name).
5. You should see a black and white menu (the GRUB menu). Select **"Try or Install Ubuntu"**.

## ⚙️ Step 4: The Installation Process

Once Ubuntu boots from the USB, the graphical installer will appear. Follow these steps:

1.  **Welcome Screen:** Choose your language and click **Install Ubuntu**.
2.  **Keyboard Layout:** Select your preferred keyboard layout and test it.
3.  **Updates and Other Software:** 
    *   Check **"Normal installation"**.
    *   Check **"Download updates while installing Ubuntu"** (requires internet).
    *   Check **"Install third-party software for graphics and Wi-Fi hardware"** (Highly recommended, especially if you have an NVIDIA GPU for Gazebo simulations).
4.  **Installation Type (Crucial Step):**
    *   *Option A (Dedicated Machine):* Choose **"Erase disk and install Ubuntu"**. (⚠️ **WARNING:** This will delete everything on the computer, including Windows).
    *   *Option B (Dual Boot):* If you already have Windows and want to keep it, select **"Install Ubuntu alongside Windows"** (The installer will help you split your hard drive).
5.  **Location:** Select your time zone on the map.
6.  **Who are you?:** Create your username, computer name, and a strong password. (Remember this password; you will need it for `sudo` commands when installing ROS!).
7.  **Install:** Click continue and wait for the installation to finish. When prompted, remove the USB drive and restart the computer.

## 🚀 Step 5: Post-Installation Updates

Once you restart and log into your fresh Ubuntu desktop, it is a good idea to ensure all system packages are fully up to date before trying to install ROS.

Open a terminal (`Ctrl` + `Alt` + `T`) and run:

```bash
sudo apt update
sudo apt upgrade -y
```

You are now ready to install ROS 2!