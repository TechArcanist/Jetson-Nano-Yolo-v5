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

### 3. **Create a Python Virtual Environment**
Create a virtual environment to isolate the YOLOv5 installation:
```bash
sudo apt-get install python3-venv
python3 -m venv yolov5-env
source yolov5-env/bin/activate
```

### 4. **Install PyTorch for Jetson Nano**
YOLOv5 relies on PyTorch, but you need to install a version compatible with the Jetson Nano.

#### **Install PyTorch and TorchVision**
Download and install PyTorch for Jetson Nano from the official NVIDIA sources:
```bash
pip install --upgrade pip
sudo apt-get install python3-pytest
pip install torch torchvision -f https://nvidia.box.com/shared/static/oh0jp5w4lf17a3zwi2c74mr4x2l3lg53.whl
```
Here’s a detailed step-by-step guide to upgrade Python and install YOLOv5 on your Jetson Nano:

### 5. **Check Current Python Version**
#### **Open a terminal and check your current Python version**
```bash
python3 --version
```
If it shows 3.6.9, you need to upgrade.

#### Upgrade Python
#### **Update Package List**:
   ```bash
   sudo apt update
   ```
#### **Install Prerequisites**:
   ```bash
   sudo apt install software-properties-common
   ```
#### **Add the Deadsnakes PPA** (to get the latest Python versions):
   ```bash
   sudo add-apt-repository ppa:deadsnakes/ppa
   ```
#### **Install a Newer Python Version** (e.g., Python 3.8):
   ```bash
   sudo apt update
   sudo apt install python3.8 python3.8-venv python3.8-dev
   ```
#### Verify Installation
Check if the new version is installed:
```bash
python3.8 --version
```
### 6. **Create a Virtual Environment**
#### **Create a New Virtual Environment**
   ```bash
   python3.8 -m venv yolov5-env
   ```
#### **Activate the Virtual Environment**
   ```bash
   source yolov5-env/bin/activate
   ```
### 7. **Upgrade `pip`**
Upgrade `pip` to the latest version:
```bash
pip install --upgrade pip
```
### 8. Install Required Packages
#### **Clone the YOLOv5 Repository**
   ```bash
   git clone https://github.com/ultralytics/yolov5.git
   cd yolov5
   ```
#### **Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   ```
### 9. Run YOLOv5
You can now run YOLOv5 commands. For example, to test with a sample image:
```bash
python detect.py --source data/images/bus.jpg
```
![bus](https://github.com/user-attachments/assets/aba2cacc-5077-4cf2-931f-ae5d4f3acfd0)

### Step 8: Deactivate the Virtual Environment
When you're done, you can deactivate the virtual environment:
```bash
deactivate
```

