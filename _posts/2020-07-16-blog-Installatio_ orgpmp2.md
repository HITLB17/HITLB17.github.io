---
title: 'Installation orgpmp2'
date: 2020-7-16
permalink: /posts/2020/07/Installation orgpmp2/
tags:
  - ubuntu
  - software install
  - orgpmp2
---

orgpmp2 is a OpenRAVE plugin for GPMP2 (Gaussian Process Motion Planner 2) algorithm described in Motion Planning as Probabilistic Inference using Gaussian Processes and Factor Graphs (RSS 2016). Examples provided for WAM arm and PR2 use python scripts. orgpmp2 is being developed by Mustafa Mukadam and Jing Dong as part of their work at Georgia Tech Robot Learning Lab and is a modified version of CHOMP openrave plugin.

### 1.Install ROS

based on you system (Recommend [kinetic]<http://wiki.ros.org/kinetic/Installation/Ubuntu>)

### 2.Install OpenRAVE

you can install  install [the fork]<https://github.com/gtrll/openrave> which has fixed few minor bugs.

```bash
sudo apt-get install libpcre++-dev libopenscenegraph-dev openscenegraph libboost-python-dev python python-dev python-numpy ipython python-scipy python-sympy liblapack-dev liblapacke-dev libode-dev libbullet-dev libsoqt4-dev libgmp3-dev libmpfr-dev libmpfi-dev collada-dom2.4-dp* assimp-utils
```

```bash
git clone https://github.com/gtrll/openrave.git
cd openrave & mkdir build & cd build
cmake ..
sudo make install

export PYTHONPATH=$PYTHONPATH:`openrave-config --python-dir`
source `openrave-config --share-dir`/openrave.bash
```

### 3.Install [GPMP2]<https://github.com/gtrll/gpmp2> core C++ 

####   Prerequisites:

1. CMake >= 2.6 (Ubuntu: sudo apt-get install cmake), compilation configuration tool.

2. Boost >= 1.50 (Ubuntu: sudo apt-get install libboost-all-dev), portable C++ source libraries.

   dpkg -S /usr/include/boost/version.hpp

3. GTSAM >= 4.0 alpha, a C++ library that implement smoothing and mapping (SAM) framework in robotics and vision. Here we use factor graph implementations and inference/optimization tools provided by GTSAM.

```bash
  git clone https://bitbucket.org/gtborg/gtsam/src
  cd src & mkdir build & cd build
  cmake ..
  make check
  sudo make install
```

​	**Test** if GTSAM install successfully: 

```
make
make VisualISAM2Example 
make VisualISAM2Example.run. 
```

4. Intel Threaded Building Blocks (TBB) (Ubuntu: sudo apt-get install libtbb-dev)
5. Intel Math Kernel Library (MKL) (Ubuntu: [installing using APT] <https://software.intel.com/content/www/us/en/develop/articles/installing-intel-free-libs-and-python-apt-repo.html>)

####   Installation GPMP2

```shell
git clone https://github.com/gtrll/gpmp2.git
cd gpmp2 & mkdir build & cd build
cmake ..
make check
sudo make install
```

 **Install Matlab Toolbox**

```shell
cmake -DGPMP2_BUILD_MATLAB_TOOLBOX:OPTION=ON -DGTSAM_TOOLBOX_INSTALL_PATH:PATH=/path/install/toolbox ..
sudo make install
```

#####    Problems:

​	if there is some problems when you cmake like the following picture:

![error](https://github.com/HITLB17/HITLB17.github.io/blob/master/images/blog_figure/20200716-1.png?raw=true)

**run the following code at the terminal**

```shell
sudo gedit /usr/local/lib/cmake/GTSAM/GTSAMConfig.cmake
```

​	line 17:  modify `find_dependency`改成`find_package`
​	then cmake gpmp2 package again.

### 4.Dependencies

```
sudo apt-get install gfortran libgsl0-dev python-enum
```

### 5.Initialize a catkin workspace

```shell
mkdir -p ~/gpmp2_catkin_ws/src
cd gpmp2_catkin_ws/src
catkin_init_workspace
```

### 6.git clone in folder gpmp2_catkin_ws/src

git clone https://github.com/gtrll/orgpmp2.git
git clone https://github.com/personalrobotics/openrave_catkin.git
git clone https://github.com/personalrobotics/prpy.git

### 7. Compile the catkin workspace

```
cd ~/gpmp2_catkin_ws
catkin_make -DCMAKE_BUILD_TYPE=Release
```

Before running the examples, the last step is setup the environment variables

```shell
source ~/gpmp2_catkin_ws/devel/setup.bash
```

