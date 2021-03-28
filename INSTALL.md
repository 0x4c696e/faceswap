# Installing faceswap/安装faceswap
- [Installing faceswap](#installing-faceswap)安装faceswap
- [Prerequisites](#prerequisites)准备工作
  - [Hardware Requirements](#hardware-requirements)硬件要求
  - [Supported operating systems](#supported-operating-systems)支持的操作系统
- [Important before you proceed](#important-before-you-proceed)在继续前的重要事项
- [Linux and Windows Install Guide](#linux-and-windows-install-guide)LINUX和windows安装指导
  - [Installer](#installer)安装包
  - [Manual Install](#manual-install)手动安装
  - [Prerequisites](#prerequisites-1)准备
    - [Anaconda](#anaconda)
    - [Git](#git)
  - [Setup](#setup)设置
    - [Anaconda](#anaconda-1)
      - [Set up a virtual environment](#set-up-a-virtual-environment)设置一个虚拟环境
      - [Entering your virtual environment](#entering-your-virtual-environment)进入虚拟环境
    - [faceswap](#faceswap)
      - [Easy install](#easy-install)简易安装
      - [Manual install](#manual-install-1)手动安装
  - [Running faceswap](#running-faceswap)运行faceswap
  - [Create a desktop shortcut](#create-a-desktop-shortcut)创建桌面快捷方式
  - [Updating faceswap](#updating-faceswap)更新faceswap
- [General Install Guide](#general-install-guide)通用安装指导
  - [Installing dependencies](#installing-dependencies)安装依赖
    - [Git](#git-1)
    - [Python](#python)
    - [Virtual Environment](#virtual-environment)
  - [Getting the faceswap code](#getting-the-faceswap-code)获取faceswap代码
  - [Setup](#setup-1)设置
    - [About some of the options](#about-some-of-the-options)关于一些选项
  - [Run the project](#run-the-project)运行项目
  - [Notes](#notes)

# Prerequisites/准备工作
Machine learning essentially involves a ton of trial and error. You're letting a program try millions of different settings to land on an algorithm that sort of does what you want it to do. This process is really really slow unless you have the hardware required to speed this up. 

机器学习基本上需要成千上万次的训练和出错。你要让一个程序尝试一个你想要用来做什么的算法的几百万个不同的选项。这个过程真的会非常慢，除非你有要求的硬件来为这个过程加速。

The type of computations that the process does are well suited for graphics cards, rather than regular processors. **It is pretty much required that you run the training process on a desktop or server capable GPU.** Running this on your CPU means it can take weeks to train your model, compared to several hours on a GPU.

这个类型的计算需要不错的图形卡（显卡），而不是常规的CPU。这非常需要你在桌面平台或者好的服务器GPU上运行训练程序。运行在你的CPU上意味着它将花费数周的时间，而GPU相比之下只要花费几个小时。

## Hardware Requirements
**TL;DR: you need at least one of the following:/你至少需要以下的其中一个**

- **A powerful CPU/一个强大的CPU**
    - Laptop CPUs can often run the software, but will not be fast enough to train at reasonable speeds/笔记本的CPU可以运行软件，但对训练来说不能达到合理的速度
- **A powerful GPU/一个强大的GPU**
    - Currently, Nvidia GPUs are fully supported. and AMD graphics cards are partially supported through plaidML./目前，英伟达的GPU已经全面支持了，并且AMD的图形卡通过plaidML得到了部分支持。
    - If using an Nvidia GPU, then it needs to support at least CUDA Compute Capability 3.5. (Release 1.0 will work on Compute Capability 3.0)
      To see which version your GPU supports, consult this list: https://developer.nvidia.com/cuda-gpus /如果使用的是英伟达GPU，那么它需要支持至少CUDA计算能力3.5
      Desktop cards later than the 7xx series are most likely supported./在7代以后的系列桌面显卡大多数都已经支持了。
- **A lot of patience/大量的耐心**

## Supported operating systems
- **Windows 10**
  Windows 7 and 8 might work. Your mileage may vary. Windows has an installer which will set up everything you need. See: https://github.com/deepfakes/faceswap/releases /windows7和8可能可以工作。你的安装时间可能因机器而异。widnows有一个将会设置好你需要的一切的安装程序。请看 https://github.com/deepfakes/faceswap/releases
- **Linux**
  Most Ubuntu/Debian or CentOS based Linux distributions will work.
- **macOS**
  GPU support on macOS is limited due to lack of drivers/libraries from Nvidia.
- All operating systems must be 64-bit for Tensorflow to run.

Alternatively, there is a docker image that is based on Debian.

# Important before you proceed/在你继续之前的重要事项
**In its current iteration, the project relies heavily on the use of the command line, although a gui is available. if you are unfamiliar with command line tools, you may have difficulty setting up the environment and should perhaps not attempt any of the steps described in this guide.** This guide assumes you have intermediate knowledge of the command line. 

在当前的阶段，这个项目重度依赖命令行的使用，尽管提供了图形界面。如果你对命令行不熟悉的话，可能设置环境会困难一些并且应该不要去尝试在这个指导中描述的任意步骤。这个指导假设你已经有了中等的命令行知识。

The developers are also not responsible for any damage you might cause to your own computer.

开发者也不会对你可能会对你电脑造成的任何损害负责。

# Linux and Windows Install Guide/Linux和windows安装指导

## Installer/安装包
Windows and Linux now both have an installer which installs everything for you and creates a desktop shortcut to launch straight into the GUI. You can download the installer from https://github.com/deepfakes/faceswap/releases.

windows和linux都提供了一个安装全部你要创建的安装包并且创建了一个桌面快捷方式来直接启动GUI图形界面。你可以从 https://github.com/deepfakes/faceswap/releases中下载对应的安装包。

If you have issues with the installer then read on for the more manual way to install faceswap on Windows.

如果你在安装过程中出现了问题，请接着阅读在windows上手动安装faceswap。

## Manual Install/手动安装

Setting up faceswap can seem a little intimidating to new users, but it isn't that complicated, although a little time consuming. It is recommended to use Linux where possible as Windows will hog about 20% of your GPU Memory, making faceswap run a little slower, however using Windows is perfectly fine and 100% supported.

设置faceswap似乎对新用户来说有一点恐惧，但其实不是那么复杂，虽然会多花费一些时间，推荐使用linux，因为可能比windows节省20%的GPU内存，后者让faceswap运行的更慢，然而使用windows也完全可以并且100%支持。

## Prerequisites/准备工作

### Anaconda
Download and install the latest Python 3 Anaconda from: https://www.anaconda.com/download/. Unless you know what you are doing, you can leave all the options at default.

下载并安装最新的anaconda。安装时你可以让所有选项都默认，除非你知道你在做什么，

### Git
Download and install Git for Windows: https://git-scm.com/download/win. Unless you know what you are doing, you can leave all the options at default.

下载并安装git。安装时你可以让所有选项都默认，除非你知道你在做什么，

## Setup/设置
Reboot your PC, so that everything you have just installed gets registered.

重启你的电脑，为了你刚才安装的一切都已经注册。

### Anaconda
#### Set up a virtual environment/设置虚拟环境
- Open up Anaconda Navigator/打开anaconda navigator
- Select "Environments" on the left hand side/在左手边选择“environments‘
- Select "Create" at the bottom/在下面选择“create”
- In the pop up:/在弹出窗口
    - Give it the name: faceswap/给它起个名字
    - **IMPORTANT**: Select python version 3.8/选择python版本3.8
    - Hit "Create" (NB: This may take a while as it will need to download Python)/点击创建
![Anaconda virtual env setup](https://i.imgur.com/CLIDDfa.png)

#### Entering your virtual environment/进入你的虚拟环境
To enter the virtual environment:/为了进入虚拟环境
- # Open up Anaconda Navigator/打开anaconda navigator
- Select "Environments" on the left hand side/在左手边选择“environments”
- Hit the ">" arrow next to your faceswap environment and select "Open Terminal"/点击在你的faceswap环境旁的”>“箭头然后选择”open terminal“
![Anaconda enter virtual env](https://i.imgur.com/rKSq2Pd.png)

### faceswap
- If you are not already in your virtual environment follow [these steps](#entering-your-virtual-environment)/如果你没有设置虚拟环境请跟随[these steps](#entering-your-virtual-environment)这些步骤
- Get the faceswap repo by typing: `git clone --depth 1 https://github.com/deepfakes/faceswap.git`/通过键入”git clone --depth 1 https://github.com/deepfakes/faceswap.git“ 来获取faceswap的仓库
- Enter the faceswap folder: `cd faceswap`/进入faceswap的文件夹”cd faceswap“

#### Easy install/简易安装方法
- Enter the command `python setup.py` and follow the prompts:/输入命令”python setup.py“然后跟随提示
- If you have issues/errors follow the Manual install steps below./如果产生了问题或错误请跟随下面的手动安装步骤

#### Manual install/手动安装
Do not follow these steps if the Easy Install above completed succesfully./如果上面的简易安装成功安装了就不要跟随这些步骤了
If you are using an Nvidia card make sure you have the correct versions of Cuda/cuDNN installed for the required version of Tensorflow
- Install tkinter (required for the GUI) by typing: `conda install tk`
- Install requirements:
  - For Nvidia GPU users: `pip install -r requirements_nvidia.txt`
  - For AMD GPU users: `pip install -r requirements_amd.txt`
  - For CPU users: `pip install -r requirements_cpu.txt`

## Running faceswap
- If you are not already in your virtual environment follow [these steps](#entering-your-virtual-environment)
- Enter the faceswap folder: `cd faceswap`
- Enter the following to see the list of commands: `python faceswap.py -h` or enter `python faceswap.py gui` to launch the GUI

## Create a desktop shortcut
A desktop shortcut can be added to easily launch straight into the faceswap GUI:

- Open Notepad
- Paste the following:
```
%USERPROFILE%\Anaconda3\envs\faceswap\python.exe %USERPROFILE%/faceswap/faceswap.py gui
```
- Save the file to your desktop as "faceswap.bat"

## Updating faceswap
It's good to keep faceswap up to date as new features are added and bugs are fixed. To do so:
- If using the GUI you can go to the Help menu and select "Check for Updates...". If updates are available go to the Help menu and select "Update Faceswap". Restart Faceswap to complete the update.
- If you are not already in your virtual environment follow [these steps](#entering-your-virtual-environment)
- Enter the faceswap folder: `cd faceswap`
- Enter the following `git pull --all`
- Once the latest version has downloaded, make sure your dependencies are up to date. There is a script to help with this: `python update_deps.py`

# General Install Guide
## Installing dependencies
### Git
Git is required for obtaining the code and keeping your codebase up to date.
Obtain git for your distribution from the [git website](https://git-scm.com/downloads).

### Python
The recommended install method is to use a Conda3 Environment as this will handle the installation of Nvidia's CUDA and cuDNN straight into your Conda Environment. This is by far the easiest and most reliable way to setup the project.
  - MiniConda3 is recommended: [MiniConda3](https://docs.conda.io/en/latest/miniconda.html)

Alternatively you can install Python (>= 3.7-3.8 64-bit) for your distribution (links below.) If you go down this route and are using an Nvidia GPU you should install CUDA (https://developer.nvidia.com/cuda-zone) and cuDNN (https://developer.nvidia.com/cudnn). for your system. If you do not plan to build Tensorflow yourself, make sure you install the correct Cuda and cuDNN package for the currently installed version of Tensorflow (Current release: Tensorflow 2.2. Release v1.0: Tensorflow 1.15). You can check for the compatible versions here: (https://www.tensorflow.org/install/source#gpu).
  - Python distributions:
    - apt/yum install python3 (Linux)
    - [Installer](https://www.python.org/downloads/release/python-368/) (Windows)
    - [brew](https://brew.sh/) install python3 (macOS)

### Virtual Environment
  It is highly recommended that you setup faceswap inside a virtual environment. In fact we will not generally support installations that are not within a virtual environment as troubleshooting package conflicts can be next to impossible.

  If using Conda3 then setting up virtual environments is relatively straight forward. More information can be found at [Conda Docs](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)

  If using a default Python distribution then [virtualenv](https://github.com/pypa/virtualenv) and [virtualenvwrapper](https://virtualenvwrapper.readthedocs.io) may help when you are not using docker.


## Getting the faceswap code
It is recommended to clone the repo with git instead of downloading the code from http://github.com/deepfakes/faceswap and extracting it as this will make it far easier to get the latest code (which can be done from the GUI). To clone a repo you can either use the Git GUI for your distribution or open up a command prompt, enter the folder where you want to store faceswap and enter:
```bash
git clone https://github.com/deepfakes/faceswap.git
```


## Setup
Enter your virtual environment and then enter the folder that faceswap has been downloaded to and run:
```bash
python setup.py
```
If setup fails for any reason you can still manually install the packages listed within requirements.txt

### About some of the options
   - CUDA: For acceleration. Requires a good nVidia Graphics Card (which supports CUDA inside)
   - Docker: Provide a ready-made image. Hide trivial details. Get you straight to the project.
   - nVidia-Docker: Access to the nVidia GPU on host machine from inside container.

CUDA with Docker in 20 minutes.
```
INFO    The tool provides tips for installation
        and installs required python packages
INFO    Setup in Linux 4.14.39-1-MANJARO
INFO    Installed Python: 3.7.5 64bit
INFO    Installed PIP: 10.0.1
Enable  Docker? [Y/n] 
INFO    Docker Enabled
Enable  CUDA? [Y/n] 
INFO    CUDA Enabled
INFO    1. Install Docker
        https://www.docker.com/community-edition
        
        1. Install Nvidia-Docker & Restart Docker Service
        https://github.com/NVIDIA/nvidia-docker
        
        1. Build Docker Image For faceswap
        docker build -t deepfakes-gpu -f Dockerfile.gpu .
        
        1. Mount faceswap volume and Run it
        # without gui. tools.py gui not working.
        nvidia-docker run --rm -it -p 8888:8888 \
            --hostname faceswap-gpu --name faceswap-gpu \
            -v /opt/faceswap:/srv \
            deepfakes-gpu
        
        # with gui. tools.py gui working.
        ## enable local access to X11 server
        xhost +local:
        ## enable nvidia device if working under bumblebee
        echo ON > /proc/acpi/bbswitch
        ## create container 
        nvidia-docker run -p 8888:8888 \
            --hostname faceswap-gpu --name faceswap-gpu \
            -v /opt/faceswap:/srv \
            -v /tmp/.X11-unix:/tmp/.X11-unix \
            -e DISPLAY=unix$DISPLAY \
            -e AUDIO_GID=`getent group audio | cut -d: -f3` \
            -e VIDEO_GID=`getent group video | cut -d: -f3` \
            -e GID=`id -g` \
            -e UID=`id -u` \
            deepfakes-gpu
        
        1. Open a new terminal to interact with the project
        docker exec -it deepfakes-gpu /bin/bash
	# Launch deepfakes gui (Answer 3 for NVIDIA at the prompt)
	python3.8 /srv/faceswap.py gui
```

A successful setup log, without docker.
```
INFO    The tool provides tips for installation
        and installs required python packages
INFO    Setup in Linux 4.14.39-1-MANJARO
INFO    Installed Python: 3.7.5 64bit
INFO    Installed PIP: 10.0.1
Enable  Docker? [Y/n] n
INFO    Docker Disabled
Enable  CUDA? [Y/n] 
INFO    CUDA Enabled
INFO    CUDA version: 9.1
INFO    cuDNN version: 7
WARNING Tensorflow has no official prebuild for CUDA 9.1 currently.
        To continue, You have to build your own tensorflow-gpu.
        Help: https://www.tensorflow.org/install/install_sources
Are System Dependencies met? [y/N] y
INFO    Installing Missing Python Packages...
INFO    Installing tensorflow-gpu
INFO    Installing pathlib==1.0.1
......
INFO    Installing tqdm
INFO    Installing matplotlib
INFO    All python3 dependencies are met.
        You are good to go.
```

## Run the project
Once all these requirements are installed, you can attempt to run the faceswap tools. Use the `-h` or `--help` options for a list of options.

```bash
python faceswap.py -h
```

or run with `gui` to launch the GUI
```bash
python faceswap.py gui
```


Proceed to [../blob/master/USAGE.md](USAGE.md)

## Notes
This guide is far from complete. Functionality may change over time, and new dependencies are added and removed as time goes on. 

If you are experiencing issues, please raise them in the [faceswap Forum](https://faceswap.dev/forum) instead of the main repo. Usage questions raised in the issues within this repo are liable to be closed without response.
