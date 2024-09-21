# Jetson-Nano-Yolo-v5

> **Note:** This project is currently a work in progress as I continue to learn and develop it. Until this note is removed, all data below or within this repository should be considered incomplete and not intended for use.

Installing YOLOv5 on Jetson Nano involves several steps including setting up a Python environment and installing necessary dependencies. I'll guide you through everything from the beginning.

### 1. **Preparing Jetson Nano**

#### **Update and Upgrade System Packages**
Open the terminal on Jetson Nano and run:
```bash
sudo apt update
sudo apt upgrade
```
To ensure your Jetson Nano is updated and that you have enough space for installing the required libraries, follow these steps:

#### **Check if Jetson Nano is Updated**
#### **Verify JetPack Version**
```bash
dpkg-query --show nvidia-jetpack
```
The output should show the installed JetPack version, such as:
```
nvidia-jetpack 4.6
```
#### **Enable Swap Memory (Optional but Recommended)**
```bash
sudo fallocate -l 4G /mnt/4GB.swap
sudo chmod 600 /mnt/4GB.swap
sudo mkswap /mnt/4GB.swap
sudo swapon /mnt/4GB.swap
```
To make this permanent, add it to `/etc/fstab`:
```bash
sudo bash -c 'echo "/mnt/4GB.swap swap swap defaults 0 0" >> /etc/fstab'
```

### 2. **Install Dependencies**
#### **Install Python3 and Pip**
Verify Python is installed (Jetson Nano comes with Python 3.6+):
```bash
python3 --version
```
If Python3 is installed, install pip:
```bash
sudo apt install python3-pip
```

#### **Install Required Packages**
Install common libraries required by YOLOv5:
```bash
sudo apt install git wget curl
sudo apt-get install libopencv-dev python3-opencv
sudo apt-get install python3-matplotlib
sudo apt-get install python3-numpy python3-pillow
sudo apt-get install libatlas-base-dev gfortran
sudo apt-get install python3-scipy
```
