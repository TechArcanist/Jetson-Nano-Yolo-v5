# Jetson-Nano-Yolo-v5-SETUP
> **Stuck? Here’s the Ultimate Guide to Setting Up YOLOv5 on Jetson Nano with GPU Acceleration!**

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
**If you don’t receive this output, please follow the steps below:**
```bash
sudo apt remove nvidia-container-csv-tensorrt
sudo apt install nvidia-container-csv-tensorrt=8.2
sudo apt install nvidia-jetpack
```
The output should show the installed JetPack version, such as:
```
nvidia-jetpack 4.6
```
### 2. **Check CUDA and cuDNN Versions: To verify the installed versions of CUDA and cuDNN**
```bash
nvcc --version
```
**If there any kind of error, please follow the steps below:** 
Check if CUDA is installed:
```bash
ls /usr/local | grep cuda
```
You should see directories like cuda-<version> if it’s installed.Now follow the steps below:
### Run:
```bash
vi ~/.bashrc
```
### Enter Insert Mode
Press `i` to enter insert mode.
### Add CUDA to PATH
Add the following lines at the end of the file:
```bash
export PATH=/usr/local/cuda-10.2/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda-10.2/lib64:$LD_LIBRARY_PATH
```
### Save and Exit
Press `Esc`, then type `:wq` and hit `Enter` to save and exit.
### Apply Changes
Run:
```bash
source ~/.bashrc
```
### Check nvcc Version Again
Now try:
```bash
nvcc --version
```
### 3. **Install Python 3.8**
```bash
sudo apt-get install python3.8 python3.8-dev python3.8-distutils python3.8-venv
```
**Now you have two python versions so you need to do some changes:**
**Open the `.bashrc` file:**
```bash
vi ~/.bashrc
```
**Enter Insert Mode**
Press `i` to enter insert mode.
**Add the aliases at the end of the file:**
```bash
alias python="python3.8"
alias python3="python3.8"
alias pip="python3.8 -m pip"
alias pip3="python3.8 -m pip"
```
**Save and Exit**
Press `Esc`, then type `:wq` and hit `Enter` to save and exit.
**Apply Changes**
Run:
```bash
source ~/.bashrc
```
**Verify that the aliases are working:**
```bash
python --version
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

### 9. Deactivate the Virtual Environment
When you're done, you can deactivate the virtual environment:
```bash
deactivate
```

