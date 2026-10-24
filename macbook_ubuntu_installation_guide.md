# 🍏 Ubuntu Installation Guide for MacBooks

Installing Ubuntu on a MacBook depends entirely on the type of processor your Mac has. 

⚠️ **Crucial Context:** Modern Macs (2020 and newer) use **Apple Silicon (M1, M2, M3, M4)**. These use an `ARM64` architecture, meaning standard `x86_64` PC software and native USB dual-booting will not work easily. The recommended and safest way to run Ubuntu on any modern Mac is via Virtualization.

---

## 🛠️ Method 1: UTM (Free & Recommended for Apple Silicon)

UTM is a fantastic, free, open-source virtualization application designed specifically for iOS and macOS. It allows you to run the ARM version of Ubuntu at near-native speeds.

### 📥 Step 1: Download Required Files
1. **Download UTM:**
   * 🔗 [Download UTM for Mac](https://mac.getutm.app/)
2. **Download Ubuntu ARM64 ISO:** (You MUST download the ARM version, not the standard AMD64 desktop version).
   * 🔗 [Ubuntu 24.04 ARM64 (For ROS 2 Jazzy)](https://cdimage.ubuntu.com/jammy/daily-live/current/) *(Look for "64-bit ARM (ARMv8/AArch64) desktop image")*
   * 🔗 [Ubuntu 22.04 ARM64 (For ROS 2 Humble)](https://cdimage.ubuntu.com/jammy/daily-live/current/) *(Search the Ubuntu downloads for ARM64)*

### ⚙️ Step 2: Create the VM in UTM
1. Open UTM and click the **"+"** button to create a new virtual machine.
2. Select **"Virtualize"** (this gives you full speed on M-series chips).
3. Select **"Linux"**.
4. In the "Boot ISO Image" box, click "Browse" and select the Ubuntu ARM64 `.iso` file you downloaded.
5. **Hardware:** Allocate at least **4096 MB (4 GB)** of RAM and at least **2 CPU cores**.
6. **Storage:** Allocate at least **30 GB** for your ROS development environment.
7. Save and click the big "Play" button to start the VM. Follow the standard Ubuntu installation prompts.

---

## 🏎️ Method 2: Parallels Desktop (Easiest, but Paid)

If you are willing to pay for a premium experience, Parallels Desktop is the absolute easiest way to run Ubuntu on a Mac. It handles downloading and installing Ubuntu automatically and supports shared folders and clipboards instantly.

1. **Download Parallels:**
   * 🔗 [Download Parallels Desktop](https://www.parallels.com/) *(Free trial available)*
2. Open Parallels and click **File > New**.
3. Under "Free Systems", select **Ubuntu Linux** and click **Continue**.
4. Parallels will automatically download the correct ARM64 version of Ubuntu and install it for you in just a few clicks.

---

## 💻 Method 3: Canonical Multipass (Best for CLI/Headless)

If you don't need a graphical user interface (no RViz or Gazebo) and just want an Ubuntu terminal to run basic ROS 2 code, Canonical (the makers of Ubuntu) provides a tool called Multipass. It spins up an Ubuntu environment in seconds.

1. **Download Multipass:**
   * 🔗 [Download Multipass](https://multipass.run/)
2. Open your Mac Terminal and run:
   ```bash
   multipass launch 22.04 -n ros-ubuntu
   ```
3. To open a terminal inside your new Ubuntu environment, simply run:
   ```bash
   multipass shell ros-ubuntu
   ```

---

## 💾 Method 4: Native Dual-Boot (Intel Macs ONLY - Pre 2020)

*Note: Do not attempt this on M1/M2/M3 Macs.*

If you have an older Intel-based Mac, you can install Ubuntu directly onto the hard drive just like a normal PC.

1. **Download the Standard ISO:** 🔗 [Ubuntu Standard AMD64 ISO](https://ubuntu.com/download/desktop)
2. **Flash to USB:** Use 🔗 [BalenaEtcher](https://etcher.balena.io/) to flash the ISO to a USB flash drive (8GB+).
3. **Partition your Mac:** Open "Disk Utility" on macOS, select your main drive, click "Partition", and create a new partition (at least 50GB) formatted as MS-DOS (FAT).
4. **Boot from USB:** Turn off the Mac. Turn it back on while holding down the **Option (⌥)** key. Select "EFI Boot" (your USB drive).
5. Follow the Ubuntu installer, and when it asks for the Installation Type, choose **"Install Ubuntu alongside macOS"**.