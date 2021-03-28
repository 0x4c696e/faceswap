# deepfakes_faceswap
<p align="center">
  <a href="https://faceswap.dev"><img src="https://i.imgur.com/zHvjHnb.png"></img></a>
<br />FaceSwap is a tool that utilizes deep learning to recognize and swap faces in pictures and videos.
</p>
<p align="center">
<img src = "https://i.imgur.com/nWHFLDf.jpg"></img>
</p>

<p align="center">
<a href="https://www.patreon.com/bePatron?u=23238350"><img src="https://c5.patreon.com/external/logo/become_a_patron_button.png"></img></a>
&nbsp;&nbsp;&nbsp;&nbsp;<a href="https://discord.gg/FC54sYg"><img src="https://i.imgur.com/gIpztkv.png"></img></a></p>
<p align="center">
  <a href="https://www.youtube.com/watch?v=r1jng79a5xc"><img src="https://img.youtube.com/vi/r1jng79a5xc/0.jpg"></img></a>
<br />Jennifer Lawrence/Steve Buscemi FaceSwap using the Villain model
</p>

[![Build Status](https://travis-ci.org/deepfakes/faceswap.svg?branch=master)](https://travis-ci.org/deepfakes/faceswap) [![Documentation Status](https://readthedocs.org/projects/faceswap/badge/?version=latest)](https://faceswap.readthedocs.io/en/latest/?badge=latest)

Make sure you check out [INSTALL.md](INSTALL.md) before getting started.

在开始之前请确保你查看过[INSTALL.md](INSTALL.md)安装文档。

- [deepfakes_faceswap](#deepfakesfaceswap)
- [Manifesto](#manifesto)/声明
  - [FaceSwap has ethical uses.](#faceswap-has-ethical-uses)
- [How To setup and run the project](#how-to-setup-and-run-the-project)/怎么设置并运行项目
- [Overview](#overview)/总览
  - [Extract](#extract)/提取
  - [Train](#train)/训练
  - [Convert](#convert)/转换
  - [GUI](#gui)/图形界面
- [General notes:](#general-notes)/总体提示
- [Help I need support!](#help-i-need-support)/我需要帮助！
  - [Discord Server](#discord-server)/discord频道
  - [FaceSwap Forum](#faceswap-forum)/faceswap论坛
- [Donate](#donate)/捐赠
  - [Patreon](#patreon)
  - [One time Donations](#one-time-donations)
    - [@torzdf](#torzdf)
    - [@andenixa](#andenixa)
    - [@kvrooman](#kvrooman)
- [How to contribute](#how-to-contribute)
  - [For people interested in the generative models](#for-people-interested-in-the-generative-models)
  - [For devs](#for-devs)
  - [For non-dev advanced users](#for-non-dev-advanced-users)
  - [For end-users](#for-end-users)
  - [For haters](#for-haters)
- [About github.com/deepfakes](#about-githubcomdeepfakes)
  - [What is this repo?](#what-is-this-repo)
  - [Why this repo?](#why-this-repo)
  - [Why is it named 'deepfakes' if it is not /u/deepfakes?](#why-is-it-named-deepfakes-if-it-is-not-udeepfakes)
  - [What if /u/deepfakes feels bad about that?](#what-if-udeepfakes-feels-bad-about-that)
- [About machine learning](#about-machine-learning)
  - [How does a computer know how to recognize/shape faces? How does machine learning work? What is a neural network?](#how-does-a-computer-know-how-to-recognizeshape-faces-how-does-machine-learning-work-what-is-a-neural-network)

# Manifesto/声明

## FaceSwap has ethical uses./FaceSwap使用道德标准，也就是什么可以做，什么不能做。此处略去不表



# How To setup and run the project/怎么设置和运行项目
FaceSwap is a Python program that will run on multiple Operating Systems including Windows, Linux, and MacOS.

FaceSwap是一个可以运行在多个操作系统（包括Windows，Linux和MacOx）的python程序。

See [INSTALL.md](INSTALL.md) for full installation instructions. You will need a modern GPU with CUDA support for best performance. AMD GPUs are partially supported.

查看[INSTALL.md](INSTALL.md)安装文档以获取完整的安装指导。你为了得到最好的性能需要一个带有CUDA支持的现代的GPU（显卡）。部分支持AMD的GPU（显卡）。

# Overview/总览
The project has multiple entry points. You will have to:

这个项目有多个接入点。你必须：
 - Gather photos and/or videos 收集照片和/或视频素材
 - **Extract** faces from your raw photos 从原始的照片中提取脸部
 - **Train** a model on the faces extracted from the photos/videos 用提取出的脸部训练出一个模型
 - **Convert** your sources with the model 转换训练后的模型

Check out [USAGE.md](USAGE.md) for more detailed instructions.

查看[USAGE.md](USAGE.md)使用方法文档来获取更多的指导。

## Extract/提取
From your setup folder, run `python faceswap.py extract`. This will take photos from `src` folder and extract faces into `extract` folder.

从你的setup文件夹中，运行“python faceswap.py extract”命令。这将从“src”文件夹中获取照片并提取出面部保存到“extract”文件夹中。

## Train/训练
From your setup folder, run `python faceswap.py train`. This will take photos from two folders containing pictures of both faces and train a model that will be saved inside the `models` folder.

从你的setup文件夹中，运行“python faceswap.py train”命令。这将从两个都包含脸部的文件夹中获取照片并训练出一个模型保存在“models”文件夹中。

## Convert/转换
From your setup folder, run `python faceswap.py convert`. This will take photos from `original` folder and apply new faces into `modified` folder.

从你的setup文件夹中，运行“python faceswap.py convert”命令。这将从original文件夹中获取照片然后应用新的脸部保存到“modified”文件夹中。

## GUI/图形界面
Alternatively, you can run the GUI by running `python faceswap.py gui`

相似的，你也可以通过“python faceswap.py gui”命令来运行图形界面（GUI）。

# General notes:/通常提示
- All of the scripts mentioned have `-h`/`--help` options with arguments that they will accept. You're smart, you can figure out how this works, right?!
- 所有提到带有-h/--help选项的脚本都可以接受这个参数。你很聪明，你能找到这是怎么运作的，对吧？！

NB: there is a conversion tool for video. This can be accessed by running `python tools.py effmpeg -h`. Alternatively, you can use [ffmpeg](https://www.ffmpeg.org) to convert video into photos, process images, and convert images back to the video.

NB：有一个专为视频准备的转化工具。可以通过运行“python tools.py effmpeg -h”命令来访问。相似的，你也可以使用 [ffmpeg](https://www.ffmpeg.org) 转化视频到照片，然后处理图像，然后再把图像转换回视频。

**Some tips:/一些提示**

Reusing existing models will train much faster than starting from nothing./重复使用已经存在的模型来训练比什么都没有就开始训练速度快很多。
If there is not enough training data, start with someone who looks similar, then switch the data./如果没有足够的训练数据，从找一个相似的面孔开始，然后再切换数据。

# Help I need support!/我需要帮助！
## Discord Server/discord频道
Your best bet is to join the [FaceSwap Discord server](https://discord.gg/FC54sYg) where there are plenty of users willing to help. Please note that, like this repo, this is a SFW Server!

## FaceSwap Forum/faceswap论坛
Alternatively, you can post questions in the [FaceSwap Forum](https://faceswap.dev/forum). Please do not post general support questions in this repo as they are liable to be deleted without response.

# Donate/捐赠
The developers work tirelessly to improve and develop FaceSwap. Many hours have been put in to provide the software as it is today, but this is an extremely time-consuming process with no financial reward. If you enjoy using the software, please consider donating to the devs, so they can spend more time implementing improvements.

## Patreon
The best way to support us is through our Patreon page:

[![become-a-patron](https://c5.patreon.com/external/logo/become_a_patron_button.png)](https://www.patreon.com/bePatron?u=23238350)

## One time Donations
Alternatively you can give a one off donation to any of our Devs:
### @torzdf
 There is very little FaceSwap code that hasn't been touched by torzdf. He is responsible for implementing the GUI, FAN aligner, MTCNN detector and porting the Villain, DFL-H128 and DFaker models to FaceSwap, as well as significantly improving many areas of the code.

**Bitcoin:** bc1qpm22suz59ylzk0j7qk5e4c7cnkjmve2rmtrnc6

**Ethereum:** 0xd3e954dC241B87C4E8E1A801ada485DC1d530F01

**Monero:** 45dLrtQZ2pkHizBpt3P3yyJKkhcFHnhfNYPMSnz3yVEbdWm3Hj6Kr5TgmGAn3Far8LVaQf1th2n3DJVTRkfeB5ZkHxWozSX

**Paypal:** [![torzdf](https://www.paypalobjects.com/en_GB/i/btn/btn_donate_SM.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=JZ8PP3YE9J62L)

### @andenixa
Creator of the Unbalanced and OHR models, as well as expanding various capabilities within the training process. Andenixa is currently working on new models and will take requests for donations.

**Paypal:** [![andenixa](https://www.paypalobjects.com/en_GB/i/btn/btn_donate_SM.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=NRVLQYGS6NWTU)

# How to contribute

## For people interested in the generative models
 - Go to the 'faceswap-model' to discuss/suggest/commit alternatives to the current algorithm.

## For devs
 - Read this README entirely
 - Fork the repo
 - Play with it
 - Check issues with the 'dev' tag
 - For devs more interested in computer vision and openCV, look at issues with the 'opencv' tag. Also feel free to add your own alternatives/improvements

## For non-dev advanced users
 - Read this README entirely
 - Clone the repo
 - Play with it
 - Check issues with the 'advuser' tag
 - Also go to the '[faceswap Forum](https://faceswap.dev/forum)' and help others.

## For end-users
 - Get the code here and play with it if you can
 - You can also go to the [faceswap Forum](https://faceswap.dev/forum) and help or get help from others.
 - Be patient. This is a relatively new technology for developers as well. Much effort is already being put into making this program easy to use for the average user. It just takes time!
 - **Notice** Any issue related to running the code has to be opened in the [faceswap Forum](https://faceswap.dev/forum)!

## For haters
Sorry, no time for that.

# About github.com/deepfakes

## What is this repo?
It is a community repository for active users.

## Why this repo?
The joshua-wu repo seems not active. Simple bugs like missing _http://_ in front of urls have not been solved since days.

## Why is it named 'deepfakes' if it is not /u/deepfakes?
 1. Because a typosquat would have happened sooner or later as project grows
 2. Because we wanted to recognize the original author
 3. Because it will better federate contributors and users

## What if /u/deepfakes feels bad about that?
This is a friendly typosquat, and it is fully dedicated to the project. If /u/deepfakes wants to take over this repo/user and drive the project, he is welcomed to do so (Raise an issue, and he will be contacted on Reddit). Please do not send /u/deepfakes messages for help with the code you find here.

# About machine learning

## How does a computer know how to recognize/shape faces? How does machine learning work? What is a neural network?
It's complicated. Here's a good video that makes the process understandable:
[![How Machines Learn](https://img.youtube.com/vi/R9OHn5ZF4Uo/0.jpg)](https://www.youtube.com/watch?v=R9OHn5ZF4Uo)

Here's a slightly more in depth video that tries to explain the basic functioning of a neural network:
[![How Machines Learn](https://img.youtube.com/vi/aircAruvnKk/0.jpg)](https://www.youtube.com/watch?v=aircAruvnKk)

tl;dr: training data + trial and error
