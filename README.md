# Jetson-Nano-Yolo-v5-SETUP
<h1 align="center">
    <img src="https://readme-typing-svg.herokuapp.com/?font=Righteous&size=35&center=true&vCenter=true&width=700&height=100&duration=4000&lines=Yolov5+Setup+on+Jetson+Nano+🔌;" />
</h1>
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
** Install pip**
Update Package List: First, make sure your package list is updated.

```bash
sudo apt update
```
Install pip: You can install pip for Python 3 using the following command:

```bash
sudo apt install python3-pip
```
Verify Installation: After the installation, you can verify that pip is installed correctly by checking its version:

```bash
pip3 --version
```

### 4.**Create a Python 3.8 Virtual Environment**
**Open Terminal**
Make sure you're in your root folder.
**Create the Virtual Environment**
```bash
vi ~/.bashrc
```
**Enter Insert Mode**
Press `i` to enter insert mode.
**Edit `.bashrc`**: Open your `.bashrc` file for editing at the end:
```bash
nano ~/.bashrc
```
**Add the Activation Command**: Scroll to the end of the file and add the following line:
```bash
source ~/techarcanist/bin/activate
```
**Save and Exit**
Press `Esc`, then type `:wq` and hit `Enter` to save and exit.
**Apply Changes**
Run:
```bash
source ~/.bashrc
```
### 5. **Installing Pytorch and Torchvision**
**Uninstall any existing torch and torchvision**
```bash
pip uninstall torch
pip uninstall torchvision
```
**First Install these**
It looks like there are several errors occurring during the installation process of `torch` and `torchvision`, specifically related to the dependencies for Pillow and NumPy. Here’s a breakdown of the issues and how to address them:
```bash
sudo apt-get install libjpeg-dev zlib1g-dev

python3.8 -m pip install cython

python3.8 -m pip install wheel

pip3 install numpy --upgrade --no-build-isolation

pip3 install cython

pip install --upgrade pip

pip install numpy --no-build-isolation

pip install --upgrade setuptools wheel

sudo apt install libopenmpi-dev

sudo apt install libomp5

sudo apt install mlocate

sudo updatedb

sudo apt install libopenblas-base

locate libopenblas.so

sudo apt update
```
**Download these two Python 3.8 compiled torch 1.11.0 and the matching torchvision 0.12.0 wheels specifically for the Jetson nano.**
[Download](https://drive.google.com/drive/folders/16_O-2jODtNIrFGr5IJP-5sYP6MWGYazX?usp=drive_link) 
**Move to that directory where the file has downloaded, in my case it was at Downloads**
```bash
cd ~/Downloads
```
**Install the Packages**
```bash
python -m pip install torch-*.whl torchvision-*.whl
```
**Verify the Installation**
Enter the Python shell:
```bash
python
```
**Import the `torch` package**
```python
import torch
```
**Check if the CUDA GPU is recognized**
```python
print(torch.cuda.device_count())
```
If it returns `1`, everything has been installed correctly.

### 6. **Enable Swap Memory (Optional but Recommended)**
```bash
sudo fallocate -l 4G /mnt/4GB.swap
sudo chmod 600 /mnt/4GB.swap
sudo mkswap /mnt/4GB.swap
sudo swapon /mnt/4GB.swap
```
**To make this permanent, add it to `/etc/fstab`**
```bash
sudo bash -c 'echo "/mnt/4GB.swap swap swap defaults 0 0" >> /etc/fstab'
```
**Verify**
```bash
cat /etc/fstab
```
**Verify Swap is Active**:
```bash
sudo swapon --show
```
**Reboot (Optional)**:
```bash
sudo reboot
```
**Verify Swap again**:
```bash
sudo swapon --show
```

### 7. Install Required Packages
**Clone the YOLOv5 Repository**
```bash
git clone https://github.com/ultralytics/yolov5.git
cd yolov5
```
**Install Dependencies**:
```bash
pip install -r requirements.txt
```

### 8. **Run YOLOv5**
```bash
python detect.py --source data/images/bus.jpg
```
![bus](https://github.com/user-attachments/assets/aba2cacc-5077-4cf2-931f-ae5d4f3acfd0)

### 9. **Optional: Enable GPU for YOLOv5**
```bash
python detect.py --source data/images/bus.jpg --weights yolov5s.pt --device 0
```
![bus](https://github.com/user-attachments/assets/f0d39ec8-1df1-4483-99c8-f2ee99e31fb3)

### 10. **Testing on Jetson Nano Camera**
You can test the live camera feed using:
```bash
python detect.py --source 0 --weights yolov5s.pt --device 0
```
This will use the onboard camera or an attached USB camera.

https://github.com/user-attachments/assets/79ff49f7-e352-48a8-8578-ad882dbd28a8

### 11. **Deactivate the Virtual Environment**
When you're done, you can deactivate the virtual environment:
```bash
deactivate
```
<h1 align="center">
    <img src="https://readme-typing-svg.herokuapp.com/?font=Righteous&size=35&center=true&vCenter=true&width=500&height=70&duration=4000&lines=Thanks+for+Visiting!+👋;" />
</h1>
